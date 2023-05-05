### Kun Validator 表单验证

1. #### 可以这样使用

   ```php
   use Kun\Validator;
   
   //校验规则
   $rule = [
       'name'  => 'require|max:25',
       'age'   => 'number|between:1,120',
       'email' => 'email',
   ];
   //自定义内容（可以不填写，已做基础处理）
   $msg = [
       'name.require' => '名称必须',
       'name.max'     => '名称最多不能超过25个字符',
       'age.number'   => '年龄必须是数字',
       'age.between'  => '年龄只能在1-120之间',
       'email'        => '邮箱格式错误',
   ];
   //待校验参数
   $data = [
       'name'  => 'thinkphp',
       'age'   => 10,
       'email' => 'thinkphp@qq.com',
   ];
   
   $validate = Validator::make($rule, $msg);
   if (!validate->check ($data)) {
         throw new Exception($validate->getError());
     }
   ```





### 本验证类 从thinkphp5.0 中 采摘而来，后续如果不满足，可自行 修改增加方法，切记一定要验证

#### 文档地址:[内置规则 · ThinkPHP5.0完全开发手册 · 看云 (kancloud.cn)](https://www.kancloud.cn/manual/thinkphp5/129356)





### 格式验证类(用的时候测试一下哈，有一部分没测试)

> ### require

验证某个字段必须，例如：

```php
'name'=>'require'
```

> ### number 或者 integer

验证某个字段的值是否为数字（采用`filter_var`验证），例如：

```php
'num'=>'number'
```

> ### float

验证某个字段的值是否为浮点数字（采用`filter_var`验证），例如：

```php
'num'=>'float'
```

> ### boolean

验证某个字段的值是否为布尔值（采用`filter_var`验证），例如：

```php
'num'=>'boolean'
```

> ### email

验证某个字段的值是否为email地址（采用`filter_var`验证），例如：

```php
'email'=>'email'
```

> ### array

验证某个字段的值是否为数组，例如：

```php
'info'=>'array'
```

> ### accepted

验证某个字段是否为为 yes, on, 或是 1。这在确认"服务条款"是否同意时很有用，例如：

```php
'accept'=>'accepted'
```

> ### date

验证值是否为有效的日期，例如：

```php
'date'=>'date'
```

会对日期值进行`strtotime`后进行判断。

> ### alpha

验证某个字段的值是否为字母，例如：

```php
'name'=>'alpha'
```

> ### alphaNum

验证某个字段的值是否为字母和数字，例如：

```php
'name'=>'alphaNum'
```

> ### alphaDash

验证某个字段的值是否为字母和数字，下划线`_`及破折号`-`，例如：

```php
'name'=>'alphaDash'
```

> ### chs

验证某个字段的值只能是汉字，例如：

```php
'name'=>'chs'
```

> ### chsAlpha

验证某个字段的值只能是汉字、字母，例如：

```php
'name'=>'chsAlpha'
```

> ### chsAlphaNum

验证某个字段的值只能是汉字、字母和数字，例如：

```php
'name'=>'chsAlphaNum'
```

> ### chsDash

验证某个字段的值只能是汉字、字母、数字和下划线_及破折号-，例如：

```php
'name'=>'chsDash'
```

> ### activeUrl

验证某个字段的值是否为有效的域名或者IP，例如：

```php
'host'=>'activeUrl'
```

> ### url

验证某个字段的值是否为有效的URL地址（采用`filter_var`验证），例如：

```php
'url'=>'url'
```

> ### ip

验证某个字段的值是否为有效的IP地址（采用`filter_var`验证），例如：

```php
'ip'=>'ip'
```

支持验证ipv4和ipv6格式的IP地址。

> ### dateFormat:format

验证某个字段的值是否为指定格式的日期，例如：

```php
'create_time'=>'dateFormat:y-m-d'
```

## 长度和区间验证类

> ### in

验证某个字段的值是否在某个范围，例如：

```php
'num'=>'in:1,2,3'
```

> ### notIn

验证某个字段的值不在某个范围，例如：

```php
'num'=>'notIn:1,2,3'
```

> ### between

验证某个字段的值是否在某个区间，例如：

```php
'num'=>'between:1,10'
```

> ### notBetween

验证某个字段的值不在某个范围，例如：

```php
'num'=>'notBetween:1,10'
```

> ### length:num1,num2

