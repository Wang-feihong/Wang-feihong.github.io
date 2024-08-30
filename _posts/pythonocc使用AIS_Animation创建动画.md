
**由于pythonocc官方案例中没有AIS_Animation的例子，想要使用该类做动画，一时间无从下手，借助ChatGPT走了一些弯路，逛了OCC论坛资料之后，现在终于可以使用了，提供一个demo，做个学习笔记。**

*下面是代码块：*
```py
# 创建一个box
box = BRepPrimAPI_MakeBox(10, 20, 30).Shape()  
# 初始化
display, start_display, add_menu, add_function_to_menu = init_display()  
Abox = display.DisplayShape(box, update=True)[0] 
context = AIS_InteractiveContext(display.Viewer)  
# 创建坐标系
ax1 = gp_Ax1(gp_Pnt(0, 0, 0), gp_Dir(0, 0, 1))  
angle1 = 45  
# 创建变换矩阵
trf1 = gp_Trsf() 
trf2 = gp_Trsf()  
trf2.SetRotation(ax1, angle1)  
# 创建AIS_Animation
name = TCollection_AsciiString("Animation1")  
animation = AIS_Animation(name) 
# 创建AIS_AnimationObject
box_ais = AIS_AnimationObject(name, context, Abox, trf1, trf2)  
# 设置动画时间
box_ais.SetOwnDuration(10)  
# 将box动画添加到AIS_Animation中
animation.Add(box_ais)  
# 获取动画的持续时间
duration = animation.Duration()  
# 启动动画计时器
animation.StartTimer(0, 1, True)  
while (not animation.IsStopped()):  
    animation.UpdateTimer()  
    context.UpdateCurrentViewer()  
# 开始显示动画
start_display()  
```

参考资料：
https://blog.csdn.net/loujiand/article/details/127955541
https://dev.opencascade.org/search/node/AIS_AnimationObject
