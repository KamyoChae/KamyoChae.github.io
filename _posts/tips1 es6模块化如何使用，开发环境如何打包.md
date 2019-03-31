## tips1 es6模块化如何使用，开发环境如何打包

#### 模块化基本语法

export 语法



```javascript
/*util1.js*/

export default{
    a: 100
}

/*util2.js*/
export function fn1(){
    alert('fn1')
}
export function fn2(){
    alert('fn2')
}

/*index.js*/
import util1 from './util1.js'
import {fn1, fn2} from './util2.js'
console.log(util1)

fn1()
fn2()

```

- 第一个import 表示引入了util1这个文件的代码，所引用的部分就是export default导出的这个对象，也就是util1 = { a: 100}
- 第二个import 表示将util2文件里面的代码块导出来，由于util2里面没有设置export default，而是export多个，所以可以用es6的解构赋值方式导出





#### 开发环境配置

借用npm包管理器

1. 安装 babel-core、babel-preset-es2015、babel-cli、babel-preset-latest

2. 创建.babelrc文件

   





#### js众多模块化标准



