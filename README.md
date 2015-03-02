# CocoaPods教程

## 1. 检查Ruby环境

CocoaPods本身是Ruby脚本语言编写的程序，因此我们首先需要安装Ruby环境。Mac OS X系统预装了Ruby，我们可以使用 `ruby -v` 或 `ruby --version` 命令查看当前的Ruby版本，如果终端打印出版本信息，则说明已安装了Ruby环境，例如：

```
$ ruby -v
ruby 2.1.2p95 (2014-05-08 revision 45877) [x86_64-darwin13.0]
```

## 2. 使用RubyGems
[RubyGems][10]（简称gems） 是Ruby附带的一款标准Ruby组件包（也称gem包）管理工具。CocoaPods就是这样一种gem包，因此我们需要通过RubyGems来下载和安装。

使用 `gem -v` 或 `gem --version` 命令查看当前RubyGems版本，如果终端打印出版本号信息则说明RubyGems已安装成功，例如：

```
$ gem -v
2.2.2
```

使用 `gem --help` 命令查看RubyGems的简介和基本使用，例如：

```
$ gem --help
RubyGems is a sophisticated package manager for Ruby.  This is a
basic help message containing pointers to more information.

  Usage:
    gem -h/--help
    gem -v/--version
    gem command [arguments...] [options...]

  Examples:
    gem install rake
    gem list --local
    gem build package.gemspec
    gem help install

  Further help:
    gem help commands            list all 'gem' commands
    gem help examples            show some examples of usage
    gem help gem_dependencies    gem dependencies file guide
    gem help platforms           gem platforms guide
    gem help <COMMAND>           show help on COMMAND
                                   (e.g. 'gem help install')
    gem server                   present a web page at
                                 http://localhost:8808/
                                 with info about installed gems
  Further information:
    http://guides.rubygems.org

```

使用 `gem update --system` 命令可以将RubyGems升级到最新版本，例如：

```
$ gem update --system
Updating rubygems-update
Fetching: rubygems-update-2.4.5.gem (100%)
Successfully installed rubygems-update-2.4.5
Parsing documentation for rubygems-update-2.4.5
Installing ri documentation for rubygems-update-2.4.5
Installing darkfish documentation for rubygems-update-2.4.5
Done installing documentation for rubygems-update after 2 seconds
Installing RubyGems 2.4.5
RubyGems 2.4.5 installed
Parsing documentation for rubygems-2.4.5
Installing ri documentation for rubygems-2.4.5
...
RubyGems system software updated

$ gem -v
2.4.5
```

使用 `gem install` 命令下载并安装一个Ruby组件包，例如：

```
$ gem install drip
Fetching: rbtree-0.4.2.gem (100%)
Building native extensions.  This could take a while...
Successfully installed rbtree-0.4.2
Fetching: drip-0.0.2.gem (100%)
Successfully installed drip-0.0.2
Parsing documentation for rbtree-0.4.2
Installing ri documentation for rbtree-0.4.2
Parsing documentation for drip-0.0.2
Installing ri documentation for drip-0.0.2
Done installing documentation for rbtree, drip after 0 seconds
2 gems installed
```

使用 `gem uninstall` 命令卸载一个Ruby组件包，例如：
```
$ gem uninstall drip
Successfully uninstalled drip-0.0.2
```
使用 `gem list` 命令查看所有已经安装的gem列表，例如：
```
$ gem list

*** LOCAL GEMS ***

activesupport (3.2.19)
bigdecimal (1.2.4)
blankslate (2.1.2.4)
...
```

### 如何更换gem源
gem源指下载gem包的服务器。由于国内网络原因（你懂的），默认gem源rubygems.org可能会出现间歇性无法连接的现象，这使你会遇到 `gem install` 命令半天无法响应的情况。因此，我们可以通过 `gem sources --remove` 和 `gem source --add` 命令来更换gem源。国内服务器比较推荐的是淘宝的RubyGems镜像（http://ruby.taobao.org/）。

更换gem源的详细步骤如下：

Step1. 使用 `gem sources` 命令查看当前使用的gem源。默认情况，gem源是RubyGems官方的。

```
$ gem sources
*** CURRENT SOURCES ***

https://rubygems.org/
```
Step2. 使用 `gem sources --remove` 命令删除原有官方gem源：

```
$ gem sources --remove https://rubygems.org/
https://rubygems.org/ removed from sources
```

Step3. 使用 `gem source --add` 命令添加新的淘宝gem源：

```
$ gem source --add http://ruby.taobao.org/
http://ruby.taobao.org/ added to sources
```

