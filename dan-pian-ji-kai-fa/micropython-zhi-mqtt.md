# MicroPython之MQTT

### 1.编辑boot.py进行基本数据设置

```python
# This file is executed on every boot (including wake-boot from deepsleep)
import time

from umqttsimple import MQTTClient

import ubinascii

import machine

import micropython

import network

import esp
#设置debug为None，激活垃圾收集器。
esp.osdebug(None)

import uos
#uos.dupterm(None, 1) # disable REPL on UART(0)
import gc
import webrepl
webrepl.start()
gc.collect()



#定义一些必要的变量，包括本地WiFi账号与密码，mqtt服务器IP地址，MQTT用户名与密码，mqtt客户端id，发布与订阅的主题，接收消息的时间间隔等。
ssid = 'WIFI NAME'

password = 'WIFI PASSWORD'

mqtt_server = 'MQTT SERVER (xxx.xxx.xxx.xxx)'

mqtt_user=''

mqtt_pwd=''

client_id = ubinascii.hexlify(machine.unique_id())

#热点开启
wifiCode = str(client_id).split("'")[1]
ap = network.WLAN(network.AP_IF)
ap.active(True)
#给热点开启密码验证 并且热点名称中包含设备ID - wifiCode
ap.config(essid='Monster-'+wifiCode,authmode=network.AUTH_WPA_WPA2_PSK, password="hellobaby")

#订阅频道
topic_sub = b""+client_id

#消息推送频道
topic_pub = b""+client_id+'After'

last_message = 0

#心跳速率
message_interval = 5

counter = 0

#接入网络


station = network.WLAN(network.STA_IF)

station.active(True)

station.connect(ssid, password)

while station.isconnected() == False:
	pass

print('Connection successful')

print(station.ifconfig())
```

### 2.上传umqttsimple.py

```python
try:
	import usocket as socket
except:
	import socket
import ustruct as struct
from ubinascii import hexlify

class MQTTException(Exception):
	pass

class MQTTClient:

	def __init__(self, client_id, server, port=0, user=None, password=None, keepalive=0,
				 ssl=False, ssl_params={}):
		if port == 0:
			port = 8883 if ssl else 1883
		self.client_id = client_id
		self.sock = None
		self.server = server
		self.port = port
		self.ssl = ssl
		self.ssl_params = ssl_params
		self.pid = 0
		self.cb = None
		self.user = user
		self.pswd = password
		self.keepalive = keepalive
		self.lw_topic = None
		self.lw_msg = None
		self.lw_qos = 0
		self.lw_retain = False

	def _send_str(self, s):
		self.sock.write(struct.pack("!H", len(s)))
		self.sock.write(s)

	def _recv_len(self):
		n = 0
		sh = 0
		while 1:
			b = self.sock.read(1)[0]
			n |= (b & 0x7f) << sh
			if not b & 0x80:
				return n
			sh += 7

	def set_callback(self, f):
		self.cb = f

	def set_last_will(self, topic, msg, retain=False, qos=0):
		assert 0 <= qos <= 2
		assert topic
		self.lw_topic = topic
		self.lw_msg = msg
		self.lw_qos = qos
		self.lw_retain = retain

	def connect(self, clean_session=True):
		self.sock = socket.socket()
		addr = socket.getaddrinfo(self.server, self.port)[0][-1]
		self.sock.connect(addr)
		if self.ssl:
			import ussl
			self.sock = ussl.wrap_socket(self.sock, **self.ssl_params)
		premsg = bytearray(b"\x10\0\0\0\0\0")
		msg = bytearray(b"\x04MQTT\x04\x02\0\0")

		sz = 10 + 2 + len(self.client_id)
		msg[6] = clean_session << 1
		if self.user is not None:
			sz += 2 + len(self.user) + 2 + len(self.pswd)
			msg[6] |= 0xC0
		if self.keepalive:
			assert self.keepalive < 65536
			msg[7] |= self.keepalive >> 8
			msg[8] |= self.keepalive & 0x00FF
		if self.lw_topic:
			sz += 2 + len(self.lw_topic) + 2 + len(self.lw_msg)
			msg[6] |= 0x4 | (self.lw_qos & 0x1) << 3 | (self.lw_qos & 0x2) << 3
			msg[6] |= self.lw_retain << 5

		i = 1
		while sz > 0x7f:
			premsg[i] = (sz & 0x7f) | 0x80
			sz >>= 7
			i += 1
		premsg[i] = sz

		self.sock.write(premsg, i + 2)
		self.sock.write(msg)
		#print(hex(len(msg)), hexlify(msg, ":"))
		self._send_str(self.client_id)
		if self.lw_topic:
			self._send_str(self.lw_topic)
			self._send_str(self.lw_msg)
		if self.user is not None:
			self._send_str(self.user)
			self._send_str(self.pswd)
		resp = self.sock.read(4)
		assert resp[0] == 0x20 and resp[1] == 0x02
		if resp[3] != 0:
			raise MQTTException(resp[3])
		return resp[2] & 1

	def disconnect(self):
		self.sock.write(b"\xe0\0")
		self.sock.close()

	def ping(self):
		self.sock.write(b"\xc0\0")

	def publish(self, topic, msg, retain=False, qos=0):
		pkt = bytearray(b"\x30\0\0\0")
		pkt[0] |= qos << 1 | retain
		sz = 2 + len(topic) + len(msg)
		if qos > 0:
			sz += 2
		assert sz < 2097152
		i = 1
		while sz > 0x7f:
			pkt[i] = (sz & 0x7f) | 0x80
			sz >>= 7
			i += 1
		pkt[i] = sz
		#print(hex(len(pkt)), hexlify(pkt, ":"))
		self.sock.write(pkt, i + 1)
		self._send_str(topic)
		if qos > 0:
			self.pid += 1
			pid = self.pid
			struct.pack_into("!H", pkt, 0, pid)
			self.sock.write(pkt, 2)
		self.sock.write(msg)
		if qos == 1:
			while 1:
				op = self.wait_msg()
				if op == 0x40:
					sz = self.sock.read(1)
					assert sz == b"\x02"
					rcv_pid = self.sock.read(2)
					rcv_pid = rcv_pid[0] << 8 | rcv_pid[1]
					if pid == rcv_pid:
						return
		elif qos == 2:
			assert 0

	def subscribe(self, topic, qos=0):
		assert self.cb is not None, "Subscribe callback is not set"
		pkt = bytearray(b"\x82\0\0\0")
		self.pid += 1
		struct.pack_into("!BH", pkt, 1, 2 + 2 + len(topic) + 1, self.pid)
		#print(hex(len(pkt)), hexlify(pkt, ":"))
		self.sock.write(pkt)
		self._send_str(topic)
		self.sock.write(qos.to_bytes(1, "little"))
		while 1:
			op = self.wait_msg()
			if op == 0x90:
				resp = self.sock.read(4)
				#print(resp)
				assert resp[1] == pkt[2] and resp[2] == pkt[3]
				if resp[3] == 0x80:
					raise MQTTException(resp[3])
				return

	# Wait for a single incoming MQTT message and process it.
	# Subscribed messages are delivered to a callback previously
	# set by .set_callback() method. Other (internal) MQTT
	# messages processed internally.
	def wait_msg(self):
		res = self.sock.read(1)
		self.sock.setblocking(True)
		if res is None:
			return None
		if res == b"":
			raise OSError(-1)
		if res == b"\xd0":  # PINGRESP
			sz = self.sock.read(1)[0]
			assert sz == 0
			return None
		op = res[0]
		if op & 0xf0 != 0x30:
			return op
		sz = self._recv_len()
		topic_len = self.sock.read(2)
		topic_len = (topic_len[0] << 8) | topic_len[1]
		topic = self.sock.read(topic_len)
		sz -= topic_len + 2
		if op & 6:
			pid = self.sock.read(2)
			pid = pid[0] << 8 | pid[1]
			sz -= 2
		msg = self.sock.read(sz)
		self.cb(topic, msg)
		if op & 6 == 2:
			pkt = bytearray(b"\x40\x02\0\0")
			struct.pack_into("!H", pkt, 2, pid)
			self.sock.write(pkt)
		elif op & 6 == 4:
			assert 0

	# Checks whether a pending message from server is available.
	# If not, returns immediately with None. Otherwise, does
	# the same processing as wait_msg.
	def check_msg(self):
		self.sock.setblocking(False)
		return self.wait_msg()
```

