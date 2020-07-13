## flutter学习

### Dart语法

#### 变量

* `final`和`const`
  * `final`不能被修改 
  *  如果 `Const `变量是类级别的，需要标记为 `static const` 

#### 内建类型

- **Number**

  - `int`
  - `double`
  - 类型转换
    - `int.parse('')`  `double.parse('')`
    - `toString()` `toStringAsFixed()` 

  > 从 Dart 2.1 开始，必要的时候 int 字面量会自动转换成 double 类型 
  > 在算术表达式中，只要参与计算的因子是编译时常量， 那么算术表达式的结  果也是编译时常量 

- **String**

  -  Dart 字符串是一组`UTF-16`单元序列 
  - 多行字符串对象
    - `'''`或`"""`创建
  - 原始`raw`字符串
    - `r`前缀

  >  如果两个字符串包含了相同的编码序列，那么这两个字符串相等 
  >
  >  一个编译时常量的字面量字符串中，如果存在插值表达式，表达式内容也是编 译时常量， 那么该字符串依旧是编译时常量 

- **Boolean**

  - 类型检查

    - 必须明确进行值检查

      ```dart
      // 检查空字符串。
      var fullName = '';
      assert(fullName.isEmpty);
      
      // 检查 0 值。
      var hitPoints = 0;
      assert(hitPoints <= 0);
      
      // 检查 null 值。
      var unicorn;
      assert(unicorn == null);
      
      // 检查 NaN 。
      var iMeantToDoThis = 0 / 0;
      assert(iMeantToDoThis.isNaN);
      ```

- **List** (也被称为 *Array*)

- **Map**

  - 构造函数：`Map()`

  > 不是new Map()
  >
  > 在 Dart 2 中，`new` 关键字是可选的 

  - 查找`key`不包含时返回`null`

- **Set**

  - 方法

    - `add()` `addAll()`

  - `map`和`set`

    -  `{}` 默认是 `Map` 类型 

    - ```dart
      var names = <String>{};
      // Set<String> names = {}; // 这样也是可以的。
      // var names = {}; // 这样会创建一个 Map ，而不是 Set 。
      ```

- **Rune**

  -  表示字符串中的`UTF-32`编码字符
  -  表示`Unicode`编码的常用方法 
    - `\uXXXX`
    - `\u{X...}`(非四个数值)
  - `String`类属性获得`rune`数据
    -  属性 `codeUnitAt` 和 `codeUnit` 返回16位编码数据 
    -  属性 `runes` 获取字符串中的``Rune` 

- **Symbol**

  - 一个`Symbol`对象表示 `Dart` 程序中声明的运算符或者标识符

  > 代码压缩后会改变标识符的名称，但不会改变标识符的符号 
  >
  > 通过字面量 Symbol ，也就是标识符前面添加一个 `#` 号，来获取标识符的 Symbol 

> 在 Dart 所有的变量终究是一个对象（一个类的实例）， 所以变量可以使用 *构造涵数* 进行初始化 

#### 函数

* 可选参数

  >  required 类型参数在参数最前面， 随后是 optional 类型参数 
  
  * 命名可选参数 
  
    * ```dart
      enableFlags(bold: true, hidden: false); //调用
      void enableFlags({bool bold, bool hidden}) {...} //定义
      ```
      
    * `@required`注释
  
      ```da
      const Scrollbar({Key key, @required Widget child})
      ```
  
  * 位置可选参数
  
    * 将参数放到 `[]` 中
  
  * 默认参数值
  
    * `=`
  
* `main()`函数

  * 参数：可选的`List<String>`
  * 返回值：空

* 匿名函数

  *  有时候也被称为 *lambda* 或者 *closure*

  > 省的下次不认识这词`hhh`

* 返回值

  > 如果没有明确指定返回值， 函数体会被隐式的添加 `return null;` 语句 

#### 运算符

* 算术运算符

  * 取整：`~/`

