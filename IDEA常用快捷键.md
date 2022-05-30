# IDEA常用快捷键

1. 删除当前行, 默认是 ctrl + Y

2. 复制当前行, 默认ctrl + D

3. 补全代码 alt + /

4. 添加注释和取消注释 ctrl + / 【第一次是添加注释，第二次是取消注释】

5. 导入该行需要的类 先配置 auto import , 然后使用 alt+enter 即可

6. 快速格式化代码 ctrl + alt + L 7) 快速运行程序 自己定义 alt + R 

7. 生成构造器等 alt + insert [提高开发效率] 

8. 查看一个类的层级关系 ctrl + H [学习继承后，非常有用] 

9. 将光标放在一个方法上，输入 ctrl + B , 可以定位到方法 [学继承后，非常有用] 

10. 自动的分配变量名 , 通过在后面加 .var 

11. alt+7查看当前类的structure

12. ctrl+alt+t 把选中代码块用某些语句包围surround with

13. ctrl+j 查看所有模板

14. itit Collection迭代器，大写I 增强for循环

15. ctrl+alt+o 清楚无效import

16. 查找当前文件内容：ctrl+F  如上图片
    查找全局文件：ctrl+shift+F  或double shift（按两下）或ctrl+shift+N

    替换当前文件内容 ：ctrl+R  如上图片
    你想通过编辑器快速的将所有的’29’，变为29，你可以 ctrl + R, 搜索： \'(\d*)\', 替换为：$1
    

# 断点调试快捷键

F7 跳入方法内

F8 跳过，逐行执行代码

F9 resume执行到下一个断点

shift+F8 跳出方法

IDEA Debug默认显示的数据为简化的数据，需要在setting->Debugger->Data Views->Java中取消勾选Enable alternative view for Collection classes
