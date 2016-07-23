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

Quick Installation
------------------
Begin by installing the package through Composer.

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
