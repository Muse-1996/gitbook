---
description: http长连接？
---

# 基于comet的HTTP数据推送技术

### Node

```text
router.get('/long',function(req,res,next){
  res.writeHead(200, {
    "Content-Type": "text/event-stream",
    "Cache-Control": "no-cache",
    "Connection": "keep-alive"
  });
  setInterval(function () {
    res.write("data: " + Date.now() + "\n\n");
  }, 1000);
})
```

