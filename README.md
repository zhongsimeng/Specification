#前端规范

#isobar 前端代码规范及最佳实践

###概述
本文档包含了Isobar公司的创意技术部（前端工程）开发web应用的规范。

编写本文档的主要驱动力是两方面： 1) 代码一致性 以及 2) 最佳实践。 通过保持代码风格和传统的一致性，我们可以减少遗留系统维护的负担，并降低未来系统崩溃的风险。而通过遵照最佳实践，我们能确保优化的页面加载、性能以及可维护的代码。

##总体指导原则
###前端开发核心思想

1. 表现、内容和行为分离
2. 标记应该是结构良好、语义正确以及普遍合法
3. JavaScript应该起到渐进式增强用户体验的作用

###总体原则
####缩进
对于所有编程语言，我们要求缩进必须是软tab（用空格字符）。在你的文笔编辑器里敲Tab应该等于4个空格。

####可读性vs压缩
对于维护现有文件，我们认为可读性比节省文件大小更重要。大量空白和适当的ASCII艺术都是受鼓励的。任何开发者都不必故意去压缩HTML或CSS，也不必把JavaScript代码最小化得面目全非。

我们会在服务器端或build过程中自动最小化并gzip压缩所有的静态客户端文件，例如css和JS。

##标记
任何网页的首要组件就是基于标签的HTML标记语言。超文本标记语言（HTML）曾有一段不堪的历史，近几年已回转。经过对它基于XML的XHTML变种的漫长试验之后，整个行业终于接受了HTML代表web的未来这一事实。

标记定义了文档的结构和纲要，并提供结构化的内容。除了最基本的概念（例如标题、段落和列表）之外，标记并不是用来定义页面上内容的外观和体验的。HTML的表现属性都已经被废弃了，有关样式的定义都应该被包含在样式表中。

###HTML5
HTML5是HTML和XHTML的新版本。在HTML5草案的规范中定义了可以用HTML和XML编写的单一的语言，意在解决在之前HTML的迭代中发现的一些问题并满足web应用的需求，这是以前HTML没有充分覆盖到的领域。

在何时的时候，我们会使用HTML5 Doctype 和 HTML5特性。

我们会对照W3C校验器测试我们的标记，以确保标记是结构良好的。我们的目标并不是100%的合法代码，但是校验肯定对呀编写可维护的站点以及调试代码都大有帮助。Isobar公司不保证代码都是100%合法，而是确信跨浏览器体验会相当一致。

###模板
对HTML5文件，我们使用H5BP针对我们自己项目需求修改的一个分支。

###Doctype
标记中必须总是使用合适的Doctype来指示浏览器触发标准模式，永远要避免Quirks模式。

HTML5特别好的一个方面就是它简化了Doctype需要的代码。无意义的属性被弃用了，Doctype声明也被显著地简化了。另外，也无需再用CDATA对内联JavaScript代码进行转义，而这在此之前为了让XHTML符合XML的严密性是必需的。

HTML5 Doctype

    <DOCTYPE html>
    
###字符编码
所有标记必须通过UTF-8编码传递，因为这种编码方式是对国际化最友好的。必须在HTTP的header和HTML文档的head部分都指定这种编码。

设定字符编码是通过`<meta>`标签进行。

    <meta http-equiv="Content-Type" content="test/html; charset=UTF-8" />

如果是HTML5，则只需要写：

    <meta charset="utf-8">

###标记的总体原则
下面是编写HTML标记的总体原则。提醒大家一点，在创建的HTML文档里总是要使用能够代表内容语义的标记。

