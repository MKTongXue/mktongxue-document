# 1 Windows 服务

## 1.1 安装

（1）在 C 盘下创建文件夹 `WindowsService`，然后在 `WindowsService` 文件夹内新建服务名文件夹，如 `KaiHua-WindowsService`

（2）将 `C:\Windows\Microsoft.NET\Framework\v4.0.30319` 文件夹内 `InstallUtil.exe` 复制到 `C:\WindowsService` 文件夹内

![WindowsService 文件夹](http://image.mktongxue.com/202206/008.png)

## 1.2 发布

（1）生成 `Windows` 服务，在解决方案内选中 `Windows Service` 项目，鼠标右键后生成，将 `bin` 目录复制到 `C:\WindowsService\KaiHua-WindowsService` 文件夹内

![选中项目](http://image.mktongxue.com/202206/009.png)

![获取 bin 文件夹](http://image.mktongxue.com/202206/010.png)

![复制 bin 文件夹](http://image.mktongxue.com/202206/011.png)

（2）
```text
// 以管理员身份打开命令行，并进入 WindowsService 文件夹
cd C:\WindowsService

// 安装 Windows 服务
InstallUtil.exe C:\WindowsService\KaiHua-WindowsService\bin\Debug\WindowsServiceRealMis.exe
```

（3）安装完成后，到 Windows 系统**服务**里，启动 `KaiHuaSystem` 即可

![启动服务](http://image.mktongxue.com/202206/012.png)

![Windows 服务名及描述来源](http://image.mktongxue.com/202206/013.png)

## 1.3 卸载

（1）
```text
// 卸载 Windows 服务
InstallUtil.exe -u C:\WindowsService\KaiHua-WindowsService\bin\Debug\WindowsServiceRealMis.exe
```

## 1.4 可能存在的问题

（1）如果启动服务出现异常
```text
// 注意 Windows 服务项目里 App.config 文件配置问题（.NETFramework 版本问题）
<startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0" />
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />
</startup>
```

（2）
```text
ProjectInstaller.cs 文件里 serviceProcessInstallerOne
Account 选择 NetworkService
```

（3）
```text
windows 服务启动不了 1053 错误
将 NT AUTHORITY\NetworkService 用户添加到 Administrator 组
服务器管理 - 工具 - 计算机管理 - 本地用户和组 - 组 - Administrators - 添加 - 高级 - 立即查找
```

（4）Windows 服务安装失败，可能是权限不足，以管理员身份启动命令行

## 1.5 参考文档

* [C# 之添加 window 服务(定时任务)](https://www.cnblogs.com/Vincent-yuan/p/10859129.html)

# 2 结束
