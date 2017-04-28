# JavaScript-Scoping-and-Hoisting
js的作用域和变量提升
##### 先上一段代码
```javascript
  var v='Hello World';
  (function(){
      alert(v);
  })()
  //毫无疑问显示结果是 hello world;
  //再看另一段代码
  var v='Hello World';
  (function(){
      alert(v);
      var v='I love you';
  })()
  //这次的结果居然是undefined ;
```
#### 这里面就是js的陷阱之一  ：变量的提升
##### 在JS中，变量的提升，就是把定义在后面的  变量  或  函数  提升到前面。
  在了解提升之前。先看看js中的作用域
```javascript 
   var x = 1;
      console.log(x); // 1
   if (true) {
     var x = 2;
     console.log(x); //2
  }
   console.log(x);// 2
```
   像if语句这样的块结构并不会创建一个新的作用域。 **只有函数才会创建新的作用域**
   因为Js函数的灵活性，对于这个问题我们有一个解决方案。如果你必须在函数中创建一个临时的作用域，请像下面这样做：
```javascript
     function a() {
        var x = 1;
        if (x) {
            (function () {
                var x = 2;
                // some other code
            }());
        }
        // x is still 1.
    }
```
    ### 变量提升
    我们定义三个变量
```javascript
    (function(){
      var a='One';
      var b='Two';
      var c='Three';
    })()
```
    实际上他们是这样的
```javascript
    (function(){
        var a,b,c;
        a='One';
        b='Two';
        c='Three';
    })()
```
    ok,我们再回到一开始的代码，其实就是这样子的：
```javascript
    var v='Hello World';
    (function(){
        var v;
        alert(v);
        v='I love you';
    })();
```
    因此，才会提示说“undefined”。
    从这里，我们也学习到，我们在写js code 的时候，我么需要把变量放在函数级作用域的顶端，比如我在上面所举的例子：var a,b,c;。以防止出现意外
    
    #### 函数提升
    函数提升是把整个函数都提到前面去。
    js的函数有两种写法，一种是函数表达式，另一种是函数声明的方式。**需要重点注意的是，只有函数声明形式才能被提升.**
```javascript
    function b(){
      foo();
      function foo(){
          alert("我来自 foo");
      }
    }
    b();
```
    函数声明式提升成功；
```javascript
    function myTest(){
      foo();
       var foo =function foo(){
            alert("我来自 foo");
        }
    }
    myTest();
```  
     函数表达式提升成功；
