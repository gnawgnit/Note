# Linux系统中添加桌面图标

源代码编译完成后，将可执行程序复制到PATH中，或者创建一个软链接在PATH中。这样就可以在bash中使用该程序，而不用到绝对路径下去执行该程序。还有就是在桌面添加图标。

在\~/桌面/目录下添加xxx.desktop文件，填写相关配置信息，保存即可。以Typora.desktop为例：

```desktop
[Desktop Entry]
Version=0.9.93(beta)
Name=Typora
Exec=~/root/soft/Typora/Typora
Icon=~/root/soft/Typora/assert/app/icon/icon.xpm
Terminal=false
Type=Application
Categories=Development
```

重要的是下面3个属性：

- Exec=软件程序路径
- Icon=软件图标
- Name=图标名称

更详细的属性如下：

- [Desktop Entry] 文件头
- Encoding=UTF-8 编码方式
- Name 应用名称
- Name[en]=en_name Name[en_US]=US_name 根据当前系统语言匹配显示名称
- Comment=comment 鼠标经过上面时的提示名称，也可国际化
- Exec=command 菜单执行的命令或程序
- Icon=iconpath 图标
- Terminal=false 是否使用终端
- Type=Application 分类
- X-MB-SingleInstance=true 是否选择单一实例
- Hidden=false 菜单是否隐藏
- Categories=Application;Network; 菜单所属类别

