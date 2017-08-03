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

`<a [routerLink]=[{outlets:{fuzhu:null}}]>链接</a>`

当点击链接的时候，fuzhu插座不显示任何组件

辅助路由允许你在同一个组件中定义多个插座，并定义每个插座显示的内容

## 路由守卫

### 简介

所谓的路由守卫，也就是在满足一定条件的时候才允许进入或退出某一个路由。例如：
- 在用户登录之前，不允许进入个人中心页面
- 在某个表单的执行流程中，只有用户完成了上一步的任务之后，才能进入下一步的环节
- 当用户没有执行保存操作而试图离开某一个路由的时候，阻止离开并进行提示

路由守卫主要有三种类型：
- CanActivate 是否能进入到某个路由
- CanDeactivate 是否能离开某个路由
- Resolve 在路由激活之前获取数据

现在，在路由对象里我们有多了一个新的参数：canActivate，该参数是数组格式，也就是说，一条路由允许接收多个守卫

**那么如何编写守卫呢？**

### canActivate守卫

在`src`目录中建立一个存放守卫的目录`guard`，新建路由守卫TypeScript文件，例如`login.guard.ts`，下面展示一个简单的Demo：

（为了便于演示，不去做真正的登录服务，只是生成一个随机数来判断是否已经登录）

```typescript
import {canActivate} from "@angular/router";

export class LoginGuard implements CanActivate {
	canActivate(){
		// 假设随机数小于0.5就代表已经登录
		let isLogin:boolean = Math.random()<0.5;

		if(!isLogin){
			console.log("未登录");
		}

		return isLogin;
	}
}
```
```typescript
import {LoginGuard} from "./guard/login.guard";

{path:'product/:id',component:ProductComponent,children:[......],canActivate:[LoginGuard]}

...

@NgModule({
	imports:[...],
	exports:[...],
	providers:[LoginGuard]
})
```

这样，我们就是先了一个简单的路由守卫，当我们试图导航到这个路由的时候，会判断守卫返回的Boolean值，为True则通过。

> ！还有这种操作？！在学Angular的时候顺便学了TypeScript~

### canDeactivate守卫

同理，我们能很轻易地区是先一个canDeactivate守卫，区别在于canDeactivate守卫在是先接口的时候需要制定一个泛型（也就是需要保护的组件），算了，直接上代码吧：

```typescript
import {CanDeactivate} from "@angular/router";
import {ProductComponent} from "../product/";

export class UnsavedGuard implements CanDeactivate<ProductComponent>{
	/*
	需要实现一个方法
	因为是需要离开，那么这里需要根据组件里的某些状态来判定
	*/
	canDeactivate(component:ProductComponent){
		return window.confirm("您还没保存，确定要离开吗？");
	}
}
```

### Resolve守卫

Resolve守卫常用于解决数据预加载问题，如果使用路由中传递的参数，在进入某一个组件之后发出Http请求去获取所需要的数据，那么在刚进入这个组件的时候，所有使用插值表达式的位置都是空的，这样用户体验会很差。这时候可以使用Resolve守卫来解决，在进入之前先获取数据，进入之后立即使用并显示出来

```typescript
import {ActivatedRouteSnapshot, Resolve, Router, RouterStateSnapshot} from '@angular/router';
import {Product} from '../product/product.component';
import {Observable} from 'rxjs/Observable';
import {Injectable} from '@angular/core';

@Injectable() // 装饰器，允许注入
export class ProductResolve implements Resolve<Product> {
  // 注入路由对象
  constructor(private router: Router) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Product | Observable<Product> | Promise<Product> {
    const productId: number = route.params['id'];
    if (productId === 1) {
      return new Product(1, '小米6', 2999, 5, '很不错的手机', ['数码'])
    } else {
      this.router.navigate(['/home']);
      return undefined;
    }
  }

}
```

在路由中我们有遇到了一个新的参数：`resolve`，接收一个数组（Resolve守卫）

