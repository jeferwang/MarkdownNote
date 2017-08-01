---
title: Angular4.0从入门到实战打造在线竞拍网站学习笔记
tags: JavaScript,Angular
grammar_cjkRuby: true
---


[TOC]

最近搞到手了一部Angular4的视频教程(是不是感觉和慕课的那个很像...没错),这几天正好有时间变学了一下,可以用来做一些前后端分离的网站,也可以直接去打包web app。

# 环境&版本信息声明

运行`ng -v`

```
@angular/cli: 1.2.0
node: 8.1.2
os: win32 x64
@angular/* 4.2.5
...
```


**好吧,那就顺便写个笔记/教程/备忘/博客咯**

# 安装Angular脚手架

安装的时候选择全局安装

`npm install @angular/cli -g`

# 创建Angular项目

运行命令

`ng new AngularStudy`

其中`AngularStudy`是项目文件夹名称

# 启动项目开发环境

在当前创建的项目目录下运行 如下命令

`ng serve`或者`npm run start`,然后在浏览器中进入所提示的地址,默认是`http://127.0.0.1:4200/`

当你访问页面的时候出现AngularLogo的时候,说明你的项目已经创建成功了,反之,请检查错误信息或日志

> 提示:在我学习的过程中遇到了一个问题,就是在Windows10系统中,当你的用户文件夹是中文名称的时候,你就要小心了,你很有可能会在创建过程中遇到错误,具体是什么错误...额我忘了,那个错误百度谷歌都找不到答案,如果你解决不了,检查一下是不是这个问题,百度有修改用户文件夹名称的教程(需要修改注册表,小白慎入)

# 安装jQuery和Bootstrap

在我们的开发流程中,jQuery和Bootstrap这两个框架已经是不可或缺的一部分了,那么,如何在Angular中优雅地安装并使用呢?

其实这很简单,首先运行以下两条命令安装jQuery和Bootstrap:

```
npm install jquery --save
npm install bootstrap --save
```

这时候,两个框架就已经安装到了我们的`node_modules`模块目录下了

但是你会发现,在TypeScript中尝试使用`$`符号的时候,编辑器仍然不能识别,这是为什么呢?

经过Google的提示,终于解决了这个问题

安装JQuery的类型描述文件,运行如下命令

`npm install @types/jquery --save-dev`

同理安装Bootstrap的TypeScript类型描述文件

`npm instakll @types/bootstrap --save-dev`

安装这两个类型描述模块的目的是让TypeScript认识jQuery和Bootstrap的语法,进而能在ts文件中使用它们

OK,是不是很简单呢?

# 生成组件

Angular毕竟是有Google做后台的,功能方面也相当齐全,component不需要我们手动地去创建,只需要一条命令即可生成

在项目根目录运行`ng g component navbar` 生成导航条组件

这条命了的意思就是`angular generate component navbar`,简单明了

有了这条命令,我们就能很轻易地生成项目中的组件

|  组件名   |  用途   |
| --- | --- |
|  app   |  项目自带的默认component   |
|  navbar  |  网页/APP导航条   |
|  search   |  搜索区域   |
|  product   |  商品详情   |
|  stars   |  星级评分   |
|  foot   |  底部信息   |

就这样,我们的项目骨架就搭建完成了

# 对模块进行布局

模块创建完成了,那么,我们下一步需要做什么?当然是就像拼图一样,使用创建好的模块,拼接起来,成为一个简单的单页面应用咯!

至于我们的拼图底板是什么,分析Angular的启动,`app`作为默认显示出来的component,肯定是在`app.component.html`中进行拼接了。

打开我们的`app.component.html`,删除里面无用的内容,使用我们刚刚创建的component在里面拼图吧

一般情况下,我们创建的组件所对应的css元素选择器(也就是标签),名字是`app-componentName`

最终拼合结果如下所示,这样,我们的单页面应用的基本骨架就搭建出来啦~

