[TOC]

## 安装
```

//isntall &Update pm2 :
npm install pm2 -g && pm2 update

//Start and add a process to the pm2 process list:
pm2 start app.js [--name app]

//Show the process list:
pm2 ls

//Stop and delete a process from the pm2 process list:
pm2 delete app

//Stop, start and restart a process from the process list:
pm2 stop (app|all)
pm2 start (app|all)
pm2 restart (app|all)

//监控访问信息 , js 的 `console.log()`会打印出来
pm2 monit
pm2 logs 
```