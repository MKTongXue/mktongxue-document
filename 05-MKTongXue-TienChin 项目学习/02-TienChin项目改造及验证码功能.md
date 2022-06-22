# 1 包含课程章节

* 《04.项目改造完善_TienChin》
* 《05.项目结构分析_TienChin》
* 《06.验证码响应结果分析_TienChin》
* 《07.验证码生成接口分析_TienChin》

# 2 修改项目 banner

（1）
```text
// 可以自定义项目 banner
https://bootschool.net/ascii
```

# 3 项目结构

（1）
* tienchin-common 公共工具类，依赖链最底层
* tienchin-farmework 配置类
* 业务模块
  - tienchin-system 系统管理
  - tienchin-generator 代码生成
  - tienchin-quartz 定时任务
* tienchin-ui 前端项目
* tienchin-admin 后端项目入口 

# 4 验证码功能

（1）
```text
// Base64 字符串转图片
https://tool.jisuapi.com/base642pic.html
```

（2）
```text
// Redis 数据库清空命令
flushdb
```

（3）验证码功能探究，更多详情请阅读代码！
```text
// 示例项目 kaptcha
D:\015-MyDocument\03-CodeMK\tienchin-example\kaptcha
```

# 5 结束