```typescript
{path:'product/:id',component:ProductComponent,resolve:{product:ProductResolve}}
```

同样需要在providers里声明一下。

那么如何取出Resolve守卫传入的数据呢？

同样可以使用参数订阅的方式：

```typescript
// routeInfo:ActivatedRoute
this.routeInfo.data.subscribe((data:{product:Product})=>{
	this.productId=data.product.id;
});
```

好了，路由的知识点到现在就告一段落，但是Angular的学习之路仍未完待续......

# 依赖注入（Dependency Injection）

正常情况下，我们写的代码应该是这样子的：

```typescript
let product = new Product();	// 实例化一个对象
createOrder(product);	// 调用方法传入商品对象，生成订单
```
createOrder方法依赖product类，但是createOrder方法自身并不知道也不能去创建一个product对象。我们把方法所需的对象实例化并当做参数传入，这个过程就成为把参数注入给这个方法。在此你可能看不出什么，但是如果依赖的对象比较多了呢？我们需要反复去new，反复去生成对象，然后传入到方法中......想想就是噩梦。

那么，能不能让某人替我们创建createOrder所依赖的对象和对象所依赖的其他对象呢？如果可以的话，那么，我们只需要写一句方法的调用即可，对象都将会呗自动创建好，并当做参数传递进去（想想就很美妙，懒人必备啊）。

也就是说，对象A只需要声明，我需要一个B类型的对象，那么这个对象就会从外部注入进来，这就是依赖注入要解决的问题。

与依赖注入经常同时出现的另一个概念叫做控制反转（Inversion Of Control），简称IOC。

控制反转是指将依赖的控制权从代码的内部转移到代码的外部，如上代码所示，方法所需的依赖是由方法的内部所决定的，如果需要改变依赖，就需要修改方法内部的代码，外面不管是传入Product的实例，还是传入Product子类的实例，是有方法外部决定的。

IOC着重描述目的；DI着重描述实现的方法，即如何去实现控制反转。实现了控制反转模式的框架被称为IOC容器。

## 实现依赖注入

那么如何在Angular中实现以来注入呢？

### 定义提供器

首先，使用命令行工具生成一个`service`，用于提供注入服务。

`ng g service shared/product`

由于product是共享的，所以放到了一个自定义的shared文件夹

接下来，对生成的服务进行编辑（由于当前没有对这个服务进行注册，显然不会生效）

```typescript
import {Injectable} from '@angular/core';

@Injectable()
export class ProductService {

  constructor() { }

  getProduct(): Product {
    return new Product(1, '小米Mix', 3999, '很666的手机');
  }

}

/**
 * 定义一个Product商品类
 */
export class Product {
  constructor(public id: number, public title: string, public price: number, public desc: string) { }
}
```

下面，进入app.module，注册服务

```typescript
...
  providers: [ProductService],
...
```

在使用的时候（需要获取product对象的时候，直接在构造函数中声明需要Product类型的变量，即可完成注入。

```typescript
constructor (product:Product){  }
```

> 这时候，注入提供器声明在了模块中，也可以在组件的@component()中添加providers属性，这时候，作用域就变成了当前组件，并且组件中声明的提供器比模块的优先级更高

#### 使用工厂声明提供器

如果在实例化类的时候需要传递参数，或需要进行一些操作去得到一个注入对象，那么使用工厂声明一个提供器是更好的解决办法。

```typescript
providers: [{
    provide: ProductService,
    useFactory: () => {
      const dev = Math.random() > 0.5;
      if (dev) {
        return new Product(1, '小米6', 2999, '很6的手机');
      } else {
        return new Product(2, '小米mix', 3999, '很美的手机');
      }
    }
  }],
```

那么，如果工厂方法依赖一个LoggerService，我们如何去解耦合并把loggerServices注入到工厂方法呢？需要使用第三个参数：

```typescript
providers: [{
    provide: ProductService,
    useFactory: (logger:LoggerService) => {
      const dev = Math.random() > 0.5;
      if (dev) {
        return new Product(1, '小米6', 2999, '很6的手机');
      } else {
        return new Product(2, '小米mix', 3999, '很美的手机');
      }
    },
    deps:[LoggerService]
  },LoggerService],
```