```html
<!--导航条-->
<app-navbar></app-navbar>
<!--/导航条-->
<!--主要内容容器-->
<div class="container">
  <div class="row">
    <!--左侧-->
    <div class="col-md-3">
      <!--搜索区域-->
      <app-search></app-search>
      <!--/搜索区域-->
    </div>
    <!--/左侧-->
    <!--右侧-->
    <div class="col-md-9">
      <div class="row">
        <!--轮播图-->
        <app-carousel></app-carousel>
        <!--/轮播图-->
      </div>
      <div class="row">
        <!--商品信息-->
        <app-product></app-product>
        <!--/商品信息-->
      </div>
    </div>
    <!--/右侧-->
  </div>
</div>
<!--/主要内容容器-->
<!--底部信息-->
<app-footer></app-footer>
<!--/底部信息-->
```
# 组件编写

## 导航条navbar

组件html内容如下

```html
<!--Bootstrap导航条-->
<nav class="navbar navbar-inverse navbar-fixed">
  <!--导航条内容容器-->
  <div class="container">
    <!--导航条头部-->
    <div class="navbar-header">
      <button class="navbar-toggle btn" data-toggle="collapse" data-target="#navbar-collapse-menu">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <!--//商标/Logo-->
      <a class="navbar-brand" href="javascript:void(0)">在线竞拍</a>
    </div>
    <!--/导航条头部-->
    <!--导航条列表菜单-->
    <div class="collapse navbar-collapse" id="navbar-collapse-menu">
      <ul class="nav navbar-nav">
        <li><a href="javascript:void(0)">关于我们</a></li>
        <li><a href="javascript:void(0)">联系我们</a></li>
        <li><a href="javascript:void(0)">网站地图</a></li>
      </ul>
    </div>
    <!--/导航条列表菜单-->
  </div>
  <!--/导航条内容容器-->
</nav>
<!--/Bootstrap导航条-->
```

```css
.main-wrap{
  margin-top: 70px;
}
```
这时候,我们需要在css文件中添加样式,使中间部分内容乡下偏移约70px,因为fix格式的导航条会盖住内容。

> 默认的全局css文件是`/src/style.css`当然也可以在配置文件中更改或者添加新的css文件

> 当然,每一个组件对应的css样式我们应该分开写,比如navbar的css写在navbar.component.css文件中


## 底部信息footer

由于尚未编写业务逻辑,简单地先做一下占位即可

```html
<div class="container">
  <hr>
  <footer>
    <div class="row">
      <div class="col-md-12">
        <p>Angular打造竞拍网站</p>
      </div>
    </div>
  </footer>
</div>
```

```css
footer{
  text-align: center;
}
```

## 商品搜索组件

就是上面那个套路,都是使用Bootstrap框架所带的那些css样式,直接贴代码,学过的应该都能看懂。

```html
<form role="form" name="searchForm">
  <div class="form-group">
    <label for="productTitle" class="control-label">商品名称：</label>
    <input id="productTitle" type="text" class="form-control" placeholder="商品名称">
  </div>
  <div class="form-group">
    <label for="productPrice" class="control-label">商品价格：</label>
    <input id="productPrice" type="number" class="form-control" placeholder="商品价格">
  </div>
  <div class="form-group">
    <label for="productCategory" class="control-label">商品类别：</label>
    <select id="productCategory" class="form-control"></select>
  </div>
  <div class="form-group">
    <label for="productTitle" class="control-label">商品名称：</label>
    <input type="submit" class="btn btn-primary btn-block" value="搜索">
  </div>
</form>
```

## 轮播图组件

轮播图稍微有些复杂,因为不仅仅使用了HTML,同时也使用了少量的JavaScript和jQuery。当然我相信，来学Angular的肯定不是小白咯。

当然,这一部分主要就是实现一个简单的轮播图,也没有用到什么Angular代码

