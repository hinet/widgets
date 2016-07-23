Caffeinated Widgets
=================
[![Laravel 5.1](https://img.shields.io/badge/Laravel-5.1-orange.svg?style=flat-square)](http://laravel.com)
[![Laravel 5.2](https://img.shields.io/badge/Laravel-5.2-orange.svg?style=flat-square)](http://laravel.com)
[![Source](http://img.shields.io/badge/source-caffeinated/menus-blue.svg?style=flat-square)](https://github.com/caffeinated/menus)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://tldrlegal.com/license/mit-license)

在laravel应用中轻松创建可重用的Widgets. Widgets非常类似Laravel的视图控件, 但它更有意义.

这个包符合PSR-1，psr-2，和psr-4规范，确保共享高水平的PHP代码之间的互操作性。 目前，该包没有单元测试，但计划在以后会被测试覆盖.

说明文档
-------------
You will find user friendly and updated documentation in the wiki here: [Caffeinated Widgets Wiki](https://github.com/caffeinated/widgets/wiki)

快速安装
------------------
通过Composer安装这个包.

```
composer require caffeinated/widgets
```

Once this operation is complete, simply add the service provider class and facade alias to your project's `config/app.php` file:

##### Service Provider
```php
Caffeinated\Widgets\WidgetsServiceProvider::class,
```

##### Facade
```php
'Widget' => Caffeinated\Widgets\Facades\Widget::class,
```

And that's it! With your coffee in reach, start building out some awesome widgets!

注册命名空间
------------------
在你开始创建Widget之前，你必须首先注册它的命名空间，这是一个很简单的过程，最好是在一个service provider中，我们通过：Widget::register()来注册，下面提供了一个示例。
```php
<?php
namespace App\Providers;

use Widget;
use Illuminate\Support\ServiceProvider;

class WidgetServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap widget services.
     *
     * @return void
     */
    public function boot()
    {
        //
    }

    /**
     * Register any widget services.
     *
     * @return void
     */
    public function register()
    {
        Widget::register('App\\Widgets');
    }
}
```

Widget::register()通知Caffeinated Widgets通过扫描给定的命名空间来完成应用程序调用.

创建Widget
------------------
现在，我们已经注册了一个命名空间，我们的小部件可能被发现，我们可以继续并创建我们的小部件。作为一个例子，让我们创建一个简单的“Hello World”小部件。下面将提供类，然后我们将在以后的更详细的细节，让您关闭创建自己的小部件。
```php
<?php
namespace App\Widgets;

use Caffeinated\Widgets\Widget;

class HelloWorld extends Widget
{
    /**
     * Handle the widget
     *
     * @return mixed
     */
    public function handle()
    {
        dd('Hello World!');
    }
}
```

正如你所看到的，小部件可以用最少的代码来设置。首先，我们在我们注册的命名空间中创建了我们的小部件类，App\Widgets。其次，所有部件实例必须继承自Caffeinated\Widgets\Widge抽象类。最后，唯一需要的方法必须定义为handle()。这是一个在应用程序调用时被调用的方法，该方法是在一个小部件被调用时被触发的。

从laravel IOC解析附加实例
------------------
当然你可以使用laravel IOC 负载任何额外的类的实例，你可能需要通过构造函数（如库或模型实例）。这个过程是任何其他类的实例的应用同样laravel。
```php
...

/**
 * @var \App\Repositories\Example
 */
protected $repository;

/**
 * Constructor method.
 * 
 * @param  \App\Repositories\Example  $example
 */
public function __construct(\App\Repositories\Example $example)
{
    $this->example = $example;
}

...
```
使用参数
------------------
部件的可选择地传递任何您可以在您的小部件实例中使用的参数数。我们将进入更多的细节，这在调用小部件。

调用Widget
------------------
###Blade
```php
{!! Widget::HelloWorld() !!}
```
###Twig
```php
{{ widget_hello_world() }}
```
传递参数
------------------

如在创建小部件时所提到的，您可以将任意数量的附加参数传递给您的小部件实例。简单地将它们传递到一个key-value数组中：

###Blade
```php
{!! Widget::HelloWorld(['lorem' => 'ipsum']) !!}
```
###Twig
```php
{{ widget_hello_world({'lorem': 'ipsum'}) }}
```
每一个传递的参数，然后在您的小部件类中可用$this->$key.在上面的例子会获得$this->lorem的值为ipsum。