如此，即可实现工厂方法的依赖注入

### 使用具体的值定义提供器

```typescript
providers: [{
    provide: ProductService,
    useFactory: (logger:LoggerService,appConfig) => {
      if (appConfig.isDev) {
        return new Product(1, '小米6', 2999, '很6的手机');
      } else {
        return new Product(2, '小米mix', 3999, '很美的手机');
      }
    },
    deps:[LoggerService,"APP_CONFIG"]
  },LoggerService,{
  	provide:"APP_CONFIG",
	useValue:{isDev:false}
  }],
```

注意，被注入的类都需要有一个`@Injectable()`装饰器，这样才能被注入

> 那么你可能会疑惑了，angular组件控制器的类并没有`@Injecdtable()`装饰器，但是构造函数却能被注入，这是因为`@component()`装饰器的实现一键集成了`@Injectable()`


为了更容易理解，接下来实现一下手工注入：

```typescript
import {Injector} from '@angular/core';

export class ProductComponent implements OnInit {

  private product: ProductService;

  constructor(private injector: Injector) {
    this.product = injector.get(ProductService);
  }
}
```

> Angular的依赖注入只有一个注入点，也就是构造函数。

# 数据绑定

数据绑定允许你将组件控制器的属性和方法与组件的模板连接起来，大大降低了开发时的编码量。

常见的表现形式有：
- 插值表达式：`<h1>{{title}}</h1>`，即把属性|表达式插入到HTML标签中
- 属性绑定：`<img [src]="imgUrl" />`，也就是将属性|表达式绑定到HTML标签的属性上
- 事件绑定：`<button (click)="show()"></button>`，讲组件控制器的一个方法绑定到模板元素的事件上

在Angular中，默认的数据绑定是单向的（AngularJS1.0中全部是双向绑定，这也是性能差的原因之一），所谓的双向绑定，也就是控制器的属性反映到模板中，同时，模板中显示出的属性被修改之后，对应的控制器属性同时发生变化；单向绑定取出了模板=>控制器的方向，使性能大大提升。（当然，双向绑定并不是被去掉了，你也可以手动指定使用双向绑定,双向绑定现在变成了一个可选项，而不是框架的默认行为）

## 事件绑定

```html
<button (click)="doOnClick($event)"></button>
```

```typescript
doOnClick(event:any){
	console.log(event);
}
```

如上代码是一个经典的事件绑定例子，被绑定的事件可以是一个标准事件也可以是一个自定义事件，绑定的操作可以是控制器里的一个方法，也可以只一个赋值表达式等等。

## 属性绑定

如下例子所示

```html
// 使用属性绑定
<img [src]="imgUrl" />
// 使用插值表达式
<img src="{{imgUrl}}" />
```

又是一个经典的例子，不难理解，上面两个方法实现的效果是完全一致的，事实上，这两个方法没有优劣之分，你只需要按照自己的喜好去选择即可

## HTML属性绑定

1. 基本HTMl属性绑定

```html
<td [attr.colspan]="value"></td>
```

2. class绑定

```html
<div class="aaa bbb" [class]="val"></div>	// 这种情况会覆盖原先的class
<div [class.aaa]="booleanVal"></div>	// 通过一个Boolean值开关来控制是否启用某一个class名，适合管理单一class名
<div [ngClass]="{aaa:isA,bbb:isB}"></div>	// 通过对象的形式开控制多个class的开关，适合同时管理多个className
```

3. 样式绑定

和class绑定类似，只不过绑定的对象为style属性

```html
<button [style.color]="isRed?'red':'green'">Red</button>
<div [ngStyle]="{color:red,'font-style':bool?'italic':'normal'}"></div>
```

## 双向绑定

双向绑定即视图和模型保持同步，无论视图和模型哪一方改变，另一方都一起同步改变。

