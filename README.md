# Ruby_Bundler（中文参考）
![](http://bundler.io/images/gembundler.png)

## Bundler 是什么？
> Bundler能够跟踪并安装所需的特定版本的gem，以此来为Ruby项目提供一致的运行环境。  
> Bundler是Ruby依赖管理的一根救命稻草，它可以保证你所要依赖的gem如你所愿地出现在开发、测试和生产环境中。利用Bundler启动项目简单到只用一条命令：``` bundle install ``` 

## 快速上手
Bundler使用起来非常简单。  

**第一步：打开命令行输入如下命令：**  
```
$ gem install bundler
```  

**第二步：在Ruby项目的根目录下新建文件 _Gemfile_（更多关于Gemfile参考后文）**  
文件内容像下面这样：  
> **source 'https://rubygems.org'  \# gem源地址  
gem 'nokogiri'                     \# 被依赖的gem，不指定版本默认安装最新版本  
gem 'rack', '~>1.1'                \# 指定版本  
gem 'rspec', :require => 'spec'    \# 指定依赖关系**  

**第三步：利用Bundler从你指定的gem源地址下载安装gem**  
```
$ bundle install
```  
```
$ git add Gemfile Gemfile.lock
```  

第一条bundle install命令执行完成之后，所有在Gemfile中指定的依赖gem会被安装到当前的环境中，并且在Gemfile的同级目录下会生成一个新的文件： **_Gemfile.lock_**,这个文件里会详细列出Gem,Platform以及Dependency的信息。  
第二条git命令将Gemfile和Gemfile.lock两个文件添加到你的git版本库中，这样做的好处是，可以确保其他开发者以及在不同的开发环境下，你的项目会依赖到完全相同的第三方库。  

## 更详细的介绍
#### Gemfile
Gemfile应该包含至少一个gem源地址，源地址以URL的形式指定：  
> **source 'https://rubygems.org'**  

用```bundle init```命令可以生成Gemfile，缺省的gem源地址是rubygems.org  
**_如果包含不止一个gem源地址，Bundler查找的顺序是从最后一行源地址往第一行查。_**  
有的gem源需要用户名和密码才可以连接，对于这种源可以使用```bundle config```命令设置名户名和密码，并且每次换新环境在执行install之前都要设置一次。 
```
$ bundle config https://gems.example.com/ user:password
```  

有些公司配置的gem源，身份信息可以直接写在源地址的URL中：  
> **source "https://user:password@gems.example.com"**  

**_直接写在URL中的身份信息优先级高于_**```config```  
跟在source后面的就是你要依赖的gem的声明，包括gem名称和版本号。
> **gem 'nokogiri'  
    gem 'rails', '3.0.0.beta3'  
    gem 'rack',  '>=1.0'  
    gem 'thin',  '~>1.1'**  