验证某个字段的值的长度是否在某个范围，例如：

```php
'name'=>'length:4,25'
```

或者指定长度

```php
'name'=>'length:4'
```

> 如果验证的数据是数组，则判断数组的长度。 如果验证的数据是File对象，则判断文件的大小。

> ### max:number

验证某个字段的值的最大长度，例如：

```php
'name'=>'max:25'
```

> 如果验证的数据是数组，则判断数组的长度。 如果验证的数据是File对象，则判断文件的大小。

> ### min:number

验证某个字段的值的最小长度，例如：

```php
'name'=>'min:5'
```

> 如果验证的数据是数组，则判断数组的长度。 如果验证的数据是File对象，则判断文件的大小。

> ### after:日期

验证某个字段的值是否在某个日期之后，例如：

```php
'begin_time' => 'after:2016-3-18',
```

> ### before:日期

验证某个字段的值是否在某个日期之前，例如：

```php
'end_time'   => 'before:2016-10-01',
```

> ### expire:开始时间,结束时间

验证当前操作（注意不是某个值）是否在某个有效日期之内，例如：

```php
'expire_time'   => 'expire:2016-2-1,2016-10-01',
```

> ### allowIp:allow1,allow2,...

验证当前请求的IP是否在某个范围，例如：

```php
'name'   => 'allowIp:114.45.4.55',
```

该规则可以用于某个后台的访问权限

> ### denyIp:allow1,allow2,...

验证当前请求的IP是否禁止访问，例如：

```php
'name'   => 'denyIp:114.45.4.55',
```

## 字段比较类

> ### confirm

验证某个字段是否和另外一个字段的值一致，例如：

```php
'repassword'=>'require|confirm:password'
```

`5.0.4+`版本开始，增加了字段自动匹配验证规则，如password和password_confirm是自动相互验证的，只需要使用

```php
'password'=>'require|confirm'
```

会自动验证和password_confirm进行字段比较是否一致，反之亦然。

> ### different

验证某个字段是否和另外一个字段的值不一致，例如：

```php
'name'=>'require|different:account'
```

> ### eq 或者 = 或者 same

验证是否等于某个值，例如：

```php
'score'=>'eq:100'
'num'=>'=:100'
'num'=>'same:100'
```

> ### egt 或者 >=

验证是否大于等于某个值，例如：

```php
'score'=>'egt:60'
'num'=>'>=:100'
```

> ### gt 或者 >

验证是否大于某个值，例如：

```php
'score'=>'gt:60'
'num'=>'>:100'
```

> ### elt 或者 <=

验证是否小于等于某个值，例如：

```php
'score'=>'elt:100'
'num'=>'<=:100'
```

> ### lt 或者 <

验证是否小于某个值，例如：

```php
'score'=>'lt:100'
'num'=>'<:100'
```

> ### 验证字段比较支持对比其他字段

验证对比其他字段大小（数值大小对比），例如：

```php
'price'=>'lt:market_price'
'price'=>'<:market_price'
```

## filter验证

支持使用filter_var进行验证，例如：

```php
'ip'=>'filter:validate_ip'
```

## 正则验证

支持直接使用正则验证，例如：

```php
'zip'=>'\d{6}',
// 或者
'zip'=>'regex:\d{6}',
```

如果你的正则表达式中包含有`|`符号的话，必须使用数组方式定义。

```php
'accepted'=>['regex'=>'/^(yes|on|1)$/i'],
```

也可以实现预定义正则表达式后直接调用，例如在验证器类中定义`regex`属性

```php
protected $regex = [ 'zip' => '\d{6}'];
```

然后就可以使用

```php
'zip' =>  'regex:zip',
```



## 上传验证

> ### file

验证是否是一个上传文件

> ### image:width,height,type

验证是否是一个图像文件，width height和type都是可选，width和height必须同时定义。

> ### fileExt:允许的文件后缀

验证上传文件后缀

> ### fileMime:允许的文件类型

验证上传文件类型

> ### fileSize:允许的文件字节大小

验证上传文件大小



## 其它验证

> ### requireIf:field,value

验证某个字段的值等于某个值的时候必须，例如：

```php
// 当account的值等于1的时候 password必须
'password'=>'requireIf:account,1'
```

> ### requireWith:field

验证某个字段有值的时候必须，例如：

```php
// 当account有值的时候password字段必须
'password'=>'requireWith:account'
```