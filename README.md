# helloreact
 Beginner
 react　学习
# require
### 1.核心模块
Node中有一些模块是编译成二进制的。这些模块在本文档的其他地方有更详细的描述。　　

核心模块定义在node源代码的lib/目录下。　　

require()总是会优先加载核心模块。例如，require('http')总是返回编译好的HTTP模块，而不管是否有这个名字的文件。　　


### 2.文件模块
如果按文件名没有查找到，那么node会添加 .js和 .json后缀名，再尝试加载，如果还是没有找到，最后会加上.node的后缀名再次尝试加载。　　

.js 会被解析为Javascript纯文本文件，.json 会被解析为JSON格式的纯文本文件. .node 则会被解析为编译后的插件模块，由dlopen进行加载。　　

模块以'/'为前缀，则表示绝对路径。例如，require('/home/marco/foo.js') ，加载的是/home/marco/foo.js这个文件。　　

模块以'./'为前缀，则路径是相对于调用require()的文件。 也就是说，circle.js必须和foo.js在同一目录下，require('./circle')才能找到。　　

当没有以'/'或者'./'来指向一个文件时，这个模块要么是"核心模块"，要么就是从node_modules文件夹加载的。　　

如果指定的路径不存在，require()会抛出一个code属性为'MODULE_NOT_FOUND'的错误。

### 3.从node_modules文件夹中加载
 如果require()中的模块名不是一个本地模块，也没有以'/', '../', 或是 './'开头，那么node会从当前模块的父目录开始，尝试在它的/node_modules文件夹里加载相应模块。　　
 
 如果没有找到，那么就再向上移动到父目录，直到到达顶层目录位置。  
 
例如，如果位于'/home/ry/projects/foo.js'的文件调用了require('bar.js')，那么node查找的位置依次为：  

* /home/ry/projects/node_modules/bar.js
* /home/ry/node_modules/bar.js
* /home/node_modules/bar.js
* /node_modules/bar.js  

这就要求程序员应尽量把依赖放在就近的位置，以防崩溃。

### 4.Folders as Modules
可以把程序和库放到一个单独的文件夹里，并提供单一入口来指向它。有三种方法，使一个文件夹可以作为require()的参数来加载。  

首先是在文件夹的根目录创建一个叫做package.json的文件，它需要指定一个main模块。下面是一个package.json文件的示例。  

***
`{ "name" : "some-library",
  "main" : "./lib/some-library.js" }`  
  
***  
  示例中这个文件，如果是放在./some-library目录下面，那么require('./some-library')就将会去加载./some-library/lib/some-library.js。  
  
  如果目录里没有package.json这个文件，那么node就会尝试去加载这个路径下的index.js或者index.node。例如，若上面例子中，没有package.json，那么require('./some-library')就将尝试加载下面的文件：  
  
  
* ./some-library/index.js
* ./some-library/index.node
#### 来至：http://nodeapi.ucdok.com/api/globals.html#globals_require_1910