### 3.编写业务代码 main.py

```python
import machine
import dht

ledState = 0
ledLight = machine.Pin(2, machine.Pin.OUT,value=1)
tiggerBtn = machine.Pin(0, machine.Pin.IN)

#定义一个订阅回调函数：

def sub_cb(topic, msg):
#	(b'1226d800', b'toggle')
	global topic_pub,ledState,ledLight,client
	if topic == topic_sub :
		if msg == b"on":
			ledLight.value(1)
			client.publish(topic_pub,b"on-1")
			ledState = 1
		elif msg == b"off":
			ledLight.value(0)
			client.publish(topic_pub,b"on-0")
			ledState = 0
		elif msg == b"toggle":
			# LED is inversed, so setting it to current state
			# value will make it toggle
			ledLight.value(ledState)
			client.publish(topic_pub,b"on-"+str(ledState))
			ledState = 1 - ledState
		elif msg == b"getTH":
			print("获取温湿度")
			

#定义一个连接MQTT服务器和订阅主题的函数：

def connect_and_subscribe():

	global client_id, mqtt_server, topic_sub,mqtt_user,mqtt_pwd
	
#	client = MQTTClient(client_id, mqtt_server,user=mqtt_user, password=mqtt_pwd, keepalive=60)
	
	client = MQTTClient(client_id, mqtt_server,keepalive=60)

	client.set_callback(sub_cb)

	client.connect()

	client.subscribe(topic_sub)

	print('Connected to %s MQTT broker, subscribed to %s topic' % (mqtt_server, topic_sub))

	return client

#定义一个重启和重新连接的函数：

def restart_and_reconnect():

	print('Failed to connect to MQTT broker. Reconnecting...')

	time.sleep(10)

	machine.reset()
	
#开始使用上面定义的函数连接MQTT服务器，订阅主题，并向after主题发布消息：
try:

	client = connect_and_subscribe()

except OSError as e:

	restart_and_reconnect()

while True:

	try:
		
		client.check_msg()

		if (time.time() - last_message) > message_interval:

#			msg = b'Hello #%d' % counter
			msg = b"t="+str(counter)

			client.publish(topic_pub, msg) 	

			last_message = time.time()

			counter += 1

	except OSError as e:

		restart_and_reconnect()
```