前面所学到的事件绑定是从视图到模型，把模板中元素的事件绑定到控制器中的方法；属性绑定的方向是从控制器到模板，使用方括号讲组件控制器的属性绑定到模板。

```html
<input [value]="name" (input)="doOnInput($event)" />
```
```typescript
export class BindComponent implements OnInit {
	name: string;
	
	doOnInput(event){
		this.name=event.target.value;
	}
}
```
这样就实现了一个双向绑定，当input内容变化的时候，出发事件，修改模型中的属性值，当模型中的属性值改变的时候，优惠在视图中表现出来。

当然，Angular肯定提供了内置的双向绑定支持：

```html
<input [(ngModel)]="name" />
```

由于`[(ngModel)]`用在input元素上，默认绑定的是`input`事件。双向绑定最常用的用途就是表单处理。

> 当然，双向绑定本来就应该用于input系列元素上，因为这些元素允许你去修改这些值，并显示出来。

将会在表单处理章节更详细讲。

# 管道

举个例子，例如我要在页面上显示我的生日信息，假设现在从服务器获取到的日期是一个Date对象，那么把它直接输出到页面上肯定是用户体验很不好的（一大串乱七八糟的字符串）。管道就是用来处理数据的，从原始值到你所需要的值，这一个过程。

使用实例：

```html
<p>{{birthday | date | uppercase}}</p>
```

上面例子中我们就使用了两个内置的管道，第一个是获取到Date对象的日期信息，第二个是把小写字母转换成大写。

## 内置管道

常用的管道：
- uppercase 大写
- lowercase 小写

**date日期管道**

> 日期管道符可以接受参数，用来规定输出日期的格式。
> `<p>现在的时间是{{today | date:'yyyy-MM-dd HH:mm:ss'}}</p>`

**number 数字处理管道**

> 接收的参数格式为{最少整数位数}.{最少小数位数}-{最多小数位数} 
> 其中最少整数位数默认为1 
> 最少小数位数默认为0 
> 最多小数位数默认为3 
> 当小数位数少于规定的{最少小数位数}时，会自动补0 
> 当小数位数多于规定的{最多小数位数}时，会四舍五入

## 自定义管道

1. 生成管道：`ng g pipe pipe/multiple`，此处用来做Demo的管道作用是扒一个数放大n倍，也就是乘法……

生成的管道代码：

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'multiple'
})
export class MultiplePipe implements PipeTransform {

  transform(value: any, args?: any): any {
    return null;
  }

}
```

可以看出，管道是一个实现了PipeTransform并且带有@Pipe装饰器的类，用于把源数据根据参数和方法定义处理成想要的结果。

> 但是，当你打开`app.modules.ts`的时候，你会发现在declaration数组里多出来了一个MultiplePipe的声明，也就是说，管道也是需要声明的，只是命令行工具自动添加进去了。

其中value是管道前端的原始值，args是一个可选参数，也就是管道的参数，最终管道把处理结果返回出去即可。

如下，我们很轻易地创建了一个管道：

```typescript
import {Pipe, PipeTransform} from '@angular/core';

@Pipe({
  name: 'multiple'
})
export class MultiplePipe implements PipeTransform {

  transform(value: number, args?: number): number {
    if (!args) {
      args = 1;
    }
    return value * args;
  }

}
```

在实战项目中，我们对管道有了新的用法，根据传入的参数来过滤商品列表：

```typescript
import {Pipe, PipeTransform} from '@angular/core';
import {Product} from '../shared/product.service';

@Pipe({
  name: 'productFilter'
})
export class ProductFilterPipe implements PipeTransform {

