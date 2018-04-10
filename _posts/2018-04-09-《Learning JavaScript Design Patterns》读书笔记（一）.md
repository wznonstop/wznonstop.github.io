---
layout: default
title: 《Learning JavaScript Design Patterns》读书笔记（一）
keywords: JavaScript设计模式, 构造器模式, prototype
sitecontent: JavaScript设计模式, 构造器模式, prototype
---


2018-04-09-《Learning JavaScript Design Patterns》读书笔记（一）
===================

# 设计模式的种类

每一个设计模式都聚焦于一个面向对象的设计难题或问题，依据要解决的问题类型，可以将设计模式分为下列几种类型：

![设计模式种类](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2018-04-09-0.png)

# JavaScript 设计模式

## 构造器模式

构造器的本质是函数，作用是当新建对象的内存被分配后，用来初始化该对象。

### 对象创建
```javascript
// Each of the following options will create a new empty object:
 
var newObject = {};
 
// or
var newObject = Object.create( Object.prototype );
 
// or
var newObject = new Object();
```

对象赋值：
```javascript
// ECMAScript 3 compatible approaches
 
// 1. Dot syntax
 
// Set properties
newObject.someKey = "Hello World";
 
// Get properties
var value = newObject.someKey;
 
 
 
// 2. Square bracket syntax
 
// Set properties
newObject["someKey"] = "Hello World";
 
// Get properties
var value = newObject["someKey"];
 
 
 
// ECMAScript 5 only compatible approaches
// For more information see: http://kangax.github.com/es5-compat-table/
 
// 3. Object.defineProperty
 
// Set properties
Object.defineProperty( newObject, "someKey", {
    value: "for more control of the property's behavior",
    writable: true,
    enumerable: true,
    configurable: true
});
 
// 下面这个是上面的简写
 
var defineProp = function ( obj, key, value ){
  var config = {
    value: value,
    writable: true,
    enumerable: true,
    configurable: true
  };
  Object.defineProperty( obj, key, config );
};
 
// To use, we then create a new empty "person" object
var person = Object.create( Object.prototype );
 
// Populate the object with properties
defineProp( person, "car", "Delorean" );
defineProp( person, "dateOfBirth", "1981" );
defineProp( person, "hasBeard", false );
 
console.log(person);
// Outputs: Object {car: "Delorean", dateOfBirth: "1981", hasBeard: false}
 
 
// 4. Object.defineProperties
 
// Set properties
Object.defineProperties( newObject, {
 
  "someKey": {
    value: "Hello World",
    writable: true
  },
 
  "anotherKey": {
    value: "Foo bar",
    writable: false
  }
 
});
 
// 3，4中取值的属性可以用1，2的任意一种
```

### 基础构造器
使用"new"关键字可以告诉JavaScript将该函数作为构造器使用。在该构造器中，**this**指向被创建的新对象。一个基础构造器：
```javascript
function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
 
  this.toString = function () {
    return this.model + " has done " + this.miles + " miles";
  };
}
 
// Usage:
 
// We can create new instances of the car
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );
 
// and then open our browser console to view the
// output of the toString() method being called on
// these objects
console.log( civic.toString() );
console.log( mondeo.toString() );
```

