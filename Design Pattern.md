# 设计模式(Design Pattern)

## 一、分类

* **构建型**-5种
* **结构型**-7种
* **行为型**-11种
![Design Patterns设计模式](http://p8surce23.bkt.clouddn.com/Design%20Patterns%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F.png)

## 二、设计原则

### 1.单一职责(SRP: Single Responsibility Principle):
- 有且只有一个原因引起类的变更(ex: 属性和动作分离）个人觉得这个原则跟OOP存在冲突,并且Hard to implement

### 2.里式替换原则(LSP: Liskov Substitution Principle):
- 父类出现的位置，必须可以使用子类替换。

### 3.依赖倒置原则(DIP: Dependence Inversion Principle):
* 高层模块不依赖底层模块，应该依赖其抽象
* 抽象不依赖细节
* 细节依赖抽象

对于弱类型语言具有天然的优势，强类型语言有可以依赖泛型。

**一段并不美好的体验**

```swift
class Benz {
    func run() {}
}

class BMW {
    func run() {}  
}

class Driver {
    func drive(_ car: BMW) {
        car.run()
    }
}
```

**我写的代码**

```swift
protocol Drivable {
    func run()
}

class Benz: Drivable {
    func run() {} 
}

class BMW: Drivable {
    func run() {}
}

class Driver {
    func drive<T: Drivable>(_ car: T) {}
}
```

* Best Practice: 本质通过抽象各个类，实现各个类与模块的独立。
* 依赖倒置原则是六个设计模式中最难遵循的原则。

## 三、常见模式分析

### a.工厂模式

> 工厂模式是为了替代类对象的生成，抽象对象的生成过程以便于在运行时确定具体对象。

**Swift**

```swift
class English {
    func sayHello() {
        print("hello")
    }
}

class Chinese {
    func sayHello() {
        print("你好")
    }
}

class Factory {
    func sayHello(with language: String) {
        if language == "English" {
            English().sayHello()
        } else {
            Chinese().sayHello()
        }
    }

}
```

**Python**

```python
class English(object):
    def say_hello(self):
        print("hello")


class Chinese(object):
    def say_hello(self):
        print("你好")
 
def say_hello(language):
    if language == 'English':
        English().say_hello()
    else:
        Chinese().say_hello()   

```

**OC**

```objc
@interface English()

-(void)sayHello;

@end

@implementation English

-(void)sayHello {
    NSLog(@"hello");
}

@end

@interface Chinese()

-(void)sayHello;

@end

@implementation Chinese

-(void)sayHello {
    NSLog(@"你好");
}

@end

@interface Factory()

-(void)sayHelloWithLanguage:(NSString *)language;

@end

@implementation Factory

-(void)sayHelloWithLanguage:(NSString *)language {
    if ([language isEqualToString: @"English"]) {
        English *instance = [[English alloc] init];
        [instance sayHello];
    } else {
        Chinese *instance = [[Chinese alloc] init];
        [instance sayHello];
    }
}

@end

```

**JAVA**

```Java
public interface Language{
    void sayHello();
}

public class English implements Language{
    @Override
    void sayHello(){
        System.out.println("English");
    }
}

public class Chinese implements Language{
    @Override
    void sayHello(){
        System.out.println("Chinese");
    }
}

public class Factory{
    public static void sayHello(String type){
        Language language = null;
        if(type.equalsIgnoreCase("English")){
            language = new English();
        }else{
            language = new Chinese();
        }
        language.sayHello();
    }
}
```

**JS**

```js
class English {
 sayHello(){
  console.log('English');
 }
}

class Chinese {
 sayHello(){
  console.log('chinese');
 }
}

class Factory{
 sayHello(type){
  switch(type){
   case 'English':
    new English().sayHello();
    break;
   case 'Chinese':
    new Chinese().sayHello();
    break;
   default:
    void 0
  }
 }
}
```



