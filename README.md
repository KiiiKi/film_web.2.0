# film_web.2.0
#### 安装grunt
1. npm install grunt -g
2. npm install grunt-cli -g  （grunt的命令行接口，会把grunt命令植入到系统路径里，就允许从任意的目录来运行
3. 安装加载任务的插件  

#### 问题汇总：
##### 1. Fatal error: Unable to find local grunt.  
> 先安装grunt-cli后npm install grunt --save-dev  

##### 2. Running "concurrent:tasks" (concurrent) task卡住，不跳出窗口/localhost没有运行
```
//把nodemon改一下
nodemon: {
        dev: {
          script: './bin/www',
          options: {
            args: [],
            nodeArgs: ['--inspect'],
            ignore: ['README.md', 'node_modules/**', '.DS_Store'],
            ext: '',
            watch: ['./'],
            delay: 1000,
            env: {
              PORT: 3000
            },
            cwd: __dirname
          }
        }
    },
```

 ##### 3. pass option { useNewUrlParser: true } to MongoClient.connect.
 > 在routes/index里的mongoose.connect加上{ useNewUrlParser: true }
    
 ##### 4. 密码加盐哈希
 
 应该使用什么哈希算法：
 * 哈希加密算法，比如SHA256，SHA512，RipeMD，WHIRLPOOL，SHA3等等
 * 设计良好的密钥扩展算法，如PBKDF2，bcrypt，scrypt
 * 安全的crypt()版本（$2y$，$5$，$6$）
 
 ##### 5. 安装bcrypt出node-pre-gyp WARN Using needle for node-pre-gyp https download
 > npm install bcryptjs --save  
var bcrypt = require('bcryptjs')

 ##### 6. 录入到数据库不用自己新建库
 > 例如models/user.js中mongoose.model('User', UserSchema) 那么数据库中包含这些数据的库就自动建成users库，就是“模型名字”+“s”
 
 ##### 7. express4的cookie-parser和express-session安装
 > npm install express-session --save  
   npm install cookie-parser --save
  ```
    var cookieParser = require('cookie-parser')
    var session = require('express-session')
    app.use(cookieParser())
    app.use(session({
        secret: 'imooc'
    }))
  ```
  
 ##### 8. require('connect-mongo')时 Most middleware (like session) is no longer bundled with Express and must be installed separately.
 > 改成var mongoStore = require('connect-mongo')(session)
 
 ##### 9. 在router里挂载app.locals全局变量
 > res.locals属性仅在请求的生命期内有效。（相当于res.render），但是app.locals又是在app.js中用的，不能用在router中  
 在中间件中用req.app.local，此属性保存对使用中间件的Express应用程序的实例的引用。
 