* 关系运算符

  * `==`运算符

  > 在极少数情况下， 要确定两个对象是否完全相同，需要使用 [identical()](https://api.dartlang.org/stable/dart-core/identical.html) 函数 

* 类型判定运算符

  * `as`
    * 将对象强制转换为特定类型
  * `is`
  * `is!`

* 赋值运算符

  * `??=`运算符
    * 被赋值的变量为 null 时才会赋值

* 条件表达式

  * `expr1??expr2`
    *  如果`expr1`是`non-null`,返回`expr1`的值； 否则, 执行并返回`expr2`的值

* 级联运算符`(..)`

  *  在返回对象的函数中谨慎使用级联操作符，不能在`void`对象上创建级联操作

    ```dart
    var sb = StringBuffer();
    sb.write('foo')
      ..write('bar'); // Error: 'void' 没定义 'write' 函数
    ```
    
    > 严格的来讲， “两个点” 的级联语法不是一个运算符。 它只是一个 Dart 的特殊语法 

#### 控制流程

* `switch case`

  *  比较的对象必须都是同一个类的实例（并且不可以是子类）， 类必须没有对 `==` 重写 
  *  支持空 `case` 语句， 允许程序以`fall-through`的形式执行 

* `assert`

  > assert 语句只在开发环境中有效， 在生产环境是无效的； Flutter 中的 assert 只在 [debug 模式](https://flutter.io/debugging/#debug-mode-assertions) 中有效。 开发用的工具，例如 [dartdevc](https://webdev.dartlang.org/tools/dartdevc) 默认是开启 assert 功能。 其他的一些工具， 例如 [dart](https://www.dartcn.com/server/tools/dart-vm) 和 [dart2js,](https://webdev.dartlang.org/tools/dart2js) 支持通过命令行开启 assert ： `--enable-asserts` 

#### 异常

* `rethrow`关键字
* `finally`

#### 类

* 使用

  * 使用 `?.` 来代替 `.` ， 可以避免因为左边对象可能为 null ， 导致的异常 

  * 构造函数前的`new`可选

  * 常量

    * 构造两个相同的编译时常量会产生一个唯一的， 标准的实例：

      ```dart
      var a = const ImmutablePoint(1, 1);
      var b = const ImmutablePoint(1, 1);
      
      assert(identical(a, b)); // 它们是同一个实例。
      ```

    * 在 *常量上下文* 中， 构造函数或者字面量前的 `const` 可以省略

  * 获取对象类型：`runtimeType`属性

    * 运行时获取对象类型
    * 返回一个`Type`对象

* 声明实例变量

  >  所有实例变量都生成隐式 *getter* 方法。 非`final`的实例变量同样会生成隐式 *setter* 方法 

  >  如果在声明时进行了示例变量的初始化， 那么初始化值会在示例创建时赋值给变量， 该赋值过程在构造函数及其初始化列表执行**之前**

* 构造函数

  > 仅当存在命名冲突时，使用 `this` 关键字。 否则，按照 Dart 风格应该省略 `this` 

  * 默认构造函数

    > 默认构造函数没有参数并会调用父类的无参构造函数

  * 继承

    >  子类不会继承父类的构造函数。 子类不声明构造函数，那么它就只有默认构造函数 (匿名，没有参数) 

  * **命名构造函数**
  
    > 使用命名构造函数可为一个类实现多个构造函数， 也可以使用命名构造函数来更清晰的表明函数意图：
    >
    > ```dart
    > class Point {
    >   num x, y;
    > 
    >   Point(this.x, this.y);
    > 
    >   // 命名构造函数
    >   Point.origin() {
    >     x = 0;
    >     y = 0;
    >   }
    > }
    > ```
  
  * 调用顺序
  
    * 默认情况下，子类的构造函数会自动调用父类的默认构造函数（匿名，无参数） 
    * 执行顺序：
      1. `initializer list` （初始化参数列表）
      2. `superclass’s no-arg constructor` （父类的无名构造函数）
      3. `main class’s no-arg constructor` （主类的无名构造函数）
    * 如果父类中没有匿名无参的构造函数， 则需要手工调用父类的其他构造函数。 在当前构造函数冒号 (`:`) 之后，函数体之前，声明调用父类构造函数
  
  * **初始化列表**
  
  * 重定向构造函数
  
    * 函数体为空
  
    * ```dart
      class Point {
        num x, y;
      
        // 类的主构造函数。
        Point(this.x, this.y);
      
        // 指向主构造函数
        Point.alongXAxis(num x) : this(x, 0);
      }
      ```
  
  * 常量构造函数
  
  * 工厂构造函数
  
    * 当执行构造函数并不总是创建这个类的一个新实例 
    * `factory`关键字
  
* **抽象类**

  * `abstract`修饰符
  * 不能实例化
  
* **隐式接口**

  * `implements`关键字

* 继承

  * **重写**时建议加上`@override`

  > `!=`运算符为非可重载运算符（因为 `e1 != e2` 表达式仅仅是 `!(e1 == e2)` 的语法糖）
  >
  >  `noSuchMethod()`方法

* 枚举类

  * `enum`关键字
  * `index`
  * `values`常量

  >  可以在`switch`语句中使用枚举， 如果不处理所有枚举值，会收到警告

  * 限制
    * 枚举不能被子类化，混合或实现。
    * 枚举不能被显式实例化

* **`Mixin`**

  * `with`+类
  * 使用`mixin`替换`class`（不希望`Mixin`作为常规类使用）
  * 使用`on`指定可以使用`Mixin`的父类类型

* **`static`**

  > 静态变量只到它们被使用的时候才会初始化 
  >
  > 静态函数可以当做编译时常量使用 

  >  对于常见或广泛使用的工具和函数， 应该考虑使用顶级函数而不是静态方法

#### 泛型

* `<...>`

* 限制泛型类型
  * `extends`实现参数类型的限制

#### 库

* `import`
  * 参数：`URI`
    * 内置库：`dart:`方案
    * 其它库：系统文件路径或`package:`方案
* `library`
* `_`开头的标识符仅在库内可见

> 每个 Dart 应用程序都是一个库，虽然没有使用 `library` 指令 

* 指定库前缀

  ```dart
  import 'package:lib1/lib1.dart';
  import 'package:lib2/lib2.dart' as lib2;
  
  // 使用 lib1 中的 Element。
  Element element1 = Element();
  
  // 使用 lib2 中的 Element。
  lib2.Element element2 = lib2.Element();
  ```

* 导入部分

  ```dart
  // Import only foo.
  import 'package:lib1/lib1.dart' show foo;
  
  // Import all names EXCEPT foo.
  import 'package:lib2/lib2.dart' hide foo;
  ```

* 延迟加载(这里不太懂)

  * > 使用场景
    >
    > * 减少`APP`的启动时间
    > * 执行`A/B`测试，例如尝试各种算法的不同实现
    > * 加载很少使用的功能，例如可选的屏幕和对话框

  * > 要延迟加载一个库，需要先使用 `deferred as` 来导入：
    >
    > ```dart
    > import 'package:greetings/hello.dart' deferred as hello;
    > ```
    >
    > 当需要使用的时候，使用库标识符调用 `loadLibrary()` 函数来加载库：
    >
    > ```dart
    > Future greet() async {
    >   await hello.loadLibrary();
    >   hello.printGreeting();
    > }
    > ```

  * > - 延迟加载库的常量在导入的时候是不可用的。 只有当库加载完毕的时候，库中常量才可以使用
    > - 在导入文件的时候无法使用延迟库中的类型。 如果你需要使用类型，则考虑把接口类型移动到另外一个库中， 让两个库都分别导入这个接口库
    > - Dart 隐含的把 `loadLibrary()` 函数导入到使用 `deferred as 的命名空间` 中 `loadLibrary()` 方法返回一个`Future`

#### 异步

* 声明：`async`

  >  如果函数没有返回有效值， 需要设置其返回类型为 `Future` 

* 返回一个`Future`对象，仅在`await`表达式完成后才恢复执行

* 处理错误：使用`try,catch,finally`

* 处理`Stream`

  * 使用`async`和异步循环（`await for`）

    ```dart
    await for (varOrType identifier in expression) {
      // Executes each time the stream emits a value.
    }
    // 返回的值必须是 Stream 类型
    ```

    > 使用`break` 或者 `return`语句可以停止接收`stream`的数据， 这样就跳出了`for`循环， 并且从`stream`上取消注册

    ```dart
    Future main() async {
      // ...
      await for (var request in requestServer) {
        handleRequest(request);
      }
      // ...
    }
    ```

  * 使用`Stream API`

#### 生成器

* `sync*`+`yield`
* `async*`+`yield`
* 使用`yield*`提高递归性能

#### 注释

* 文档注释

  * `///`和`/**`

  > 在文档注释中，除非用中括号括起来，否则Dart 编译器会忽略所有文本
  > 使用中括号可以引用类、 方法、 字段、 顶级变量、 函数、 和参数
  > 括号中的符号会在已记录的程序元素的词法域中进行解析 

