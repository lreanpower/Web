# JavaScript

## 箭头函数

```
//返回一个对象
() => {}
//将对象赋值给变量
() => ({})
```

## 扩展运算符

扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

```javascript
console.log(...[1, 2, 3])
```

## `for...of`循环

- `entries()` 返回一个遍历器对象，用来遍历`[键名, 键值]`组成的数组。对于数组，键名就是索引值；对于 Set，键名与键值相同。Map 结构的 Iterator 接口，默认就是调用`entries`方法。

  ```javascript
  let arr = ['a', 'b', 'c'];
  for (let pair of arr.entries()) {
    console.log(pair);
  }
  // [0, 'a']
  // [1, 'b']
  // [2, 'c']
  ```

  

- `keys()` 返回一个遍历器对象，用来遍历所有的键名。

- `values()` 返回一个遍历器对象，用来遍历所有的键值。

```javascript
let arr = [3, 5, 7];
for (let i of arr.values()) {
  console.log(i); //  "3", "5", "7"
}
```



## Array对象的方法

### 静态方法

`Array.isArray`方法返回一个布尔值，表示参数是否为数组。它可以弥补`typeof`运算符的不足。

### 实例方法

#### 会改变原数组

##### 方法的参数为函数

###### sort排序分类

##### 方法的参数不是函数

###### push末尾加，unshift首个加  ，join分隔符， splice删始终插

##### 方法无参数

###### shift首个删，pop末尾减，reverse颠倒排，toString组变串

#### 不会改变原数组，返回一个新数组

##### 方法的参数为函数

###### map单个传进处理，filter过滤，some类似或，every类似与，reduce两两处理，reduceRight，forEach()

##### 方法的参数不是函数

###### concat连数组，slice提始终，indexOf，lastIndexOf，valueOf

#### 不会改变原数组

###### find找符合，includes包含，flat组‘拉平’ 

`forEach()`方法与`map()`方法很相似，也是对数组的所有成员依次执行参数函数。但是，`forEach()`方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用`map()`方法，否则使用`forEach()`方法。

`forEach()`的用法与`map()`方法一致，参数是一个函数，该函数同样接受三个参数：当前值、当前位置、整个数组。

### 链式使用

上面这些数组方法之中，有不少返回的还是数组，所以可以链式使用。

```JavaScript
var users = [
  {name: 'tom', email: 'tom@example.com'},
  {name: 'peter', email: 'peter@example.com'}
];

users
.map(function (user) {
  return user.email;
})
.filter(function (email) {
  return /^t/.test(email);
})
.forEach(function (email) {
  console.log(email);
});
// "tom@example.com"
```

上面代码中，先产生一个所有 Email 地址组成的数组，然后再过滤出以`t`开头的 Email 地址，最后将它打印出来。