```html
<div class="carousel slide" data-ride="carousel">
  <!--轮播图导航区域-->
  <ol class="carousel-indicators">
    <li class="active"></li>
    <li></li>
    <li></li>
  </ol>
  <!--/轮播图导航区域-->
  <!--轮播图片区域-->
  <div class="carousel-inner">
    <div class="item active">
      <img src="http://placehold.it/800x300" alt="carousel" class="slide-image">
    </div>
    <div class="item">
      <img src="http://placehold.it/800x300" alt="carousel" class="slide-image">
    </div>
    <div class="item">
      <img src="http://placehold.it/800x300" alt="carousel" class="slide-image">
    </div>
  </div>
  <!--/轮播图片区域-->
  <!--轮播图控制按钮-->
  <a href="javascript:$('.carousel').carousel('prev')" class="left carousel-control">
    <i class="glyphicon glyphicon-chevron-left"></i>
  </a>
  <a href="javascript:$('.carousel').carousel('next')" class="right carousel-control">
    <i class="glyphicon glyphicon-chevron-right"></i>
  </a>
  <!--/轮播图控制按钮-->
</div>
```

```css
.slide-image{
  width:100%;
}
```
> 从下一部分开始我们就需要接触到更多Angular的知识了

## 商品详情组件

首先,每一件商品都是一个对象,那么我门可以建立如下的模型:

`product.component.ts`

```typescript
export class Product {
  constructor(
    public id: number,
    public title: string,
    public price: number,
    public rating: number,
    public desc: string,
    public categories: Array<string>
  ) {

  }
}
```

然后,在这个ts文件中进行商品(对象)的实例化(因为现在还没有学到http)

```typescript
export class ProductComponent implements OnInit {

  public products: Array<Product>;

  constructor() {
  }

  ngOnInit() {
    this.products = [
      new Product(1, '第一个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电']),
      new Product(2, '第二个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电']),
      new Product(3, '第三个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电']),
      new Product(4, '第四个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电']),
      new Product(5, '第五个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电']),
      new Product(6, '第六个商品', 899, 3.5, '这是一个垃圾电脑', ['电子产品', '家电'])
    ]
  }

}
```

这样,即可在模块实例化的时候获取到商品对象列表,并传递到component模板中

> `ngOnInit()`方法会在component实例化的时候自动调用一次,这个知识点稍后会更详细讲到

有了数据之后,下一步当然是制作component模板咯,顺便吧数据也显示出来呗(满满的都是套路额)

```html
<div class="col-sm-4 col-md-4 col-lg-4" *ngFor="let product of products">
  <div class="thumbnail">
    <img src="http://placehold.it/320x150" alt="商品图片">
    <div class="caption">
      <h4 class="pull-right">￥{{product.price}}</h4>
      <h4><a>{{product.title}}</a></h4>
      <p>{{product.desc}}</p>
    </div>
    <div>
      <app-stars></app-stars>
    </div>
  </div>
</div>
```

> ngFor可以理解为在html中对一个数组进行循环遍历,同时循环这个html标签……就类似PHP那样,慢慢理解吧,挺简单的额,稍后也会讲到
> 但是这个指令反映出来的思想很重要,Angular的数据绑定,也叫作数据驱动

然后,从开始搞事情以来第一个比较难的地方已经过去了(以后你回头看的时候还会发现...其实好简单的哦)

## 星级评分组件

别看这个组件很小不起眼,但是星际评分组件是当前所有组件里最复杂的一个(相对复杂...)

主要使用了：

> `*ngFor`指令
> `class`绑定
> 组件属性值输入`@Input()`

直接上代码呗

控制器代码如下,这部分代码的关键点在于把`Production component`的`product.rating`注入到`Star Component`中

```typescript
export class StarsComponent implements OnInit {
  @Input()
  public rating: number;
  public stars = [];

  constructor() {
  }

  ngOnInit() {
    const full: number = Math.floor(this.rating);
    const half: number = Math.ceil(this.rating - full);
    const empty: number = 5 - full - half;
    for (let i = 0; i < 5; i++) {
      if (i < full) {
        this.stars.push('full');
      } else if (i === full && half !== 0) {
        this.stars.push('half')
      } else {
        this.stars.push('empty')
      }
    }
  }
}
```

