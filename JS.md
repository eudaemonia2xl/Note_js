### JS

#### 函数和对象的增强

* 纯函数

```javascript
// slice:纯函数
var names = ["abc","cba","nba","mba"]
var newNames = [].slice.apply(names,[1,3])
var newNames2 = [].slice.call(names,1,3)
// react中，组件都必须像纯函数一样保护props不能被修改，只能使用。

// splice 操作数组的利器，不是纯函数
names.splice(2,2)
```

* 柯里化：Currying 

```javascript
// 自动转换柯里化过程（有一点难度）
function xlCurrying(fn) {
  function curryFn(...args) {
    if (args.length >= fn.length) {
      // return fn.apply(this,args)
      return fn(...args)
    } else {
      // return curryFn.apply(this,args.concat(newArgs))
			return curryFn(...args.concat(newArgs))
    }
  }
  return curryFn
}
```

* 组合函数

```js
// 传入多个函数，自动将多个函数组合在一起逐个调用
function composeFn(...fns) {
  // 边界判断
  var length = fns.length
  if (length <= 0) return
  for(var i = 0; i < length; i++) {
    var fn = fns[i]
    if (typeof fn !== "function") {
      throw new Error(`index ${i} must be function`)
    }
  }
  // 返回新的函数
  return function(...args) {
    var result = fns[0].apply(this,args)
    for (var i = 1; i < length; i++) {
      var fn = fns[i]
      result = fn.apply(this,[result])
		}
    return result
	}
}
```

#### 面向对象原型

* 对象原型：查找属性找不到时去原型上查找：`__proto__`
* 函数原型:   通过new操作符创建对象时，将函数的显示原型 `prototype`赋值给新创建对象的隐式原型`__proto__`