  transform(productList: Product[], filterField: string, keyword: string): any {
    if (!filterField || !keyword) {
      return productList;
    }
    return productList.filter((product: Product) => product[filterField].indexOf(keyword) >= 0);
  }

}
```

# 组件间通信

要想开发出重用性高、松耦合的组件，光有依赖注入是不够的，接下来我们继续学习如何使用松耦合的方式在组件之间传递数据

要学习的知识点主要有：

- 组件的输入输出属性，在两个具有父子关系的组件间传递数据
- 什么是中间人模式，如何实现中间人模式，在没有父子关系的组件间传递数据
- 组件的生命周期，Angular的变化发现机制

## 输入输出属性

要想开发一个松耦合的组件，我们应该把组件打造成一个黑盒模型，组件无需去知道是谁在输入，只需要在被输入之后在黑盒内进行处理，得到想要的结果即可，保持和其他组件之间的松耦合关系。

### 输入属性

前面我们在开发星级评分组件的时候使用到了`@Input()`装饰器，`输入属性`就是用`@Input()`装饰器装饰的属性。例如：

```typescript
export class OrderComponent implements OnInit {
	@Input()
	stockCode: string;	// 股票代码
	
	@Input()
	amount: number;	// 购买数量
}
```

上述代码是组件`app-order`的控制器，在父组件中使用的时候输入数据的方式如下：

```html
// 与父组件的stock属性进行双向绑定
<input type="text" placeholder="请输入股票代码" [(ngModel)]="stock" />
// 双向绑定之后的属性stock作为子组件<app-order></app-order>的参数传入
<app-order [stockCode]="stock" [amount]="100"></app-order>
```

如此，便实现了父组件和子组件的解耦合。

> 这里的属性绑定也是单向的，也就是说，子组件对应的属性变化不会影响到父组件

总结一下，输入属性是由父组件向子组件单向传递参数。

### 输出属性

所谓输出属性即组件向外发出事件

结合上面的例子，我们实现一个股票价格更新事件。

```typescript
import {Emitter} from "@angular/core";

export class PriceQuoteComponent implements OnInit{
	stockCode: string='IBM';
	price: number;
	
	// 定义事件抛出者
	@Output()	// 括号中可以自定义抛出的事件的名称
	lastPrice=EventEmitter<ProductQuote> = new ProductEmitter();	// 定义事件抛出装置
	
	constructor () {
		setInterval(
			()=>{
				let priceQuote: PriceQuote = new PriceQuote(this.stockCode,Math.random()*100);	// 生成一个报价对象
				this.lastPrice.emit(priceQuote);	// 抛出事件
			},1000
		);
	}
}

export class PriceQuote {
	constructor (
		public stockCode: string,
		public lastPrice: number
	) {
	}
}
```

当这个组件的事件抛出之后，在父组件中，子组件的标签上添加事件绑定即可，和前面的事件绑定类似：

```html
<app-price-quote (lastPrice)="eventHandle($event)"></app-price-quote>
```

其中，传入的参数`$event`即`PriceQuote`对象。

这样，就实现了子组件向父组件的数据传递。

**但是，如果两个组件之间不存在父子关系呢？请看下面的中间人模式**

## 中间人模式

当你设计一个组件时，这个组件应该是内聚的，不应该依赖外部已经存在的组件要实现这么一个松耦合组件，可以使用中间人模式。

> 中间人负责从一个组件接收数据，并将数据传给另一个组件。

还是举上面的栗子，股票报价页面有一个下单按钮，但是报价组件并不知道如何去厦大，这时候，点击按钮可以把股票代码和价格传递给中间人，中间人知道谁可以执行下单操作，负责带着参数去找执行者。

给股票报价页面添加一个下单购买按钮：

```html
<input tyle='button' (click)="buyStock($event)" />
```

在报价控制器中添加一个方法，用于想歪发射一个事件：

```typescript
import {EventEmitter} from "@angular/core";

...

// 定义一个事件发射器，发出购买事件（带上报价实例）
@Output()
buy:EventEmitter<PriceQuote> = new EventEmitter();

// （点击之后）执行发射事件的方法
buyStock(event){
	this.buy.emit(new PriceQuote(this.stockCode,this.price));
}
```

这样，在报价组件的父组件中，很容易地就能通过在`<app-price-quote>`上监听`buy`事件来获取发射出去的报价信息（和上节一样）。