如何注入呢?上面有一个装饰器`@Input()`标识着rating变量是外部注入的

那么,在实例化`star component`的位置……

就是这里!!!

```html
 <app-stars [rating]="product.rating"></app-stars>
```

就是这么简单

接下来当然是模板代码咯,关键点都在这里

```html
<p>
  <i *ngFor="let star of stars" class="fa"
     [class.fa-star]="star==='full'"
     [class.fa-star-half-o]="star==='half'"
     [class.fa-star-o]="star==='empty'"
  ></i>
  <span>{{rating}}星</span>
</p>
```
> 这里首先使用`ngFor`指令对`i`标签(星星)进行遍历
> 接下来使用`[class.xxx]`进行样式绑定,根据控制器里组合成的数组进行星星标签的生成
> 这里使用了`Font-Awesome`图标

代码只要稍微细心看就能看懂,主要就在于样式绑定,根据数组中不同的字符串绑定不同的星星样式

就这样,我们的基本组件已经实现了大部分了,等有空了进行下一章的学习……

# 路由

## 简介

接下来学习路由的相关知识

> 本来是不准备写下去的，因为当时看视频学的时候感觉自己掌握的不错 ( 这是一个灰常不好的想法 ) ,过了一段时间才发现Angular这个对我这个PHP程序猿来说不太常用的东西非常容易忘！幸好之前去写了笔记。

首先需要先了解一个概念(SPA)，也就是单页面应用，一个页面只加载一次，不再刷新，只改变页面部分内容的应用。

路由的作用就是为每一个视图分配一个唯一的URL，进入这个URL的时候，使应用跳到某个特定的视图状态。

## 创建

在创建项目的时候 ， 带上参数`ng new RouterDemo --routing`即可生成一个带路由文件的项目


Angular路由常见对象

|   名称  |  简介   |
| --- | --- |
|  Routes   |  路由的配置，URL和组件之间的映射以及组件和组件插座RouterOutlet的映射关系   |
|  RouterOutlet   |  在HTML中标记组件插入位置的占位符标签   |
|  Router   |  在运行时执行路由的对象,`navigate()`和`navigateByUrl()`方法导航到指定的路由，使用依赖注入在控制器中获取   |
|  RouterLink   |  在HTML中声明路由导航的标签属性   |
|  ActivatedRoute | 当前激活的路由对象，保存着当前路由的信息，如路由地址参数等，使用依赖注入在控制器中获取  |

在项目中,路由文件通常为`app-routing.module.ts`

## 配置

打开路由文件，在routes:Routes对象中定义路由列表，其中，每一个路由至少包含两个参数，即`path`和`component`也就是URL和组件的映射关系

> 注意：这里的`path`最好不要以`/`开头,否则会导致路由URL相对关系的混乱，Angular会自动帮你处理和子路由的关系，除非你明确知道你要做什么

app-routing.module.ts源码

```typescript
import {NgModule} from '@angular/core'
import {RouterModule, Routes} from '@angular/router';
import {ProductDetailComponent} from './product-detail/product-detail.component';
import {HomeComponent} from './home/home.component';

const routes: Routes = [
    {path: '', component: HomeComponent},
    {path: 'product/:prodTitle', component: ProductDetailComponent}
];

@NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule],
    providers: []
})

export class AppRoutingModule {}
```

app.module.ts修改部分

```typescript
imports: [
        ...
        AppRoutingModule
		...		
    ],
```

如上,最简单的路由便定义完毕啦

## 插座

所谓的插座,也就是在HTML中定义的路由对应的组件插入点

使用`<router-outlet></router-outlet>`标签定义路由对应组件的插入位置(在该标签下面)

## 路由链接

使用`<a [routerLink]=['/product']>商品详情</a>`来定义一个路由导航链接

