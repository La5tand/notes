# QT

## delegate

- comboxdelegate

 Qt 中视图与模型绑定时,模型必须用 new 来创建, 否则初始化时候,视图没有数据显示,或者后期视图不能随着模型的改变而改变.
 原因分析: 可能是局部变量的生命周期问题, new 创建的变量在堆空间中,不手动释放的话,会一直存在. 如果不 new 一个 model , 把 model 放在类的成员变量中, 视图也可以正常显示数据.(最后一条未验证)

 ```cpp
    
 ```

## QTableWidget 和 QTableView

- 区别
    QTableWidget 继承自 QTableView

- QTablewidget
    可以在ui文件中设置行和列
    1. 固定宽高
        > setFixdSize(width,height);
    2. 设置水平标题头自动缩进
        > horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);
    3. 设置垂直标题头自动缩进
        > verticalHeader()->setSectionResizeMode(QHeaderView::Stretch);
        >horizontalHeader() verticalHeader() 这两个方法得到的是QHeaderView 类型的对象,调用这个对象的 setSectionResizeMode() 方法
    4. 隐藏垂直标题头
        > verticalHeader()->hide() 实际上调用的是QHeaderView 的 hide() 方法
    5. 设置不可编辑
        > setEditTriggers(QAbstractItemView::NoEditTriggers);
    6. QTableWidget 继承自 QAbstractItemView
        > QAbstractItemView 的 setEditTriggers 方法可以设置是否可以编辑,只要继承自 QAbstractItemView 的其他控件都可以设置为是否可编辑,而且方法一致
    7. 设置每个单元格的文字居中显示
        > 通过 item(row,column) 得到单元格 QTableWidgetItem 的对象 再使用 QTableWidget 的 setTextAlignment(Qt::AlignHCenter|Qt::AlignVCenter) 方法
- QTableView
    设置行和列只能在 Model 中设置,我的理解是因为 QTableView 是个显示数据的 View,只有有数据才能生成行和列

- QPushbutton
    设置背景色,设置选中状态,划过状态的字体颜色

    ```cpp
    pushbutton->setStyleSheet("QPushButton{background-color:green}"
                              "QPushButton:checked{background-color:red}"
                              "QPushButton:hover{background-color:blue}");
    ```

## QDialog

- 窗口的模态和非模态
  - 使用 `exec()` 显示一个模式对话框,锁住程序直到用户关闭这个对话框为止,函数返回一个 DialogCode 结果,在对话框弹出期间，用户不可以切换同程序下的其它窗口，直到该对话框被关闭
  - 使用 `show()` 显示一个非模式对话框。控制权即刻返回给调用函数。弹出窗口是否模式对话框，取决于modal属性的值

## QWidget

- widget window 窗体主窗口关闭后,子窗口还存在
  先说结论 对子窗体设置一个属性 `setAttribute(Qt::WA_QuitOnClose,false);`
  每个 `Qt::Window` 类型的 widget 都有,默认都为 `true`