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
### 适配器模式

将一个类的接口转换成客户希望的另一个接口，使原本不兼容而不能在一起工作的类可以在一起工作

```php
interface db_driver
{
   function connect();
   function query();
}

//mysql数据库实现
class mysql implements db_driver
{
   public function connect()
   {
      /*具体实现代码*/
   }
   public function query()
   {
      /*具体实现代码*/
   }
}

//pdo数据库实现
class pdo implements db_driver
{
   public function connect()
   {
      /*具体实现代码*/
   }
   public function query()
   {
      /*具体实现代码*/
   }
 }
 //定义适配器类
 class db_adapter
 {
    private $db;
    public function __construct($db_obj)
    {
       $this->db = $db_obj;
    }
    
    function connect()
    {
      $this->db->connect();
    }
    function query($sql)
    {
      $this->query($sql)
    }
 }
  $db = new db_adapter(new mysql());

```

### 策略模式
使用场景：
    1、一个页面A进去要显示A的信息，B进去要显示B的信息，平时的写法就是用if  else 判断，但C要是进去，我们还得更改if else很麻烦，我们用了策略者模式后，就不用添加else了，直接添加一个策略就可以
    2、超市促销活动，原价，八折，满300减50，就可以用策略模式

```php
 interface StrategyAbstract
 {
     function action();
 }
 
 //满减活动  manjian.php
 class manjian implements StrategyAbstract
 {
    public function action()
    {
       echo "满减";
    }
 }
 
 //打八折活动  dazhe.php
 class dazhe implements StrategyAbstract
 {
    punlic function action()
    {
      echo "打折";
    }
 }
 
 //策略工厂类 
 class strategy
 {
    private $object;
    
    //初始时传入具体的策略
    public function __contruct($model)
    {
       $this->object = $model;
    }
    
    //执行策略
    public function get()
    {
       $this->object->action()
    }
    
 }
 
 //执行满减的策略
 $a = new strategy(new manjian());
 $a->get();
 
 //执行打折的策略
 $a = new strategy(new dazhe())
 $a->get();

```

### 观察者模式

当一个对象的状态发生改变时，依赖他的对象会全部收到通知，并更新

```php
class BuyMilk
{
   public $name; 
   public $price;  //价钱
   public $store;  //库存
   public $account;//账户余额
   
   //私有变量 用于储存观察者
   private $_observer = array();
   
   public function __contruct($name,$store,$price)
   {
     $this->name = $name;
     $this->store = $store;
     $this->price = $price;
   }
   
   //添加观察者
   public function addObserver($observer)
   {
      $this->_observer[] = $observer;
   }
   
   //通知观察者
   public function notify()
   {
      foreach($this->_observer as $_observer)
      {
         $_observer->update();
      }
   }
   
   public function buy()
   {
      $this->notify();
   }
}

class BuyMilkStoreObserver 
{
    public function update(BuyMilk $product)
    {
        $product->store -=1;
    }
}

class BuyMilkMoneyObserver
{
    public function update(BuyMilk $product)
    {
        $product->account += $product->price;
    }
}

$a = new BuyMilk('HD',10,1);
$a->addObserver(new BuyMilkStoreObserver());

$a->addObserver(new BuyMilkMoneyObserver);

$a->buy();
```


