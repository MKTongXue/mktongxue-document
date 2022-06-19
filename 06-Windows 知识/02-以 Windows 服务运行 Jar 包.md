# 1 以 Windows 服务运行 Jar 包

## 1.1 简要说明

（1）因为 Windows 系统经常自动重启更新，所以我们部署的 `.jar` 包，或者 `nacos` 服务，需要开机自启动。

（2）办法有很多，我们可以在网上查询实现。我这里以公司同事开发的软件 `应用程序以服务形式运行-安装程序.msi` 为示例，演示一下部署流程。

![软件截图](http://image.mktongxue.com/202206/015-01.png)

## 1.2 配置 Nacos 服务

（1）在 `Nacos` 安装目录，新建 `Nacos-WindowsServer.bat` 文件，内容如下
```text
cd C:\KaiHua\Nacos\bin
startup.cmd -m standalone
```
即：进入安装目录，单机模式启动 `Nacos` 服务

![Nacos 启动文件](http://image.mktongxue.com/202206/015-02.png)

## 1.3 配置 Jar 包

（1）在 `.jar` 包目录，新建 `RefuseHandling-WindowsServer.bat` 文件，内容如下
```text
cd C:\KaiHua\API
java -jar refuse-handling-0.0.1-SNAPSHOT.jar
```
即：进入 `.jar` 包所在目录，启动 `.jar` 包

![Jar 启动文件](http://image.mktongxue.com/202206/015-03.png)

## 1.4 应用程序以服务形式运行

（1）进入软件 `应用程序以服务形式运行-安装程序.msi` 解压目录，`InstallUtil.exe` 是系统安装 `Windows` 服务的可执行文件，`应用程序以服务形式运行.exe` 是安装的服务，`Config.xml` 是配置文件。

![解压目录](http://image.mktongxue.com/202206/015-05.png)

（2）`Config.xml` 是配置文件内容，有多个服务，可以配置多个 `<Execution></Execution>` 内容行
```text
<?xml version="1.0" encoding="utf-8" ?>
<Config>
  <!-- 注：当程序不支持无 Shell 运行时，请将记录日志和记录异常设为 false -->
  <Execution Name="MKNacos" ExecutablePath="C:\Windows\System32\cmd.exe" Arguments="/k C:\KaiHua\Nacos\bin\Nacos-WindowsServer.bat"
    SingleInstance="false" NeedProtect="true" LogNormal="false" LogError="false">
  </Execution>

  <Execution Name="MKJar" ExecutablePath="C:\Windows\System32\cmd.exe" Arguments="/k C:\KaiHua\API\RefuseHandling-WindowsServer.bat"
    SingleInstance="false" NeedProtect="true" LogNormal="false" LogError="false">
  </Execution>
</Config>
```

![配置文件内容](http://image.mktongxue.com/202206/015-06.png)

（3）安装 `Windows` 服务，以管理员身份运行 `cmd` 命令行
```text
// 进入目录
cd C:\KaiHua\WindowsServer
// 安装服务
InstallUtil.exe 应用程序以服务形式运行.exe

// 卸载服务
InstallUtil.exe -u 应用程序以服务形式运行.exe
```

![安装命令](http://image.mktongxue.com/202206/015-07.png)

（4）启动服务

![启动服务](http://image.mktongxue.com/202206/015-08.png)

（5）事件查看器，检查运行结果

![检查运行结果](http://image.mktongxue.com/202206/015-09.png)

（6）访问 `Nacos` 服务，或者 `.jar` 运行结果

![Nacos 启动成功](http://image.mktongxue.com/202206/015-10.png)

（7）重启电脑，相关服务正常启动！！！


# 2 结束
