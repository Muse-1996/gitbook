# time包

#### 获取当前时间

```go
t := time.Now()
fmt.Println(t)  //2021-01-17 10:39:34.684213 +0800 CST m=+0.000149615
fmt.Printf("%T\n",t)  //time.Time
```

#### 获取指定时间

```go
t2 := time.Date(2020,1,24,18,18,18,0,time.Local)
fmt.Println(t2)  //2020-12-24 18:18:18 +0800 CST
fmt.Printf("%T\n",t2)  //time.Time
```

#### 时间格式化到字符串

```go
t2 := time.Date(2020,1,24,18,18,18,0,time.Local)
str := t2.Format("2006-01-02 15:04:05")
fmt.Println(str)  //2020-01-24 18:18:18
```

#### 时间字符串解析到日期

```go
t3Str := "2020-12-12"
pt,err := time.Parse("2006-01-02",t3Str)
if err != nil{
    fmt.Println(err)
}
fmt.Println(pt) //2020-12-12 00:00:00 +0000 UTC
```

#### 时间获取年月日等

```go
t3 := time.Now()
fmt.Println(t3.Year())    //2021
fmt.Println(t3.YearDay()) //17  今年已经过了多少天
fmt.Println(t3.Month())   //January
fmt.Println(t3.Day())     //17
fmt.Println(t3.Hour())    //10
fmt.Println(t3.Minute())  //51
fmt.Println(t3.Second())  //4
```

#### 获取年月日时分秒简单写法

```go
y,m,d := t3.Date()  // 获取 年月日
fmt.Println(y,m,d)  //2021 January 17
h,min,s := t3.Clock() // 获取 时分秒
fmt.Println(h,min,s) //10 54 55
```

#### 获取时间戳

```go
fmt.Printf("%v\n",t3.Unix())  //1610852241  秒差值
fmt.Printf("%v\n",t3.UnixNano() / 1e6)  //1610852437110  毫秒
fmt.Printf("%v\n",t3.UnixNano())  //1610852319907460000  纳秒差值
```

#### 睡眠，相当于Python的sleep

```go
time.Sleep(time.Second * 5)
```

