# JS+DOM学习记录

#####  浏览器执行JS

- 渲染引擎/内核：用来解析HTML和CSS
- JS引擎：用来读取JS代码并运行

##### JS的组成

- ECMAScript
- DOM——文档对象模型
- BOM——浏览器对象模型

##### JS书写位置

- 行内：直接写在元素的标签内部
- 内嵌：写在.html文档内，用双标签<script>标签包起来
- 外部：写在.js文件里，用双标签<script>引入

##### JS的作用域和变量

- 概念
  - 一个名字的可用性的代码范围就是这个名字的作用域 
  - 作用域的使用提高了代码的逻辑性，减少命名冲突
- 作用域的分类
  - 全局作用域
    - 整个script标签
    - 一个.js文件

  - 局部作用域（又称函数作用域）
    - 函数内部

  - ES6之前没有块级作用域

- 变量的分类
  - 全局变量：在全局作用域下的变量
  - 局部变量：在局部作用域下的变量

- 作用域链
  - 根据内部函数可以访问外部函数的变量的机制，用**链式查找**的方式决定外部函数中的哪些变量可以被内部函数访问，就称为作用域链


##### 预解析

- JS 引擎在运行代码时分为两步：预解析和代码执行 
- 预解析：JS引擎会把.js里面所有的var和function提升到当前作用域的最前面
  - 变量提升：把所有的变量**声明**提升到当前作用域的最前面，**不提升赋值操作**
  - 函数提升：把所有的函数**声明**提升到当前作用域的最前面，**不调用函数**
- 代码执行：按照代码书写的顺序从上往下执行

##### 对象

- 概念：对象是一组无序的相关**属性和方法的集合**

