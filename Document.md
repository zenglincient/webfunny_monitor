## 监控后台部署教程

友情声明：部署后的版本难免会出现一些问题，希望大家及时提出来，我会尽快修复。

[【环境要求】](https://github.com/a597873885/webfunny_monitor/blob/master/Document.md#%E7%8E%AF%E5%A2%83%E8%A6%81%E6%B1%82)
[【部署步骤】](https://github.com/a597873885/webfunny_monitor/blob/master/Document.md#%E9%83%A8%E7%BD%B2%E6%AD%A5%E9%AA%A4)
[【常见问题】](https://github.com/a597873885/webfunny_monitor/blob/master/Document.md#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)

#### 环境要求：

node版本号： 10.6.0  (node安装教程自行搜索, 建议先安装[nvm](https://www.jianshu.com/p/d0e0935b150a), 这样切换node版本会方便很多)

mysql版本号. 5.6.45  (mysql 安装教程自行搜索 [Linux安装教程](https://www.cnblogs.com/warm-stranger/p/10333348.html))

#### 部署步骤

  1. 下载或者克隆代码到本地
  
  2. 执行测试命令(稍微耗时)$: npm run test_start
  
  3. 访问链接地址： [http://localhost:8010/home.html](http://localhost:8010/home.html) 即可看到官网数据。
  
  #### 那么如何展示自己的数据呢？
  
    【小提示】：项目错误日志都在更目下 logs/ 目录里，方便小伙伴们排查错误
  
  4. 在项目根目录下，进入 config/db.js ，配置mysql数据库的连接配置 （mysql必须先安装好,并手动创建一个数据库）
  
  5. 在项目根目录下，config.js文件中，进行如下配置：
  
          /**
           * 请求接口域名 webfunny-servers 的服务的部署域名
           * 本地请使用 "//localhost:8011"
           */
          const default_api_server_url = "//localhost:8011"

         /**
          * 静态资源域名 webfunny-admin 的部署域名
          * 本地请使用 "//localhost:8010"
          */
          const default_assets_url = "//localhost:8010"

  6. 配置完成后，再一次执行命令$: node config.js  来完成自定义配置
  
     服务所有的配置都配置好了，还差最后一步。
  
  7. 创建数据库表，执行命令$: npm run table_config 
  
    【提示】这个步骤需要耗费一些时间5-10分钟，请耐心等待。 数据库表生成后，在根目录下执行命令$:  npm run start, 本地服务完成启动。
  
  8. 生成你的探针代码，进入首页，点击 "新建" 按钮进入创建页面，探针生成后，将其插入到你的前端页面中，OK, 所有的部署都已经完成了。
  
  访问链接地址： [http://localhost:8010/home.html](http://localhost:8010/home.html) 即可看到你自己mysql里边的数据了（如果你的探针已经在上传数据了）。
  
  
  #### 常见问题
  
    0）正常情况下，更新后需要重新执行 node config 命令才能够正常运行，如果还是不行，请检查一下 config/db.js、config.js的内容是否被覆盖。

    1）报错日志一般都会在根目录下的logs里生成，帮助大家排查错误。

    2）有些数据会在一小时内生成，不要着急，有些是实时的。

    3）如需启动生产服务，需安装PM2, 然后运行命令$: npm run prd, 即可启动生产服务。

    4）数据库表都是程序自动创建的，但是（数据库）需要你手动创建

