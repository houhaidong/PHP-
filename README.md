# PHP-
PHP设计模式
### 单例模式
```php
 class SingleInstance{
    //先定义一个私有的静态方法 用来存放实例
    private static $instance;
    
    //定义一个私有的构造函数，防止外部new,只能有一个实例
    private function __construct(){
    
    }
    //定义一个私有的克隆函数，防止外部克隆实例
    private function __clone(){
    
    }
    //定义一个共有的静态方法，提供给外部实例
    public static function getInstance(){
      if(!self::$instance instanceof self){
            self::$instance = new self();
      }
      return self::$instance
    }
    
    public function getName(){
      //CODE ...
    }
 
 }
 $instance = $SingleInstance::getInstance();
 $instance->getName();
```
