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
    用工厂的方法或者类来生成对象，不用再代码中直接new
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
### 注册树模式 
当很多地方用到一个类的时候，我们需要每次都new一下，我们可以用注册树模式将类注册到一个全局的静态变量里边，然后每次用的的时候直接从变量边拿
```php


class Register
{
   //用于储存实例
   protected static $objects;
   //将实例注册到注册树中
   public static function set($alias,$object)
   {
       self::$objects['$alias'] = $object
   }
   //获取注册树的实例
   public static function get($alias)
   {
      if(isset(self::$objects[$alias])){
          return self::$objects[$alias];
      }else{
          echo "实例而不存在";
      }
   }
   //销毁注册树的实例
   public static function __unset($alias)
   {
       unset(self::$objects[$alias]);
   }
} 
```

