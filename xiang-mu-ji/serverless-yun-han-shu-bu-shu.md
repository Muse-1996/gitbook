---
description: 腾讯云
---

# ServerLess云函数部署

无需购买和管理服务器的情况下运行代码。只需使用平台支持的语言编写核心代码并设置代码运行的条件，即可在腾讯云基础设施上弹性、安全地运行代码。SCF 是实时文件处理和数据处理等场景下理想的计算平台。

{% hint style="danger" %}
Egg.js项目中不能包含aliNode性能监控插件，因为该插件会操作目录，而云函数的运行环境内除 /tmp 目录下，其他均限制为只读。
{% endhint %}

越权操作目录报错内容

```bash
{"errorCode":-1,"errorMessage":"user code exception caught","stackTrace":"Error: EROFS: read-only file system, mkdir '/home/qcloud'
at Object.mkdirSync (fs.js:752:3)
at sync (/opt/node_modules/mkdirp/index.js:72:13)
at sync (/opt/node_modules/mkdirp/index.js:78:24)
at Function.sync (/opt/node_modules/mkdirp/index.js:78:24)
at module.exports.appInfo (/opt/node_modules/egg-alinode/config/config.default.js:15:10)
at AppWorkerLoader.loadFile (/opt/node_modules/egg-core/lib/loader/egg_loader.js:304:13)
at AppWorkerLoader._loadConfig (/opt/node_modules/egg-core/lib/loader/mixin/config.js:83:25)
at AppWorkerLoader.loadConfig (/opt/node_modules/egg-core/lib/loader/mixin/config.js:37:29)
at AppWorkerLoader.loadConfig (/opt/node_modules/egg/lib/loader/app_worker_loader.js:17:11)
at new EggApplication (/opt/node_modules/egg/lib/egg.js:54:17)"}
```

在项目`config.default.js`中增加配置

```text
//serverless 配置
config.rundir = '/tmp';
config.logger = {
    dir: '/tmp'
};
```

选用的Coding平台进行代码托管及自动化部署，在项目中新建构建计划，设置环境变量

![](../.gitbook/assets/image%20%2812%29.png)

根据需要设置触发条件

![](../.gitbook/assets/image%20%283%29.png)

编写构建流程

{% hint style="danger" %}
官方示例中安装serverless使用的\`npm i serverless-cli -g\`，这种写法会出错，在腾讯云官方文档中可见在linux环境下的安装命令

```bash
curl -o- -L https://slss.io/install | bash'
```
{% endhint %}

```bash
pipeline {
  agent any
  stages {
    stage('检出代码') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: GIT_BUILD_REF]],
          userRemoteConfigs: [[
            url: GIT_REPO_URL,
            credentialsId: CREDENTIALS_ID
          ]]])
        }
      }
      stage('安装serverless cli') {
        steps {
          sh 'curl -o- -L https://slss.io/install | bash'
        }
      }
      stage('部署') {
        steps {
          echo '部署中...'
          withCredentials([
            cloudApi(
              credentialsId: "Https证书ID",
              secretIdVariable: 'TENCENT_SECRET_ID',
              secretKeyVariable: 'TENCENT_SECRET_KEY'
            ),
          usernamePassword(
                credentialsId: "${env.CCI_CURRENT_PROJECT_COMMON_CREDENTIALS_ID}",
                passwordVariable: 'password',
                usernameVariable: 'userName'
              )
            ]) {
              sh 'echo "TENCENT_SECRET_ID=${TENCENT_SECRET_ID}/nTENCENT_SECRET_KEY=${TENCENT_SECRET_KEY}" > .env'
              sh 'sls deploy | tee console'
              //上边获取到了账号信息，用来发布项目公告，可省略
              script {
                def content = sh(script:'grep -A 6 customDomains console', returnStdout: true)
                content = "【${ENV}】<small>部署完成</small><br>"+"任务ID:${CI_BUILD_ID}<br>"+content.substring(content.indexOf("http"))
                sh "echo 'content=${content}' | curl --user ${userName}:${password} https://${CCI_CURRENT_TEAM}.coding.net/api/project/${PROJECT_ID}/tweet -d@-"
              }

              sh 'rm .env'
            }

                echo '部署完成'
              }
            }
          }
        }
```

