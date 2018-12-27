### PHP代码解析
一个PHP代码解析的小工具，主要实现了全局函数、类、接口、类内方法等的解析，解析内容目前包括结构体的起止行号和结构体内的无效代码行数。以便用于单元测试代码覆盖度统计。

核心实现方法是利用PHP提供的 token_get_all() 函数，获取PHP代码的解析结果，根据token值去判断相应的内容。
实现过程中利用到了状态机的设计模式，所以有额外的两个文件依赖，需要单独使用该工具的同学可以自行剥离使用。

[核心源码文件](https://github.com/pureisle/MicroMVC/blob/master/Framework/Libraries/PHPFunctionParser.php)
#### 相关文件
```
|- Framework	框架
	|- Libraries	框架类库
	|- PHPFunctionParser.php  核心解析类
	|- FiniteStateMachine.php 状态机控制类
	|- FiniteState.php  状态基类
```

### 使用方法
```
$source_string = file_get_contents($file_path);
$ps = new  PHPFunctionParser($source_string);
$ret = $ps->parse();
var_dump($ret);
```

### 输出结果如下
```
array(2) {
  ["current_namespace"]=>
  string(19) "Framework\Libraries"
  ["classes"]=>
  array(1) {
    ["Framework\Libraries\Debug"]=>
    array(3) {
      ["begin_line"]=>
      int(12)
      ["methods"]=>
      array(6) {
        ["debugDump($data, $type = 'DEBUG')"]=>
        array(3) {
          ["begin_line"]=>
          int(22)
          ["end_line"]=>
          int(40)
          ["invalid_line_count"]=>
          int(0)
        }
        ["getDebug()"]=>
        array(3) {
          ["begin_line"]=>
          int(45)
          ["end_line"]=>
          int(47)
          ["invalid_line_count"]=>
          int(0)
        }
        ["setDebug($debug)"]=>
        array(3) {
          ["begin_line"]=>
          int(51)
          ["end_line"]=>
          int(57)
          ["invalid_line_count"]=>
          int(0)
        }
        ["setErrorMessage($error_code, $error_msg)"]=>
        array(3) {
          ["begin_line"]=>
          int(61)
          ["end_line"]=>
          int(68)
          ["invalid_line_count"]=>
          int(0)
        }
        ["getErrorMessage()"]=>
        array(3) {
          ["begin_line"]=>
          int(72)
          ["end_line"]=>
          int(74)
          ["invalid_line_count"]=>
          int(0)
        }
        ["echoErrorMessage($error_message, $is_exit = true)"]=>
        array(3) {
          ["begin_line"]=>
          int(78)
          ["end_line"]=>
          int(81)
          ["invalid_line_count"]=>
          int(0)
        }
      }
      ["end_line"]=>
      int(82)
    }
  }
}
```
