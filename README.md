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

### 工厂模式
```php
//声明一个接口类
interface db{
   public function db();
}
class mysql implements db(){
   public function db(){
       ehco "链接mysql成功";
   }
}
class oracel implements db(){
   public function db(){
       echo "链接oracel成功";
 }
 
 class dbFactory{
    public static function conn($db){
        switch($db){
           case "mysql":
               rerurn new mysql();
           break;
           case "oracel":
               return new oracel();
           break;
           defaule:
               return new mysql();
           break;
        }
    }
 }
 $a = dbFactory::conn("mysql");
 $a->db();
 
 
 
 
}



```
