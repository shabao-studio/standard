# 规范文档
沙包工作室项目管理相关规范

## 版本号规范
参照 [语义化版本号(semver)](http://semver.org/lang/zh-CN/)

这里在semver的基础上, 针对包含硬件的项目, 扩充版本号的语义.

硬件项目中 硬件的衍生项目如固件/外壳设计的版本号跟随硬件的`主版本号.次版本号` 

例如: 当固件增加功能而硬件未变更时无需递增版本号 而硬件的`主版本号.次版本号`递增时 固件即使无修改 也需进行版本号迭代(即增加空的更新日志并打上tag)

### 主版本号
硬件与其他部分之间的接口改变, 例如: 

* 与PC端的通讯接口改变导致与之前版本不兼容
* 主要物理接口定义改变(不包含功能无关的接口,如调试口定义/测试点定义)导致不兼容

### 次版本号
硬件变更影响其功能性/与硬件衍生项目先前版本不兼容时递增次版本号, 例如: 

* 增加感光元件(即使无需修改外壳设计 因为这里发生了功能性变更)
* 按钮位置变更(需要修改外壳设计 与之前的硬件衍生项目"外壳设计"发生不兼容)

### 修订号
这里未扩充修订号的语义, 即"必须在只做了向下兼容的修正时递增".

硬件变更未影响其功能性时仅递增修订版本, 包含而不仅限于以下情况: 

* 更换不合适的元件
* 修正焊盘尺寸
* 修正走线(如改善高频特性等)

### 先行版本号
硬件不使用先行版本号

### 版本编译信息
硬件产品中版本编译信息对应生产批次编号 该编号从`00`开始迭代 相同主版本号下 每生产新的一批硬件时递增此编号 用两位数字表示 如`v4.0.0`的第3次生产批次写作:
```
v4.0.0+02
```

## 源代码管理
使用git作为版本管理工具

私有项目使用[码云作为托管平台](https://git.oschina.net/organizations/shabao-studio)

开源项目使用[Github作为托管平台](https://github.com/shabao-studio/)

### 版本库命名

```
项目名-版本库文件内容
```

#### 项目名 
由小写字母/数字/下划线构成,如`osu_keyobard_v3`

#### 版本库文件内容
如版本库中的文件为项目`osu_keyobard_v3`的固件,版本库命名为 `osu_keyobard_v3-fw`

```
对照表
固件 - fw
文档 - doc
PC端程序 - pc
说明书 - um
参考手册 - rm
数据手册 - ds
```

### tag,release功能的使用

tag在关键点添加, 如pcb打样/正式生产/固件发布时, 添加tag时需在更新日志中编写变更项目. 

release在对外发布时使用, 项目的各个部分需分别执行release操作. 

以上操作必须携带`先行版本号`, 软件在release操作时必须携带`版本编译信息`.

### 更新日志规范

更新日志在

参照 [如何维护更新日志](http://keepachangelog.com/zh-CN/0.3.0/)

## 文档规范
将文档等同于源代码进行管理, 必要时可使用 [Read The Docs](http://docs.readthedocs.io) 生成html或pdf.

### 使用Markdown的场合
简单的文档, 如维护记录, 更新日志等.

### 使用reStructuredText
较复杂文档,如规范手册/库参考手册等使用rst格式书写文档.

