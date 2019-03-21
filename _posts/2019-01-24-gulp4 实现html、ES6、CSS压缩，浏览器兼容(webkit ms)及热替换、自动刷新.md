---
layout: post
title:  gulp4 实现html、ES6、CSS压缩，浏览器兼容(webkit ms)及热替换、自动刷新
tags: [gulp]
---

其实 gulp4 和gulp3差别不是很大，但不注意的话很容易被坑了

前提条件：
1. 安装了node
2. 安装了git
3. 安装了gulp3
#
具体操作：

### 1. 打开git bash 安装一些插件
```
$ npm install
gulp-connect gulp-strip-debug
gulp-uglify gulp-autoprefixer gulp-clean-css
gulp-babel gulp-less gulp-htmlclean gulp-imagemin 
--save-dev

```
注意：如果安装的babel是7以下，则继续执行下面这行
```javascript
$ npm install babel-core babel-preset-es2015  gulp-babel --save-dev
```
如果安装的babel是7及7以上，则继续执行下面这行
```javascript
npm install @babel/core @babel/preset-env gulp-babel --save-dev

```

### 2.在根目录创建gulpfile.js

### 3.gulpfile内引入文件
```javascript
var gulp = require('gulp');
var uglify=require('gulp-uglify');//js压缩
var less=require('gulp-less');//编译less
var minifyCss = require("gulp-minify-css");//压缩CSS
var minifyHtml = require("gulp-minify-html");//压缩html
var jshint = require("gulp-jshint");//js检查
var imagemin = require('gulp-imagemin');
var connect=require('gulp-connect');//引入gulp-connect模块 


```

### 4.添加任务
```javascript


gulp.task('connect',function(){
    connect.server({
        livereload:true,//自动更新
        port:9909//端口
    })
})

gulp.task("images",function(){
    return gulp.src(folder.src+"images/*") 
    // 读取src/images文件夹下面的所有文件
    .pipe(imagemin())               // 图片压缩
    .pipe(gulp.dest(folder.dist+"images/")) 
    // 输出代码到dist/images目录下面
    .pipe(connect.reload());
})

gulp.task('html',function(){
    return gulp.src('src/*.html')
    .pipe(minifyHtml())
    .pipe(gulp.dest('dist/html'))
    .pipe(connect.reload());
})

gulp.task('css',function(){
    return gulp.src('src/css/*.less')
    .pipe(less())//编译less
    .pipe(minifyCss())//编译less
    .pipe(gulp.dest('src/css')) //当前对应css文件
    .pipe(connect.reload());//更新
})

gulp.task('js',function(){
    return gulp.src('src/js/jquery-1.8.0.min.js')
    .pipe(jshint())//检查代码
    .pipe(uglify())//压缩js
    .pipe(gulp.dest('dist/js'))
    .pipe(connect.reload());
})


gulp.task('watchs',function(){
    gulp.watch('src/*.html',gulp.series('html'));
    gulp.watch('src/css/*.less',gulp.series('css'));
    gulp.watch('src/js/*.js',gulp.series('js'));
    gulp.watch('src/images/*',gulp.series('images'));
})
```


### 5.加入启动队列
```javascript

 //gulp.series|4.0 依赖
 //gulp.parallel|4.0 多个依赖嵌套
gulp.task('default',gulp.series(
            gulp.parallel('connect','watchs','html','css','js')
        )
);
```


### 6.启动gulp，完成
```

$gulp
```