* 段落分隔符要使用实际对应的`<p>`元素，而不是多个`<br>`标签。
* 在合适的条件下，充分利用`<dl>`(定义列表)和`<blockquote>`标签。
* 列表中的条目必须总是放置于`<ul>`、`<ol>`、`<dl>`中，永远不要用一组`<div>`和`<p>`来表示。
* 给每个表单里的字段加上`<label>`标签，其中的`for`属性必须和对应的输入字段对应，这样用户就可以点击标签。同理，给标签加上`cursor:pointer;`样式也是明智的做法。
* 不用使用输入字段中的`size`属性。该属性是和输入字段里文本的`font-size`相关的。应该使用CSS宽度。
* 在某些闭合的`</div>`标签旁边加上一段html注释，说明这里闭合的是什么元素。这在有大量嵌套和缩进的情况下会很有用。
* 不要把表格用于页面布局。
* 在合适的条件下，利用`microformats`和`/`或者`Microdata`，具体说是`hCard`和`adr`。
* 在合适的条件下，利用`<thead>`、`<tbody>`、`<th>`标签（以及`Scope`属性）。

具备恰当语法结构(THEAD,TBODY,TH[scope])的Table标记

    <table summary="This is a chart of year-end returns for 2005.">
      <thead>
        <tr>
          <th scope="col">Table header 1</th>
          <th scope="col">Table header 2</th>
        </tr>
      <thead>
      <tbody>
        <tr>
          <td>Table data 1></td>
          <td>Table data 2</td>
        </tr>
      </tbody>
    </table>
    
* 对于页眉和标题，永远使用首字母大写格式。不要在标记中使用全部大写或小写的标题，而是应用CSS属性`text-transform:uppercase/lowercase`。

###属性加引号
在HTML规范里并没有严格要求属性值两边加引号。但考虑到一些属性可以接受空白值，为了保持一致性，我们要求所有属性值必须加上引号。

##CSS
网页的第二个组件就是在层叠样式表(css)中包含的表现信息。Web浏览器成功实现css后，整整一代web开发者对他们的网站的外观和体验拥有了全部的控制权。

正如网页信息在语义方面由HTML标记描述，css从表现方面则是通过对视觉属性的定义来描述网页。css的强大之处在于，这些属性可以混合并通过各种标示符匹配，它可以通过样式规则的分层（“层叠”）来控制页面的布局和视觉特征。

###编码总体原则

* 从外部文件加载css，尽可能减少文件数。加载标签必须放在文件HEAD部分。
* 用LINK标签加载，永远不要用@import。

        //加载样式表
        <link rel="stylesheet" type="text/css" herf="myStylesheet.css" />

        //不要用内联式样式
        <p style="font-size: 12px; color: #FFFFFF">This is poor form, I say</p>
        
* 不要在文件中用内联式引入的样式，不管它是定义在样式标签里还是直接定义在元素上。这样会很难追踪样式规则。
* 使用normalize.css让渲染效果在不同浏览器中更一致。
* 使用类似YUI fonts.css的字体规格化文件。
* 定义样式的时候，对样式的页面只出现一侧的元素用id，其他用class。
* 理解层叠和选择器的明确度，这样你就可以写出非常简洁且高效的代码。
* 编写性能优化的选择器。尽可能避免使用开销大的css选择器。例如，避免`*`通配符选择器，也不要叠加限定条件到ID选择器（例如`div#myid`）或class选择器（例如`table.results`上。这对于速度至上并包含了成千上万个DOM元素的web应用来说尤为重要）。更多相关内容请参阅MDN上的这篇《编写高效css》。

###CSS盒子模型
深入学习和理解css及基于浏览器的盒子模型，对于掌握css布局的基础是非常必要的。

###CSS校验
我们一般不用w3c校验器。

###CSS格式
最低要求：选择器单独占一行，每个属性占一行。属性声明要有缩进。

作为提高的要求，关联或孩子样式要增加2-4个空格的缩进。这样有利于分层查看和组织，产生（对于某些人来说）可读性更好的样式表。

另外，在给一个样式指定多个选择器的时候，把每个选择器单独放一行是个好主意。这样可以避免一行变得太长，也能提高可读性及版本控制流程。

    .post-list li a{
        color:#A8A8A8;
    }
        .post-list li a:hover{
            color:#000;
            text-decoration:none;
        }
        .post-list li .author a,
        .post-list li .author a:hover{
            color:#F30;
            text-transform:uppercase;
        }
        
在多个开发者协作环境下，避免用单行css格式，因为这样会给版本控制带来问题。

###字母排序
