### 安装brew
##### 打开终端直接输入下面指令回车:
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```
注意：如果当前的用户是管理员，需要对权限进行许可，在执行上面的指令前先执行：sudo chmod -R g+w /usr/local
##### 常用的三条语句搜索(search)、更新(install)、卸载(remove)

搜索：brew search SoftwareName

更新：brew install SoftwareName

卸载：brew remove SoftwareName

### 安装grafana
Mac下需要首先安装brew这个包管理工具，在安装grafana就方便多了
```
brew update
brew install grafana
```

上面的命令用来安装grafana的最新稳定版本。
如果需要升级grafana，则可以通过下面的命令实现。

```
brew update
brew reinstall grafana
```

出现如下提示，则说明安装完成

```
To have launchd start grafana now and restart at login:
  brew services start grafana
Or, if you don't want/need a background service you can just run:
grafana-server --config=/usr/local/etc/grafana/grafana.ini --homepath /usr/local/share/grafana cfg:default.paths.logs=/usr/local/var/log/grafana cfg:default.paths.data=/usr/local/var/lib/grafana cfg:default.paths.plugins=/usr/local/var/lib/grafana/plugins
```

### 启停命令
通过下面命令可以后台启动/停止grafana,默认端口3000

```
// start
brew services start grafana
// stop
brew services stop grafana
```

grafana的默认端口是3000，用户名和密码为 admin admin
