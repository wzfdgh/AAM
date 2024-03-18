***

# 前言
> * **`AAM`的基础功能是很薄弱的，各种内置配置也不能合每个人的胃口，所有才有了`模块功能`**
> * **为了方便大家更快的做出更好的模块，特此编写此须知**

# 原理
> * **模块功能的实现很简单，就和`Hook`一样，那里不好改哪里

![module](../assets/img/img01.jpg)

# 开始 
* 为了讲解，使用了 `Ext` 里的 `examaple.py`
```python
Versions = '0.1.0' # 版本号
Author = github/abcuders

def Auxiliary_RMSubtitlingTeam(File):
    if File[0] == '《':# 判断有无字幕组信息
        File = sub(r'《|》','',File,flags=I) 
    else:
        ItemName = findall(r'^=.*?=',File,flags=I)
        File = sub(r'^=.*?=','',File,flags=I)
        Auxiliary_Log(f'字幕组 >> {ItemName}')
    return File

def main(Globals,*ConfigDict):
    global sub,I,findall,Auxiliary_Log
    
    sub = Globals['sub']
    I = Globals['I']
    findall = Globals['findall']
    Auxiliary_Log = Globals['Auxiliary_Log']

    if ConfigDict != ():
        for ConfigName in ConfigDict[0]:
            ConfigValue = ConfigDict[0][ConfigName]
            Auxiliary_Log(f'配置 < {ConfigName} = {ConfigValue}','INFO')
            exec(f'global {ConfigName};{ConfigName} = {ConfigValue}')

    
    Globals['Auxiliary_RMSubtitlingTeam'] = Auxiliary_RMSubtitlingTeam
```

* **一个合格的模块，应该至少存在版本号-Versions和作者名称（带联系地址）-Author，更详细的请带上说明文档的地址-Docs**
* 我们简单看看，这个模块的功能是来截取番剧文件的字幕组信息的
* 所以我们截获了`Auxiliary_RMSubtitlingTeam`
```python
def Auxiliary_RMSubtitlingTeam(File):
    if File[0] == '《':# 判断有无字幕组信息
        File = sub(r'《|》','',File,flags=I) 
    else:
        ItemName = findall(r'^=.*?=',File,flags=I)
        File = sub(r'^=.*?=','',File,flags=I)
        Auxiliary_Log(f'字幕组 >> {ItemName}')
    return File
```
* `Auxiliary_RMSubtitlingTeam`中引用了`sub`,`I`,`findall`等主程序的data,故我们需要在`globals( )`中获取
* `main`是每个模块都必须拥有的，是模块的入口，必须规定`Globals,*ConfigDict`俩个参数，`*ConfigDict`可变参数是模块的配置项目接受参数

```python
def main(Globals,*ConfigDict):
    global sub,I,findall,Auxiliary_Log
    
    sub = Globals['sub']
    I = Globals['I']
    findall = Globals['findall']
    Auxiliary_Log = Globals['Auxiliary_Log']

    if ConfigDict != ():
        for ConfigName in ConfigDict[0]:
            ConfigValue = ConfigDict[0][ConfigName]
            Auxiliary_Log(f'配置 < {ConfigName} = {ConfigValue}','INFO')
            exec(f'global {ConfigName};{ConfigName} = {ConfigValue}')


    Globals['Auxiliary_RMSubtitlingTeam'] = Auxiliary_RMSubtitlingTeam
```

* 最后`Globals['XXX'] = XXX`是来实际替换效果函数的

# 模块的配置项目
* 参见 [配置文件](../config/config.md)