# Puppeteer爬虫开发

> \#背景
>
> 前段时间学习Flutter的时候准备写一个实用的影视工具，通过各大视频网站的播放地址获取真实地址在APP上进行播放，网上有很多这种VIP资源解析的网站，但是iframe嵌套很深，基本都是异步渲染，而且时不时会出现让人心跳加速的小广告，这显然是不合适的...

基于这种比较七八个iframe嵌套的网页，爬取数据用superagent显然不够用了；经过一番摸索，发现Puppeteer完全可以实现需求，而且非常强大，而且非常适合测试人员使用。感觉上像是给程序里加了一个浏览器，可以通过代码控制和操作很多内容，当然，对单页面网站的爬取也是可以的。

[Puppeteer](https://www.npmjs.com/package/puppeteer)是一个Node库，它提供了高级API来通过[DevTools协议](https://chromedevtools.github.io/devtools-protocol/)控制Chrome或Chromium 。

### 安装依赖

```bash
cnpm install puppeteer -S
```

### 基本使用

```javascript
//这里的args参数是因为在Linux服务器环境没有图像渲染的依赖，如果在本地开发，则不需要配置
const browser = await puppeteer.launch({ args: ['--no-sandbox', '--disable-setuid-sandbox'] });
//想象打开一个新的页面
const page = await browser.newPage();
//监听页面的一些行为
page.on('response', msg => {
    let stu = msg.status();
    let req = msg.request();
    let res;
    //xhr 看过浏览器控制台network的都明白吧
    if (req.resourceType() == 'xhr') {
        res = msg.json()
    }
    if (req.resourceType() == 'xhr' && stu == 200) {
        res.then((_res) => {
            if (_res.msg == 'ok') {
                //_res.url
                //这里可以获取到请求的连接
            }
        })
    }
})
//加载链接
await page.goto("这里是要打开的URL");
//完成操作后，关闭浏览器
await browser.close();
```

这里只是基于Puppeteer的一个小功能实现的爬虫思路，不过感觉大批量爬取数据应该是效率不高的，但是好在灵活和强大，非常适合做自动化测试的工作，更多的用法和api请参考官方文档。

