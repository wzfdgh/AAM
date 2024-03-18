***

# 配置文件
* 没有配置文件时工具使用默认配置,存在配置文件时,配置文件会自动加载
* 以下是工具的默认配置信息,也是工具的所有可配置项,您可以在工具目录下的`config.ini`中进行自由配置,
```ini
[#Config]
PRINTLOGFLAG = True # 打印log开关
USEMODULE = False # 使用模块
NOTLOADEXTLIST = 'exmaple1', # 模块排除列表,格式 'exmaple1','exmaple2' + ,

# NetConfig
HTTPPROXY = '' # Http代理
HTTPSPROXY = 'http://10.0.0.1:7890' # Https代理
ALLPROXY = '' # 全部代理
USEBGMAPI = True # 使用BgmApi
USETMDBAPI = True #使用TMDBApi

# File处理Config
USELINK = True # 使用硬链接开关
LINKFAILSUSEMOVEFLAGS = False #硬链接失败时使用MOVE
RMLOGSFLAG = False # 日志文件超时删除,填数字代表删除多久前的

# FileName处理Config
JELLYFINFORMAT = False # jellyfin 使用 ISO/639 标准 简体和繁体都使用chi做标识
USETITLTOEP = False # 给每个番剧视频加上番剧Title 

# QBConfig
USERQBAPI = True # 使用QBApi
QBIP = '192.168.1.112' # QB的ip
QBPORT = 8081 # QBApi端口
QBUSERNAME = 'admin' # Qb账号
QBPASSWORD = 'Syn123456!' # Qb密码

# 附加Config
TIMELAPSE = 0 # 延时处理番剧
SEEPSINGLECHARACTER =False # SE EP单字符模式

[#模块名称1]
模块参数key = value...... 

[#模块名称2]
模块参数key = value...... 
```
* `config.ini.Template`是配置文件的模板,内容如上

## 配置介绍
* 类似`[#Config]`这样的标志是用来区别各类程序使用的配置项目
> * `[#Config]`是主程序的配置项目
> * `[#模块名称]`是模块使用的配置项目，如`[#example]`就是模块`example`的配置

* 如果您想在配置文件中屏蔽一条配置项,在前面添上 `#` 即可
  ```ini
  #PRINTLOGFLAG = True
  ```

* `HTTPPROXY` `HTTPSPROXY` `ALLPROXY` 配置项是用来给您配置代理相关信息的,请按自己情况的来填

* `USELINK` 配置项是 `使用硬链接` 来整理番剧的开关,如果您需要保种请设置为 `True` [什么是硬链接？](https://zh.wikipedia.org/zh-cn/%E7%A1%AC%E9%93%BE%E6%8E%A5)

* `LINKFAILSUSEMOVEFLAGS`配置项,功能是硬链接失败时使用 Move 来整理番剧,部分文件系统不支持硬链接请注意(如 `exFat` )

* `RMLOGSFLAG` 配置项是用来控制工具删除保存天数达到和超过 `RMLOGSFLAG` 的值的配置,默认为 7 天,如果您不想删除请设置为 `False`
