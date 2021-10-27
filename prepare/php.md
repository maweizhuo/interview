
### [echo、print、print_r、var_dump 区别]
 > `echo`和`print`是语言结构，`print_r`和`var_dump`是普通函数`
 - echo: 输出一个或多个字符串
 - print: 输出字符串
 - print_r: 打印关于变量的易于理解的信息
 - var_dump: 打印关于变量的易于理解的信息(带类型)
###  [单引号和双引号的区别]
 双引号可以被分析器解析，单引号则不行
###  [isset 和 empty 的区别]
- isset: 检查变量是否已经设置并且非null
- empty: 判断变量是否为空，0/false也被认为空；变量不存在，不会产生警告
### [static、self、$this 的区别]
- static: static可以用于静态或非静态方法中，也可以访问类的静态属性，静态方法，变量和非静态方法，但不能访问非静态属性
- self: 可以用于访问类的静态属性，静态方法和常量，但self指向的是当前定义所在的类，这是self的限制
- $his: 指向的是实际调用时的对象，也就是说实际过程中谁调用了类的属性或方法，$this指向的就是那个对象。但$this不能访问类的静态熟悉和常量，且$this不能存在于静态方法中
### [include、require、include_once、require_once 的区别]
require 和 include 几乎完全一样，除了处理失败的方式不同之外。require 在出错时产生 E_COMPILE_ERROR 级别的错误。换句话说将导致脚本中止而 include 只产生警告（E_WARNING），脚本会继续运行
include_once 语句在脚本执行期间包含并运行指定文件。此行为和 include 语句类似，唯一区别是如果该文件中已经被包含过，则不会再次包含。如同此语句名字暗示的那样，只会包含一次
### [数组处理函数]
array_count_values 统计数组中所有的值
array_flip 交换数组的键和值
array_merge 合并一个或多个数组
array_multi_sort 对多个数组或多维数组进行排序
array_pad 以指定长度将一个值填充进数组
array_pop 弹出数组最后一个元素（出栈）
array_push 将一个或多个单元压入数组的末尾(入栈)
array_rand — 从数组中随机(伪随机)取出一个或多个单元
array_keys — 返回数组中部分的或所有的键名
array_values — 返回数组中所有的值
count — 计算数组中的单元数目，或对象中的属性个数
sort — 对数组排序
### [Cookie 和 Session]
Cookie：PHP 透明的支持 HTTP cookie 。cookie 是一种远程浏览器端存储数据并以此来跟踪和识别用户的机制
Session：会话机制(Session)在 PHP 中用于保持用户连续访问Web应用时的相关数据
### [传值和传引用的区别]
传值导致对象生成了一个拷贝，传引用则可以用两个变量指向同一个内容
### [502、504 错误产生原因及解决方式]
#### 502
502 表示网关错误，当 PHP-CGI 得到一个无效响应，网关就会输出这个错误
- `php.ini` 的 memory_limit 过小
- `php-fpm.conf` 中 max_children、max_requests 设置不合理
- `php-fpm.conf` 中 request_terminate_timeout、max_execution_time 设置不合理
- php-fpm 进程处理不过来，进程数不足、脚本存在性能问题
#### 504
504 表示网关超时，PHP-CGI 没有在指定时间响应请求，网关将输出这个错误
- Nginx+PHP 架构，可以调整 FastCGI 超时时间，fastcgi_connect_timeout、fastcgi_send_timeout、fastcgi_read_timeout
#### 500
php 代码问题，文件权限问题，资源问题
#### 503
超载或者停机维护
### [代码执行过程]
PHP 代码 => 启动 php 及 zend 引擎，加载注册拓展模块 => 对代码进行词法/语法分析 => 编译成opcode(opcache) => 执行 opcode
> PHP7 新增了抽象语法树(AST)，在语法分析阶段生成 AST，然后再生成 opcode 数组
### PHP 数组底层实现 （HashTable + Linked list）
PHP 数组底层依赖的散列表数据结构，定义如下（位于 Zend/zend_types.h）。
数据存储在一个散列表中，通过中间层来保存索引与实际存储在散列表中位置的映射。
由于哈希函数会存在哈希冲突的可能，因此对冲突的值采用链表来保存。
哈希表的查询效率是o（1），链表查询效率是o（n）；因此PHP数据索引速度很快；但是相对比较占用空间。
