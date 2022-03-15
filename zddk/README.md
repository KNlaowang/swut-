
## 特色
 - 支持多用户使用

 - 支持默认表单模板或学校自定义模板

 - 支持将所有打卡结果推送给指定的一人

## 开始使用
### 在 GitHub Actions 上使用

1. `Star`并`Fork`本项目

2. 前往 `Settings`-`Secrets` ， 点击 `New repository secret`

3. 在新建 Secret 的界面上， `Name` 值输入 `USERS` ， `Value` 处输入用户的配置信息，多个用户配置之间使用`英文分号`隔开。
   
   单个用户的配置信息格式如下（[ ]内为可选参数）：
   ```
   username,password,post_type[,school_id,api_type,api_key]
   ```
   
   `username`, `password` 分别是学号和密码
   
   `post_type`是本程序目前支持填报的表单代码，详情见[支持的学校表单](#支持的学校表单)中的[表单代码]一栏
   
   `school_id`是学校代号，获取方法见[学校id获取](#学校id获取)
   
   `api_type`, `api_key`是消息推送类型代号及密钥，详情见[消息推送介绍](#消息推送介绍)
   
   示例如下：
   
   用户需要消息推送服务，并且使用学号登录：
   ```
   20192233,12345Abc,default,209,2,5e58d2264821c69ebcd46c448e7f5fe6
   ```
   
   若用户不使用学号登录，或者不需要使用消息推送服务，则**按照上述格式的顺序**，仅保留需要的参数即可

   例如用户使用手机号而不是学号登录，需要消息推送服务：
   
   ```
   13878000000,5678Zyx,default,2,46d002ca1ed0c82e1c251a9e5893cd62
   ```
   
   使用手机号登录，仅需要基础功能：

   ```
   18866000000,8899Qwe,nnnu
   ```
   
   要注意不能以`,`作为末尾

   多用户时，每个用户的配置信息用英文分号`;`间隔：

   ```
   20192233,12345Abc,default,209,2,5e58d2264821c69ebcd46c448e7f5fe6;13878000000,5678Zyx,default,2,46d002ca1ed0c82e1c251a9e5893cd62;18866000000,8899Qwe,nnnu
   ```

   同样注意末尾不需要有分号`;`  

   完成后点击`Add secret`保存该 Secret
   
4. （可选）用同样的方法添加一个名为 `SEND` 的 Secret ，用于将所有用户的填报结果推送给管理员。

   格式为`api_type,api_key`，例如

   ```
   2,5e58d2264821c69ebcd46c448e7f5fe6
   ```

5. （可选）再添加一个名为 `LOGPASS` 的 Secret ，用于将 GitHub Actions 的执行结果日志加密。

   这是因为 GitHub Actions 的日志是公开的，设置该 Secret 后会将日志文件用 7z 加密压缩并上传，可在每个 Action 页面的 Artifacts 处下载，使用任意解压软件解压即可查看。

   若不设置该 Secret 则不会保留日志，也无法查看，除非设置了消息推送可以查看填报结果。

6. Secret 添加完成后，前往项目的 `Actions` 面板，同意开启并进入 Actions 。然后选择 `Health Report` ，点击 `Enable workflow` 开启工作流。此时 Actions 开启成功，可以点击 `Run workflow` 测试填报一次。

7. 当本项目更新时，你所 Fork 的项目不会自动更新。在你的项目主页上点击 `Fetch upstream`-`Fetch and merge`以更新程序。


## 表单
| 表单代码 | 名称 | 备注 |
| :---: | :---: | :---: |
| test  | 测试用表单 | 一个不限时间和次数的填报表单，[表单主页](http://office.chaoxing.com/front/web/apps/forms/fore/apply?id=13243&enc=3a9416c86432c5f667f2b23a88a0123a)
| default | 学习通默认健康打卡表单 | 绝大部分学校所用，[表单主页](http://office.chaoxing.com/front/web/apps/forms/fore/apply?id=7185&enc=f837c93e0de9d9ad82db707b2c27241e)
| swut | 山东外国语职业技术大学健康打卡 | [表单主页](https://office.chaoxing.com/front/web/apps/forms/fore/apply?id=139669&enc=d3fd2b1818f116a76aff41eee80ea348) |
| swut | 山东外国语职业技术大学学生午检 | [表单主页](http://office.chaoxing.com/front/web/apps/forms/fore/apply?id=175235&enc=fb50b811a71a357bbb3a87424f7c074c) |

## 消息推送介绍
目前支持以下消息推送服务：

| 接口代号 | 名称| 官网 |
| :---: | :---: | :---: |
| 1 | Server酱 | https://sct.ftqq.com/ |
| 2 | 推送加 | https://www.pushplus.plus/ |
| 3 | 推送加（hxtrip域名下） | https://pushplus.hxtrip.com/ |

请前往任意官网注册得到`key`后即可在本项目中使用，在项目中使用时注意接口代号正确设置。

## 学校id获取
1. 访问 http://passport2.chaoxing.com/login

2.找到自己学习鼠标右击检查



