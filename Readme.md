# 代码使用说明  Code instructions

Cpse核心文件位于./CpseCore/中，主文件夹中DemoGame.py是基于Cpse开发的一款示例游戏。详细介绍以及说明文档请查看CPSE2说明文档.pdf

The CPSE core file is located in ./CpseCore/ , DemoGame.py is a sample game developed based on CPSE. Please refer to CPSE2说明文档.pdf for detailed introduction and documentation

#### Cpse依赖模块：pynput、pywin32
#### CPSE dependent modules: pynput, pywin32


# 更新计划
## 近期更新计划
#### 1.用C#重写渲染逻辑，加快运行效率
#### 2.增加物理引擎

## 目前待解决问题
#### 1.渲染逻辑低效
#### 2.文字渲染易错位


# 介绍

CPSE2是一款基于Python的Windows平台控制台画面渲染引擎，提供了丰富的游戏引擎功能，可以实现在Windows控制台高效率渲染画面以及开发游戏。

Cpse2 is a Python based console image rendering engine for Windows platform. It provides rich game engine functions and can achieve efficient rendering of images and game development on Windows console.

## 基本类

### CpseEngine

CpseEngine为CPSE2基本类，负责CPSE2的画面渲染，进行CPSE2的任何渲染操作均需要通过实例化后的CpseEngine进行操作，CpseEngine中亦包含许多实用方法为开发提供帮助。

| **Code**                 |   |
|--------------------------|---|
| Cpse.CpseEngine()        |   |
| **参数列表**             |   |
| None                     |   |
| **示例Code**             |   |
| cpse = Cpse.CpseEngine() |   |

### CpseFrame

CpseFrame为CPSE2基本类，负责CPSE2的画面组建，所有CPSE2所渲染出的画面均为一个CpseFrame，可通过调整实例化后的CpseFrame改变画面。CpseFrame中可添加CpseObject，在CpseFrame中可以组织调整 CpseObject，最后提供给CpseEngine进行渲染。

| **Code**                        |       |             |
|---------------------------------|-------|-------------|
| Cpse.CpseFrame(frameSize:tuple) |       |             |
| **参数列表**                    |       |             |
| frameSize                       | Tuple | Frame的宽高 |
| **Code**                        |       |             |
| frame = Cpse.CpseFrame((50,50)) |       |             |

### CpseObject

CpseObject为CPSE2基本类，作为CPSE2画面的基本组成部分。

| **Code**                                                       |       |                  |
|----------------------------------------------------------------|-------|------------------|
| Cpse.CpseObject(objList:list,anchorPoint:tuple)                |       |                  |
| **参数列表**                                                   |       |                  |
| objList                                                        | List  | Object的组成列表 |
| anchorPoint                                                    | Tuple | Object的锚点     |
| **Code**                                                       |       |                  |
| obj = Cpse.CpseObject([[0,0,0],[1,0,0],[0,1,0],[1,1,0]],(0,0)) |       |                  |

# 基本方法介绍

## CpseEngine

### CpseEngine.StartRenderingAndShowThread()

| **Code**                                                         |           |                                                |
|------------------------------------------------------------------|-----------|------------------------------------------------|
| CpseEngine.StartRenderingAndShowThread(frame,maxFPs,updata)      |           |                                                |
| **介绍**                                                         |           |                                                |
| 启动CpseEngine渲染Frame并Show的进程                              |           |                                                |
| **参数列表**                                                     |           |                                                |
| frame                                                            | CpseFrame | 被渲染的Frame                                  |
| maxFPs                                                           | int       | 最大渲染帧率；可空，默认100 Fps                |
| updata                                                           | function  | 更新函数，每渲染帧会执行一次；可空，默认无函数 |
| **Code**                                                         |           |                                                |
| cpse.StartRenderingAndShowThread(frame,maxFPs=120,updata=updata) |           |                                                |

### CpseEngine.ExitRenderingAndShowThread()

| **Code**                                |
|-----------------------------------------|
| CpseEngine.ExitRenderingAndShowThread() |
| **介绍**                                |
| 结束CpseEngine渲染Frame并Show的进程     |
| **Code**                                |
| cpse.ExitRenderingAndShowThread()       |

### CpseEngine.RenderingFrame()