Step4. 再次检查当前gem源，确保修改成功：

```
$ gem source
*** CURRENT SOURCES ***

http://ruby.taobao.org/
```
注：gem源可以有多个，因此不删除原有的，直接添加新的也是可以的。但为了确保我们使用了期望的gem源，建议只保留一个。

## 3. 安装CocoaPods
使用 `gem install` 命令安装CocoaPods：

```
$ gem install cocoapods
Fetching: i18n-0.7.0.gem (100%)
Successfully installed i18n-0.7.0
Fetching: cocoapods-0.35.0.gem (100%)
Successfully installed cocoapods-0.35.0
Parsing documentation for i18n-0.7.0
Installing ri documentation for i18n-0.7.0
Parsing documentation for cocoapods-0.35.0
Installing ri documentation for cocoapods-0.35.0
Done installing documentation for i18n, cocoapods after 4 seconds
2 gems installed

```

使用 `pod --version` 命令查看当前版本以确保安装成功：

```
$ pod --version
0.35.0
```

使用 `pod --help` 命令查看CocoaPods的使用方法，例如：

```
$ pod --help
Usage:

    $ pod COMMAND

      CocoaPods, the Objective-C library package manager.

Commands:

    + init                Generate a Podfile for the current directory.
    + install             Install project dependencies to Podfile.lock versions
    + ipc                 Inter-process communication
    + lib                 Develop pods
    + list                List pods
    + outdated            Show outdated project dependencies
    + plugins             Show available CocoaPods plugins
    + repo                Manage spec-repositories
    + search              Searches for pods
    + setup               Setup the CocoaPods environment
    + spec                Manage pod specs
    + trunk               Interact with the CocoaPods API (e.g. publishing new
                          specs)
    + try                 Try a Pod!
    + update              Update outdated project dependencies and create new
                          Podfile.lock

Options:

    --silent              Show nothing
    --completion-script   Print the auto-completion script
    --version             Show the version of the tool
    --verbose             Show more debugging information
    --no-ansi             Show output without ANSI codes
    --help                Show help banner of specified command
```

使用 `pod setup` 命令下载CocoaPods仓库索引列表，例如：

```
$ pod setup --verbose

Setting up CocoaPods master repo

Creating shallow clone of spec repo `master` from `https://github.com/CocoaPods/Specs.git` (branch `master`)
  $ /usr/bin/git clone 'https://github.com/CocoaPods/Specs.git' master --depth=1
  Cloning into 'master'...
Checking out files: 100% (29778/29778), done.
  $ /usr/bin/git checkout master
  Already on 'master'
  Your branch is up-to-date with 'origin/master'.

CocoaPods 0.36.0.beta.2 is available.
To update use: `gem install cocoapods --pre`
[!] This is a test version we'd love you to try.

For more information see http://blog.cocoapods.org
and the CHANGELOG for this version http://git.io/BaH8pQ.

Setup completed

```

注：`pod setup` 就是将CocoaPods仓库索引目录（托管在 https://github.com/CocoaPods/Specs ）更新到本地的 ~/.cocoapods/目录下，目录结构如下：

```
~/.cocoapods
   |_ repos
       |_ master
           |_ CocoaPods-version.yml
           |_ README.md
           |_ Specs
              |_ 1PasswordExtension
                  |_ 1.0.0
                      |_ 1PasswordExtension.podspec.json
                  |_ ...
              |_ ...                
```
`podspec` 文件是pod的描述文件，json格式。

使用 `pod list` 命令查看本地仓库，例如：

```
$ pod list
  1PasswordExtension 1.1
  25519 1.8
  320Categories 0.2.2
  500px-iOS-api 1.0.5
  7blur 0.0.1
  A2DynamicDelegate 2.0.2
  A2StoryboardSegueContext 1.0.1
  A3GridTableView 0.0.1
  A3ParallaxScrollView 1.0.2
  ...
  zhihudailyAPI 1.0
  zip-archive-static-libary 1.0.0
  zipzap 8.0.3
  zxcvbn-ios 1.0.1
