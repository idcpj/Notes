[TOC]

## 设置风格
```
创建(注册)   /user            post    code:201(创建成功),400(请求错误),500(服务器内部错误)
用户登陆    /usr/:username    post    code: 200(ok),400,500
获取用户信息  /user/:username  get  code:200,300,401(没有验证),403(验证不通过),500
用户注销    /user/:username    delete  code:204(删除成功),400,401,403,500
```