| **Code**                                                                                                                                                                                                                                                                                                      |                                                         |               |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|---------------|
| CpseEngine.RenderingFrame(frame)                                                                                                                                                                                                                                                                              |                                                         |               |
| **介绍**                                                                                                                                                                                                                                                                                                      |                                                         |               |
| 渲染Frame，返回渲染完成后的CRObj对象，该对象为Frame的渲染结果。该方法仅渲染Frame，并不会显示到控制台，需使用CpseEngine.ShowCRObj才可以将CRObj显示到控制台。如非使用预渲染技术或自定义渲染过程，建议直接使用包含渲染和显示的[CpseEngine.StartRenderingAndShowThread()](#cpseenginestartrenderingandshowthread) |                                                         |               |
| **参数列表**                                                                                                                                                                                                                                                                                                  |                                                         |               |
| frame                                                                                                                                                                                                                                                                                                         | CpseFrame                                               | 被渲染的Frame |
| **返回值类型**                                                                                                                                                                                                                                                                                                |                                                         |               |
| CRObj                                                                                                                                                                                                                                                                                                         | 已完成渲染的Frame，可用CpseEngine.ShowCRObj显示到控制台 |               |
| **Code**                                                                                                                                                                                                                                                                                                      |                                                         |               |
| crobj = cpse.RenderingFrame(frame)                                                                                                                                                                                                                                                                            |                                                         |               |

### CpseEngine.ShowCRObj()

| **Code**                                                                                                                                                                                                                  |       |                                                             |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|-------------------------------------------------------------|
| CpseEngine.ShowCRObj(crobj)                                                                                                                                                                                               |       |                                                             |
| **介绍**                                                                                                                                                                                                                  |       |                                                             |
| 将已经完成渲染的Frame显示到控制台，该方法只会显示一帧，请配合循环使用。如非使用预渲染技术或自定义渲染过程，建议直接使用包含渲染和显示的[CpseEngine.StartRenderingAndShowThread()](#cpseenginestartrenderingandshowthread) |       |                                                             |
| **参数列表**                                                                                                                                                                                                              |       |                                                             |
| Crobj                                                                                                                                                                                                                     | CRObj | 已经渲染完成的Frame，可用CpseEngine.RenderingFrame渲染Frame |
| **Code**                                                                                                                                                                                                                  |       |                                                             |
| cpse.ShowCRObj(crobj)                                                                                                                                                                                                     |       |                                                             |

### CpseEngine.ObjectMoveKeyboardControlSet()

| **Code**                                                                 |            |                                                           |
|--------------------------------------------------------------------------|------------|-----------------------------------------------------------|
| CpseEngine.ObjectMoveKeyboardControlSet(cpseFrame,obj,buttonTuple,speed) |            |                                                           |
| **介绍**                                                                 |            |                                                           |
| 快速创建CpseObject键盘控制上下左右移动                                   |            |                                                           |
| **参数列表**                                                             |            |                                                           |
| cpseFrame                                                                | CpseFrame  | 被控制的CpseObject所在的Frame                             |
| obj                                                                      | CpseObject | 被控制的CpseObject                                        |
| buttonTuple                                                              | Tuple      | 上下左右四个方向的控制按键；可空，默认为("w","s","a","d") |
| speed                                                                    | int        | 移动速度；可空，默认为1                                   |
| **Code**                                                                 |            |                                                           |
| cpse.ObjectMoveKeyboardControlSet(frame,obj)                             |            |                                                           |

### CpseEngine.WaitRun()

| **Code**                          |          |              |
|-----------------------------------|----------|--------------|
| CpseEngine.WaitRun(time,function) |          |              |
| **介绍**                          |          |              |
| 等待时间后执行函数                |          |              |
| **参数列表**                      |          |              |
| time                              | float    | 等待的时间   |
| function                          | function | 被执行的函数 |
| **Code**                          |          |              |
| cpse.WaitRun(2,Run)               |          |              |

### CpseEngine.WaitRunRe()

| **Code**                            |          |              |
|-------------------------------------|----------|--------------|
| CpseEngine.WaitRunRe(time,function) |          |              |
| **介绍**                            |          |              |
| 每过去指定时间后运行函数            |          |              |
| **参数列表**                        |          |              |
| time                                | float    | 等待的时间   |
| function                            | function | 被执行的函数 |
| **Code**                            |          |              |
| cpse.WaitRunRe(2,Run)               |          |              |

### CpseEngine.GetKeyboardButtonDown()

| **Code**                                                                    |     |                                                                 |
|-----------------------------------------------------------------------------|-----|-----------------------------------------------------------------|
| CpseEngine.GetKeyboardButtonDown(key)                                       |     |                                                                 |
| **介绍**                                                                    |     |                                                                 |
| 获取按键是否按下                                                            |     |                                                                 |
| **参数列表**                                                                |     |                                                                 |
| Key                                                                         | Any | 被获取的按键，字母按键提供字母字符串，控制按键调用Cpse的key变量 |
| **Code**                                                                    |     |                                                                 |
| cpse.GetKeyboardButtonDown("j") cpse.GetKeyboardButtonDown(Cpse.key.ctrl_l) |     |                                                                 |

## CpseFrame

### CpseFrame.AddObject()

| **Code**                     |            |                    |
|------------------------------|------------|--------------------|
| CpseFrame.AddObject(obj,pos) |            |                    |
| **介绍**                     |            |                    |
| 用于往Frame中添加Object      |            |                    |
| **参数列表**                 |            |                    |
| obj                          | CpseObject | 被添加的CpseObject |
| pos                          | tuple      | obj在Frame中的位置 |
| **Code**                     |            |                    |
| frame.AddObject(obj,(0,1))   |            |                    |

### CpseFrame.DelObject()

| **Code**                            |            |                    |
|-------------------------------------|------------|--------------------|
| CpseFrame.AddObject(obj)            |            |                    |
| **介绍**                            |            |                    |
| 删除Frame中第一个同类型的CpseObject |            |                    |
| **参数列表**                        |            |                    |
| obj                                 | CpseObject | 被删除的CpseObject |
| **Code**                            |            |                    |
| frame.DelObject(obj)                |            |                    |

### CpseFrame.SetObjectPoint()

| **Code**                          |            |                    |
|-----------------------------------|------------|--------------------|
| CpseFrame.SetObjectPoint(obj,pos) |            |                    |
| **介绍**                          |            |                    |
| 设置Object在Frame中的位置         |            |                    |
| **参数列表**                      |            |                    |
| obj                               | CpseObject | 被设置的CpseObject |
| pos                               | tuple      | 设置点             |
| **Code**                          |            |                    |
| frame.SetObjectPoint(obj,(50,50)) |            |                    |

### CpseFrame.GetObjectPoint()

| **Code**                        |                    |                    |
|---------------------------------|--------------------|--------------------|
| CpseFrame.GetObjectPoint(obj)   |                    |                    |
| **介绍**                        |                    |                    |
| 获取Object在Frame中的位置       |                    |                    |
| **参数列表**                    |                    |                    |
| obj                             | CpseObject         | 被获取的CpseObject |
| **返回值类型**                  |                    |                    |
| tuple                           | CpseObject的所在点 |                    |
| **Code**                        |                    |                    |
| pos = frame.GetObjectPoint(obj) |                    |                    |

### CpseFrame.MoveObject()

| **Code**                                               |            |                                                                  |
|--------------------------------------------------------|------------|------------------------------------------------------------------|
| CpseFrame.MoveObject(obj,direction = "f",distance = 1) |            |                                                                  |
| **介绍**                                               |            |                                                                  |
| 移动Object                                             |            |                                                                  |
| **参数列表**                                           |            |                                                                  |
| obj                                                    | CpseObject | 被移动的CpseObject                                               |
| direction                                              | str        | 移动方向，提供str指定方向，默认为f（"f"前，"b"后，"u"上，"d"下） |
| distance                                               | int        | 移动距离，默认为1                                                |
| **Code**                                               |            |                                                                  |
| frame.MoveObject(obj)                                  |            |                                                                  |

### CpseFrame.SetObjectLifeCycle()

| **Code**                                         |            |                                        |
|--------------------------------------------------|------------|----------------------------------------|
| CpseFrame.SetObjectLifeCycle(obj,time,function)  |            |                                        |
| **介绍**                                         |            |                                        |
| 设置Object的生命周期，生命周期时间结束后会被销毁 |            |                                        |
| **参数列表**                                     |            |                                        |
| obj                                              | CpseObject | 被设置的CpseObject                     |
| time                                             | float      | 生命周期时间                           |
| function                                         | function   | 生命周期函数，生命周期结束后会执行一次 |
| **Code**                                         |            |                                        |
| frame.SetObjectLifeCycle(Obj,1)                  |            |                                        |

## CpseObject

### CpseObject.SetObjcetList()

| **Code**                       |      |              |
|--------------------------------|------|--------------|
| CpseObjct.SetObjectList(_list) |      |              |
| **介绍**                       |      |              |
| 设置Object的列表               |      |              |
| **参数列表**                   |      |              |
| \_list                         | list | 被设置的列表 |
| **Code**                       |      |              |
| obj.SetObjectList(_list)       |      |              |

### CpseObject.GetObjcetList()

| **Code**                     |                  |
|------------------------------|------------------|
| CpseObjct.GetObjectList()    |                  |
| **介绍**                     |                  |
| 获取Object的ObjectList       |                  |
| **返回值类型**               |                  |
| list                         | CpseObject的List |
| **Code**                     |                  |
| \_list = obj.GetObjectList() |                  |

### CpseObject.SetAnchorPoint()

| **Code**                              |       |              |
|---------------------------------------|-------|--------------|
| CpseObjct.SetAnchorPoint(anchorPoint) |       |              |
| **介绍**                              |       |              |
| 设置Object的锚点                      |       |              |
| **参数列表**                          |       |              |
| anchorPoint                           | tuple | 被设置的锚点 |
| **Code**                              |       |              |
| obj.SetAnchorPoint((1,1))             |       |              |

### CpseObject.GetAnchorPoint()

| **Code**                   |                  |
|----------------------------|------------------|
| CpseObjct.GetAnchorPoint() |                  |
| **介绍**                   |                  |
| 获取Object的锚点           |                  |
| **返回值类型**             |                  |
| tuple                      | CpseObject的锚点 |
| **Code**                   |                  |
| pos = obj.GetAnchorPoint() |                  |

### CpseObject.SetTag()

| **Code**              |     |        |
|-----------------------|-----|--------|
| CpseObjct.SetTag(tag) |     |        |
| **介绍**              |     |        |
| 设置Object的标签      |     |        |
| **参数列表**          |     |        |
| tag                   | str | 标签名 |
| **Code**              |     |        |
| obj.SetTag("Player")  |     |        |

### CpseObject.GetTag()

| **Code**           |                  |
|--------------------|------------------|
| CpseObjct.GetTag() |                  |
| **介绍**           |                  |
| 获取Object的标签   |                  |
| **返回值类型**     |                  |
| str                | CpseObject的标签 |
| **Code**           |                  |
| tag = obj.GetTag() |                  |

### CpseObject.SetKeyPoint()

| **Code**                          |       |            |
|-----------------------------------|-------|------------|
| CpseObjct.SetKeyPoint(posTag,pos) |       |            |
| **介绍**                          |       |            |
| 用于创建/更改Object的关键点       |       |            |
| **参数列表**                      |       |            |
| posTag                            | str   | 关键点标签 |
| pos                               | tuple | 关键点坐标 |
| **Code**                          |       |            |
| obj.SetKeyPoint("muzzle",(-1,-1)) |       |            |

### CpseObject.GetKeyPoint()

| **Code**                        |                        |            |
|---------------------------------|------------------------|------------|
| CpseObjct.GetKeyPoint(posTag)   |                        |            |
| **介绍**                        |                        |            |
| 获取Object的关键点              |                        |            |
| **参数列表**                    |                        |            |
| posTag                          | str                    | 关键点标签 |
| **返回值类型**                  |                        |            |
| tuple                           | CpseObject的关键点坐标 |            |
| **Code**                        |                        |            |
| pos = obj.GetKeyPoint("muzzle") |                        |            |

### CpseObject.AcceptCollisionStart()

| **Code**                                              |          |                                                                                                                 |
|-------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------|
| CpseObjct.AcceptCollisionStart(trigger)               |          |                                                                                                                 |
| **介绍**                                              |          |                                                                                                                 |
| 启用Object的碰撞检测，每帧若触发碰撞会触发trigger函数 |          |                                                                                                                 |
| **参数列表**                                          |          |                                                                                                                 |
| trigger                                               | function | 触发函数，该函数需要设置接受下述参数："target"，用于获取被碰撞对象的CpseObject；"selfObj"，用于碰撞体获取自身。 |
| **Code**                                              |          |                                                                                                                 |
| obj.AcceptCollisionStart(Trigger_Collision_Obj)       |          |                                                                                                                 |

### CpseObject.AcceptCollisionEnd()

| **Code**                       |
|--------------------------------|
| CpseObjct.AcceptCollisionEnd() |
| **介绍**                       |
| 关闭Object的碰撞检测           |
| **Code**                       |
| obj.AcceptCollisionEnd()       |

### CpseObject.CopyObject()

| **Code**                                     |                      |
|----------------------------------------------|----------------------|
| CpseObjct.GetKeyPoint(posTag)                |                      |
| **介绍**                                     |                      |
| 将该CpseObject复制，返回复制完成的CpseObject |                      |
| **返回值类型**                               |                      |
| CpseObject                                   | 复制完成的CpseObject |
| **Code**                                     |                      |
| tempObj = Obj.CopyObject()                   |                      |

### CpseObject.TextToObjectList()

| **Code**                                                                                       |                    |                                            |
|------------------------------------------------------------------------------------------------|--------------------|--------------------------------------------|
| CpseObjct.TextToObjectList(text,color = 0x07)                                                  |                    |                                            |
| **介绍**                                                                                       |                    |                                            |
| 静态方法。将Text转换为CpseObjectList，以此显示文字，暂不支持多行。部分半角符号会出现渲染错误。 |                    |                                            |
| **参数列表**                                                                                   |                    |                                            |
| posTag                                                                                         | str                | 被转换的文字                               |
| color                                                                                          | int                | 文字颜色，提供十六进制数，默认为黑色(0x07) |
| **返回值类型**                                                                                 |                    |                                            |
| list                                                                                           | 返回CpseObjectList |                                            |
| **Code**                                                                                       |                    |                                            |
| obj = CpseObject(CpseObject.TextToObjectList(f"您的得分：{score}"),(0,0))                      |                    |                                            |