```
 
----
## 4. 为自己的iOS工程添加CocoaPods
Step1. 使用 `cd` 命令跳转到你的iOS工程根目录（即 `.xcodeproj` 文件所在目录）下，例如：

```
$ cd ~/Desktop/JYXCocoaPodsDemo/
$ ls -al
total 0
drwxr-xr-x   5 jyx  staff  170  2  8 13:01 .
drwx------+ 15 jyx  staff  510  2  8 13:01 ..
drwxr-xr-x  10 jyx  staff  340  2  8 13:01 JYXCocoaPodsDemo
drwxr-xr-x   5 jyx  staff  170  2  8 13:01 JYXCocoaPodsDemo.xcodeproj
drwxr-xr-x   4 jyx  staff  136  2  8 13:01 JYXCocoaPodsDemoTests
```

Step2. 使用 `pod init` 命令为工程创建名为 `Podfile` 的配置文件，例如：

```
$ pod init
$ ls -al
total 8
drwxr-xr-x   6 jyx  staff  204  2  8 13:03 .
drwx------+ 15 jyx  staff  510  2  8 13:01 ..
drwxr-xr-x  10 jyx  staff  340  2  8 13:01 JYXCocoaPodsDemo
drwxr-xr-x   5 jyx  staff  170  2  8 13:01 JYXCocoaPodsDemo.xcodeproj
drwxr-xr-x   4 jyx  staff  136  2  8 13:01 JYXCocoaPodsDemoTests
-rw-r--r--   1 jyx  staff  166  2  8 13:03 Podfile
```
使用 `cat` 命令查看初始Podfile的内容，例如：

```
$ cat Podfile 
# Uncomment this line to define a global platform for your project
# platform :ios, '6.0'

target 'JYXCocoaPodsDemo' do

end

target 'JYXCocoaPodsDemoTests' do

end
```

Step3. 定制Podfile文件。例如，AFNetworking的Podfile配置如下（参见AFNetworking的github主页）：

```
platform :ios, '7.0'
pod "AFNetworking", "~> 2.0"
```

Step4. 使用 `pod install` 命令安装配置的pods，例如：

```
$ pod install
Analyzing dependencies
...
```

如果 `pod install` 卡在 Analyzing dependencies 半天没有响应，是因为CocoaPods会默认更新一次仓库索引，可以使用 `pod install --no-repo-update` 命令禁止索引更新操作。

如果安装成功，工程根目录下会生成两个名为 `Podfile.lock` 和 `.xcworkspace` 的文件，以及一个名为 `Pods` 的目录。你工程所依赖的第三方库源码都会在Pods这个新的工程里。
```
$ ls -al
total 16
drwxr-xr-x   9 jyx  staff  306  2  8 13:24 .
drwx------+ 15 jyx  staff  510  2  8 13:01 ..
drwxr-xr-x  10 jyx  staff  340  2  8 13:01 JYXCocoaPodsDemo
drwxr-xr-x   5 jyx  staff  170  2  8 13:01 JYXCocoaPodsDemo.xcodeproj
drwxr-xr-x   3 jyx  staff  102  2  8 13:24 JYXCocoaPodsDemo.xcworkspace
drwxr-xr-x   4 jyx  staff  136  2  8 13:01 JYXCocoaPodsDemoTests
-rw-r--r--   1 jyx  staff   51  2  8 13:20 Podfile
-rw-r--r--   1 jyx  staff  888  2  8 13:24 Podfile.lock
drwxr-xr-x   8 jyx  staff  272  2  8 13:24 Pods
```
Step5. Xcode打开 `.xcworkspace` 工程文件，如果一切配置正确，应该可以直接Build并运行。工程目录如下图：

![工程目录.png](http://upload-images.jianshu.io/upload_images/77521-a362becc299e0254.png)

## 5. CocoaPods原理
...

## 6. 搭建CocoaPods私有仓库
...

## 参考资料
1. [CocoaPods安装和使用教程][1] by Code4App
2. [用CocoaPods做iOS程序的依赖管理][2] by [唐巧][22]
3. [CocoaPods最佳实践探讨][3] by [王_晓磊][20]
4. [极速化 CocoaPods][4] by [icyleaf][21]
5. [深入理解 CocoaPods][5] by [objc中国][23]

[1]: http://code4app.com/article/cocoapods-install-usage "CocoaPods安装和使用教程"
[2]: http://blog.devtang.com/blog/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/ "用CocoaPods做iOS程序的依赖管理"
[3]: http://weibo.com/p/1001603800875490492754 "CocoaPods最佳实践探讨"
[4]: http://icyleaf.com/2015/01/speed-up-cocoapods/ "极速化 CocoaPods"
[5]: http://objccn.io/issue-6-4/ "深入理解 CocoaPods"

[10]: https://rubygems.org/ "RubyGems"

[20]: http://weibo.com/xiaoleiwang "王_晓磊"
[21]: http://icyleaf.com/ "icyleaf"
[22]: http://blog.devtang.com/ "唐巧"
[23]: http://objccn.io/ "objc中国"