> 注意这里的路由字符串需要加上`/`，后面我们会使用`./`等来区分路由和子路由  
> 路由的参数是一个数组而不是字符串，因为后面我们需要给路由传递参数

然后我们就可以通过点击**商品详情**链接来显示`product`组件的内容了

## 使用Router对象进行导航

当你定义了一个事件进行跳转的时候，例如：

```html
<input type="button" (click)="toProductInfo()" />
```

控制器代码

```typescript
export class AppComponent {
    // 使用依赖注入拿到Router对象
    constructor(private router:Router){}
    // 事件绑定的方法，跳转
    toProductInfo() {
        this.router.navigate(['/product']);
    }
}
```

即可实现用代码进行路由跳转

## 默认路由

当输入一个不存在的地址时，路由插座区域无法显示，并且会在控制台抛出异常，我们可以通过定义一个默认路由（例如404page）来避免错误发生

首先，我们生成一个新的组件，运行`ng g component code404`

生成404页面组件，简单编写内容之后，进入路由配置文件，添加一个新的路由配置信息

```typescript
...
// 放在最后，当匹配不到的时候会选择此路由
{path:'**',component:Code404Component}
```
## 传递参数

### 传递

传递方式 | 形式 | 获取方式
---|--- | ---
查询参数传递（GET方法） | `<a [routerLink]=['/product'] [queryParams]="{id:1}"></a>`=>/?id=1&name=jeffrey | ActivatedRoute.queryParams['id']
在路由形式中定义参数 | {path:'product/:id'}=>`<a [routerLink]=['/product/',1]></a>`=>/product/1 | ActivatedRoute.params['id']
在路由配置中定义静态数据 | {{path:'product/:id',component:ProductComponent,data:[{osProd:true}]}} | ActivatedRoute.data[0]['isProd']

### 获取

在constructor构造函数参数中使用依赖注入获取到`ActivatedRoute`存入`routeInfo`变量，在ngOnInit()取出参数

- 直接取出（参数快照）  
  `this.productId=this.routeInfo.snapshort.queryParams['id']`
- 关联获取（参数订阅），在同翼哥组件之间路由的时候，由于`ngOnInit()`只会执行一次，导致参数不能刷新，这时候可以使用参数订阅来关联地获取到参数。（下面例子使用了箭头函数）  
  `this.routeInfo.params.subscribe((params:Params)=>this.productId=params['id'])`

## 重定向路由

在访问一个特定路由时，重定向到另一个指定地址

例如：

```typescript
{path: '', redirectTo:'/home',pathMatch:'full'},
{path: 'home', component: HomeComponent},
```
> `pathMatch`指匹配策略

当我们访问`http://127.0.0.1:4200`的时候，会自动跳转到`http://127.0.0.1:4200/home`

## 子路由

在一个路由的组件中展示其他组件的内容时，使用子路由来实现。

> 其实更应该理解为“子组件”，也就是一个大的组件里的一部分，使用子路由来控制

在主路由的`routerOutlet`显示主路由的组件内容时，根据子路由的变化，在主路由组件中子路由对应`routerOutlet`位置显示对应的子路由组件

## 辅助路由

形式：`<router-outlet name="fuzhu"></router-outlet>`

`{path:'xxx',component:XxxComponent,outlet:'fuzhu'}`

`<a [routerLink]=['/home',{outlets:{fuzhu:'xxx'}}]>链接</a>`或`<a [routerLink]=[{outlets:{primary:'home',fuzhu:'xxx'}}]>链接</a>`

当点击链接的时候，主插座会显示home组件的内容，fuzhu插座会显示xxx路由匹配到的Xxx组件

`<a [routerLink]=[{outlets:{fuzhu:'xxx'}}]>链接</a>`

当点击链接的时候，主插座不变，fuzhu插座会显示xxx路由匹配到的Xxx组件

辅助路由允许你在同一个组件中定义多个插座，并定义每个插座显示的内容











