# Python爬虫XPath 的基本使用
## 简介
XPath 是一门在 XML 文档中查找信息的语言。XPath 可用来在 XML 文档中对元素和属性进行遍历。XPath 是 W3C XSLT 标准的主要元素，并且 XQuery 和 XPointer 都构建于 XPath 表达之上。
- XPath 使用路径表达式在 XML 文档中进行导航  
XPath 使用路径表达式来选取 XML 文档中的节点或者节点集。这些路径表达式和我们在常规的电脑文件系统中看到的表达式非常相似。
- XPath 包含一个标准函数库
- XPath 是 XSLT 中的主要元素
- XPath 是一个 W3C 标准
## XPath 节点
- 在 XPath 中，有七种类型的节点：元素、属性、文本、命名空间、处理指令、注释以及文档节点（或称为根节点）
- 基本值（或称原子值，Atomic value）
基本值是无父或无子的节点。
- 项目（Item）  
项目是基本值或者节点。

## XPath 语法
XPath 使用路径表达式来选取 XML 文档中的节点或节点集。节点是通过沿着路径 (path) 或者步 (steps) 来选取的。
选取节点
XPath 使用路径表达式在 XML 文档中选取节点。节点是通过沿着路径或者 step 来选取的。
下面列出了最有用的路径表达式：

|表达式|	描述|
|:---|:---|
|nodename|	选取此节点的所有子节点|
|/	|从根节点选取|
|//	|从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置|
|.	|选取当前节点|
|..	|选取当前节点的父节点|
|@	|选取属性|

谓语（Predicates）
谓语用来查找某个特定的节点或者包含某个指定的值的节点。
谓语被嵌在方括号中。

选取未知节点
XPath 通配符可用来选取未知的 XML 元素。

|通配符|	描述|
|:---|:---|
|*	|匹配任何元素节点。|
|@* |	匹配任何属性节点。|
|node()|	匹配任何类型的节点。|

XPath 轴
轴可定义相对于当前节点的节点集。

|轴名称	| 结果|
|:---|:---|
|ancestor	|选取当前节点的所有先辈（父、祖父等）。|
|ancestor-or-self|	选取当前节点的所有先辈（父、祖父等）以及当前节点本身。|
|attribute|	选取当前节点的所有属性。|
|child|	选取当前节点的所有子元素。|
|descendant|	选取当前节点的所有后代元素（子、孙等）。|
|descendant-or-self	|选取当前节点的所有后代元素（子、孙等）以及当前节点本身。|
|following|	选取文档中当前节点的结束标签之后的所有节点。|
|namespace|	选取当前节点的所有命名空间节点。|
|parent|	选取当前节点的父节点。|
|preceding|	选取文档中当前节点的开始标签之前的所有节点。|
|preceding-sibling|	选取当前节点之前的所有同级节点。|
|self|	选取当前节点。|

位置路径表达式
位置路径可以是绝对的，也可以是相对的。

绝对路径起始于正斜杠( / )，而相对路径不会这样。在两种情况中，位置路径均包括一个或多个步，每个步均被斜杠分割：

绝对位置路径：
/step/step/...
相对位置路径：
step/step/...
每个步均根据当前节点集之中的节点来进行计算。

步（step）包括：
轴（axis）
定义所选节点与当前节点之间的树关系
节点测试（node-test）
识别某个轴内部的节点
零个或者更多谓语（predicate）
更深入地提炼所选的节点集
步的语法：
轴名称::节点测试[谓语]
实例

|例子|结果|
|:---|:---|
|child::book	|选取所有属于当前节点的子元素的 book 节点。|
|attribute::lang|	选取当前节点的 lang 属性。 
|child::*	|选取当前节点的所有子元素。|
|attribute::* |	选取当前节点的所有属性。|
|child::text()	|选取当前节点的所有文本子节点。|
|child::node()	|选取当前节点的所有子节点。|
|descendant::book|	选取当前节点的所有 book 后代。|
|ancestor::book	|选择当前节点的所有 book 先辈。|
|ancestor-or-self::book|	选取当前节点的所有 book 先辈以及当前节点（如果此节点是 book 节点)|
|child::* /child::price	|选取当前节点的所有 price 孙节点。| 

XPath 运算符
下面列出了可用在 XPath 表达式中的运算符：

|运算符	| 描述	|实例|	返回值|
|:---|:---|:---|:---|
||	计算两个节点集	|//book | //cd	|返回所有拥有 book 和 cd 元素的节点集|
|+	|加法|	6 + 4	|10|
|-	|减法	|6 - 4	|2|
|*	|乘法|	6 * 4	|24|
|div	|除法|	8 div 4|	2|
|=|	等于|	price=9.80	|如果 price 是 9.80，则返回 true。如果 price 是 9.90，则返回 false。|

运算符	描述	实例	返回值
|	计算两个节点集	//book | //cd	返回所有拥有 book 和 cd 元素的节点集
+	加法	6 + 4	10
-	减法	6 - 4	2
*	乘法	6 * 4	24
div	除法	8 div 4	2
=	等于	price=9.80	
如果 price 是 9.80，则返回 true。

如果 price 是 9.90，则返回 false。

!=	不等于	price!=9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.80，则返回 false。

<	小于	price<9.80	
如果 price 是 9.00，则返回 true。

如果 price 是 9.90，则返回 false。

<=	小于或等于	price<=9.80	
如果 price 是 9.00，则返回 true。

如果 price 是 9.90，则返回 false。

>	大于	price>9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.80，则返回 false。

>=	大于或等于	price>=9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.70，则返回 false。

or	或	price=9.80 or price=9.70	
如果 price 是 9.80，则返回 true。

如果 price 是 9.50，则返回 false。

and	与	price>9.00 and price<9.90	
如果 price 是 9.80，则返回 true。

如果 price 是 8.50，则返回 false。

mod	计算除法的余数!=	不等于	price!=9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.80，则返回 false。

<	小于	price<9.80	
如果 price 是 9.00，则返回 true。

如果 price 是 9.90，则返回 false。

<=	小于或等于	price<=9.80	
如果 price 是 9.00，则返回 true。

如果 price 是 9.90，则返回 false。

>	大于	price>9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.80，则返回 false。

>=	大于或等于	price>=9.80	
如果 price 是 9.90，则返回 true。

如果 price 是 9.70，则返回 false。

or	或	price=9.80 or price=9.70	
如果 price 是 9.80，则返回 true。

如果 price 是 9.50，则返回 false。

and	与	price>9.00 and price<9.90	
如果 price 是 9.80，则返回 true。

如果 price 是 8.50，则返回 false。

mod	计算除法的余数	5 mod 2	1