- 创建和调用

  - 使用**字面量**创建对象

    - 用花括号{}，var obj = {键:值,};
    - 里面的属性或方法采用**键值对**的形式，中间用逗号隔开
    - 方法的冒号后面跟的是一个**匿名函数**

  - 使用new Object创建对象

    - var 对象名 = new Object(); 创建一个空对象
    - 追加属性：对象名.属性名 = 属性值
    - 追加方法：对象名.方法名 = function(形参){//方法体}

  - 构造函数创建对象

    - 构造函数就是把对象里面一些**相同的属性名和方法**抽象出来封装到函数里面

    - 语法格式：

      - ```javascript
        function 构造函数名(属性值的形参){
            this.属性名=属性值的形参;
            this.方法名=function(形参){
                //方法体
            }
        }
        ```

        

      - 构造函数名的首字母要大写

    - 调用构造函数创建对象：

      - ```javascript
        var 对象名 = new 构造函数名(属性值实参);
        ```

    - 构造函数不需要return就可以返回结果

    - new关键字执行过程

      - new一个空对象
      - 构造函数中的this指向刚才创建的新对象
      - 执行构造函数中的代码，给新对象添加属性和方法
      - 返回这个新对象

  - 调用对象

    - 调用对象的属性：**对象名.属性名**或**对象名['属性名']**
    - 调用对象的方法：**对象名.方法名()**，不要忘记添加小括号

##### 内置对象

- 概念：内置对象就是JS语言自带的一些对象，供开发者使用

- 常用的内置对象——建议查询MDN文档

  - Math对象，不是构造器

  - Date对象，是一个构造函数，必须new来调用

    - 格式化日期——建议查文档
    - 时间戳——1970年1月1日
      - H5中可以用Date.now()获取时间戳
      - 时间戳可以用于制作倒计时效果——把毫秒数转换成时分秒

  - Array对象，是一个构造函数

    - 创建数组

      - 用字面量创建
      - 用new Array()创建，里面填一个数字表示长度为多少的空数组

    - 检测是否为数组

      - 用 **待检测对象 instanceof Array**，返回bool
      - H5新增的方法：用 **Array.isArray(待检测对象)**，返回bool

    - 添加或删除数组中的元素

      - 添加
        - .push(待添加的元素)，在末尾添加元素，返回值是数组的**长度**，**原数组会发生变化**
        - .unshift(待添加的元素)，在前面添加元素，返回值是数组的**长度**，**原数组会发生变化**
      - 删除
        - .pop()，没有参数，删除**数组的最后一个元素**，返回值是**被删除的元素**，**原数组会发生变化**
        - .shift()，没有参数，删除**数组的第一个元素**，返回值是**被删除的元素**，**原数组会发生变化**

    - 数组排序

      - .reverse()，翻转数组

      - .sort()，数组排序（！有坑），如果要升序/降序则需要在里面插一个匿名函数，具体查文档

        ```javascript
        arr1.sort(function(a,b){
            return a-b;//升序
            return b-a;//降序
        });
        ```

    - 获取数组的索引号

      - .IndexOf(元素)，返回值是数组元素的索引号，只返回第一个满足条件的索引号，如果没有返回-1
      - .lastIndexOf(元素)，从后往前找

    - 数组转换成字符串

      - .toString()
      - join('分隔符')

    - 数组的其他操作——查文档吧

      - .concat()，连接两个或多个数组，不影响原数组
      - .slice()，数组截取
      - .spice()，连续删除元素

  - String对象

    - 是值类型（C#的String是引用类型，不要弄混了
      - **重新赋值的本质是开辟一个新地址存放**
      - 原有地址存放的值不会变
      - 大量对字符串重新赋值和拼接会造成**内存垃圾**
    - 查找某个字符的位置
      - .IndexOf(待查找字符, 起始位置)
      - .lastIndexOf(待查找字符, 末尾位置)
    - 根据位置返回字符
      - .charAt(index)，返回值是指定位置处的字符
      - .charCodeAt(index)，返回值是指定位置处字符的ASCII码
      - H5新增[index]，返回值是指定位置处的字符
    - 拼接和截断——查文档吧
      - .concat(str1, str2, str3...)，用+拼接更简单 
      - .substr(start, length)
      - .slice(start, end)
      - .substring(start, end)
    - 替换字符
      - .replace('被替换的字符', '替换的字符')，只会替换符合条件的第一个，可以利用while循环和IndexOf查找来实现全部替换
    - 把字符串转换为数组
      - .split('分隔符')
    - 大小写转换
      - .toUpperCase()
      - .toLowerCase()

##### 数据类型——和C#差不多

- 值类型：数据储存在栈中

  - string, number, boolean, undefined, null
  - 特殊：null是一个空object
- 引用类型：在栈中储存堆的**地址**，**在堆中存放数据**

  - Object, Array, Date
  - 需要通过关键字new来创建对象
  - 每次new一个新对象就会在堆中开辟新空间用于存放数据


##### DOM——文档对象模型

- 基本概念
  - 处理可扩展标记语言（HTML或XML）的标准编程**接口**
  - 通过这些接口可以改变网页的内容、结构和样式
- DOM树
  - 文档：一个页面就是一个文档
  - 元素：页面里面所有的标签都是元素，element
  - 节点：网页中所有的内容（标签/属性/文本/注释）
  - DOM把以上内容都看作是对象
- 获取元素的接口
  - 根据ID获取：document.getElemetById()，返回一个匹配到ID的element对象，没有则返回null
  - 根据标签名获取：
    - document.getElementsByTagName()，返回带有指定标签名的所有对象的**集合**，以**伪数组**的形式存储，得到的元素对象是动态的
    - element.getElementsByTagName()，获取某个**父元素**内部所有指定标签名的子元素，element是父元素，且必须是单个对象
  - 根据类名和选择器选择对象（H5新增）：
    - document.getElementsByClassName('类名')，根据类名返回元素对象集合
    - document.querySelecter('选择器')，根据指定选择器返回**第一个**元素对象
    - document.querySelectorAll('选择器')，根据指定选择器返回元素对象集合
- 获取body元素和html元素
  - 获取body元素：document.body
  - 获取html元素：document.documentElement
- 自定义属性
  - H5规定**自定义属性要以data-开头**
  - 获取/设置/删除属性的接口——主要用于自定义属性
    - element.getAttribute('属性')
    - element.dataset.属性名/element.dataset['属性名']，这是H5新增的方法
    - element.setAttribute('属性')
    - element.removeAttribute('属性')

- 修改元素内容：使用element.innerHTML和element.innerText接口
- 修改表单属性——典型的应用是密码的显示和隐藏（text和password的切换）
- 修改样式属性：
  - element.style： **行内样式操作**，权重比较高
  - element.className：**类名样式操作**，先把要修改的样式包裹在class里写在CSS中，再把class添加给要修改样式的元素
- 文档对象的innerHTML/innerText/outerHTML属性的区别
  - innerHTML：对象的标签内部包含的所有内容，包括其他的html标签，**保留空格和换行**
  - innerText：对象的标签内部包含的所有内容，不包括其他的html标签（仅文本），**去除空格和换行**
  - outerText：对象的标签内部包含的所有内容+对象的标签本身
- DOM事件与Event对象
  - 联系：当触发DOM中的某个事件时，会创建一个Event对象/事件对象
  - AnimationEvent
  - DragEvent
  - FocusEvent
  - InputEvent
  - KeyboardEvent
  - WheelEvent
- **DOM节点操作（*重点）**——主要操作**元素节点**
  - 节点的概念
    - nodeType：元素节点为1，属性节点为2，文本节点为3
    - nodeName：节点名称
    - nodeValue：节点的值
  - 父节点
    - node.parentNode，返回最近的父节点（亲爹）
  - 子节点
    - node.childNodes，返回子节点的集合（包含所有类型的节点），但是不提倡使用
    - **node.children（非标准）**，是一个只读属性，返回所有的子**元素节点**，推荐使用
    - node.firstChild，返回第一个子节点（包含所有类型的节点），不提倡使用
    - node.lastChild，返回最后一个子节点（包含所有类型的节点），不提倡使用
    - node.firstElementChild，返回第一个子元素节点，相当于node.children[0]
    - node.lastElementChild，返回最后一个子元素节点
  - 兄弟节点
    - node.nextSibling
    - node.previousSibling
    - node.nextElementSibing
    - node.previousElementSibling
- **创建+添加节点**
  - document.createElement('标签名')
  - node.appendChild(child)，node是父节点，append是**追加**元素
  - node.insertBefore(child, 指定元素)，把child插到指定元素之前
  - create和append配合使用才能在文档中创建节点
- **删除节点**
  - node.removeChild(child)，删除一个子节点

- **复制节点**
  - node.cloneNode()，node是被克隆的节点
  - node要和append配合使用
  - **若参数为空或者false，则是浅拷贝**，只复制节点本身，不复制里面的子节点（内容）
  - **若参数为true，则是深拷贝**，会复制节点本身以及里面的所有子节点

##### 事件

- 概述：事件是可以被JS侦测到的行为，可以理解为“触发——响应”机制。 
- 事件三要素
  - 事件源：事件被触发的对象，如button
  - 事件类型：如何触发事件，如onclick
  - 事件处理程序：通过一个匿名函数赋值的方式完成
- 执行事件的步骤
  - 获取事件源
  - 注册事件，如div.onclick
  - 添加事件处理程序，给上面一步赋值
- 注册/绑定事件的两种方式
  - 传统方式：以on开头的事件
    - 注册的事件有唯一性
    - 即同一个元素同一个事件只能注册一个处理函数，后面注册的函数会覆盖前面注册的函数
  - 方法监听方式：addEventListener()
    - 同一个元素同一个事件可以注册多个监听器，即function
    - eventTarget.addEventListner(eventType, listener[, useCapture])
      - type：事件类型字符串，不用带on
      - listener：事件处理函数，function
      - useCapture：可选参数，bool值默认为false表示冒泡阶段，true表示捕获阶段
  - 方法监听方式：attachEvent（H5之前）
- 删除事件（解绑）的方式
  - 传统方式：事件类型直接赋值为null，如div.onclick=null;
  - 方法监听方式：eventTarget.removeEventListener(eventType, listener)


##### DOM事件流

- 概念
  - 描述从页面中接收事件的**顺序**
  - 事件发生时会在元素节点之间按照特定顺序传播，这个传播过程即为事件流
- 阶段：捕获阶段/目标阶段/冒泡阶段
  - **JS只能执行捕获和冒泡其中一个阶段**
  - 只有addEventListener才能有捕获阶段（要设置useCapture参数为true）
  - 传统方式只能处于冒泡阶段
  - 有些事件没有冒泡：blur、focus、mouseenter、mouseleave

##### 事件对象

- 特点
  - **写在监听函数的小括号里**，当形参来看
  - 对象有了事件才会存在事件对象，**不需要传实参**
  - 事件对象是事件的一系列相关数据的集合
  - 事件对象可以自己命名，一般用e-开头
- 属性
  - target：返回**触发**该事件的对象，即谁注册了（而this返回**绑定**了该事件的对象）
  - type：返回事件类型
- 方法
  - eventTarget.preventDefault()：阻止默认事件，如链接跳转和表单提交
  - eventTarget.stopPropgation()：阻止事件冒泡

##### 事件委托——最大的好处是节约代码

- 原理：不给每个子节点设置事件监听器，而是设置在父结点上，然后**利用冒泡原理影响每一个子节点**

##### 常用键盘事件——建议查文档

- keydown——不区分字母大小写
- keypress——不能识别功能键，区分字母大小写
- keyup——不区分字母大小写
- 键盘事件对象的属性
  - key
  - keycode（ASCII码值）
