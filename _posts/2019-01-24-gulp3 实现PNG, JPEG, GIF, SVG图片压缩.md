---
layout: post
title:  gulp3 实现PNG, JPEG, GIF, SVG图片压缩
tags: [gulp]
---



以前的老项目了，写几篇gulp3的文章，后面再折腾一下gulp4

前提条件：
1. 安装了node
2. 安装了git
3. 安装了gulp3
#
具体操作：

### 1. 打开git bash 安装gulp-imagemin
 
```javascript
$ npm install gulp-imagemin --save-dev
```
gulp-imagemin：对图片进行压缩


### 2.在根目录创建gulpfile.js

### 3.在gulpfile内引入文件
```javascript
var gulp = require('gulp')
var babel = require('gulp-imagemin') 
```
  
### 4.添加task任务
```javascript
var folder = {
    'src':'src/',
    'dist':'dist/'
}
gulp.task("images",function(){
    gulp.src(folder.src+"images/*") // 读取src/images文件夹下面的所有文件
    .pipe(imagemin())               // 图片压缩
    .pipe(gulp.dest(folder.dist+"images/")) // 输出代码到dist/images目录下面
})
```

### 5.加入启动队列
```javascript

gulp.task("default", ["images"])
```

### 6.启动gulp，完成
```
$gulp
```

