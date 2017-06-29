# fastD Eloquent
使用 Eloquent 替换 fastD 自带的 Medoo

## 安装
```bash
$ composer require zqhong/fastd-eloquent
```

## 配置
修改配置文件 `config/app.conf`，添加 `EloquentServiceProvider`，如下：
```php
<?php
return [
    // 省略了无关配置
    'services' => [
        \ServiceProvider\EloquentServiceProvider::class,
    ],
];
```

## 直接使用
```php
<?php
// create
eloquent_db('default')
    ->table('demo')
    ->insert([
        'content' => 'hello world',
    ]);

// read
// 参数一可省略，默认值为 default
eloquent_db()
    ->table('demo')
    ->where('id', 1)
    ->where('created_at', '<=', time())
    ->get([
        'id',
        'content',
    ]);

// update
eloquent_db()
    ->table('demo')
    ->where('id', 1)
    ->update([
        'content' => 'hello 2',
    ]);

// delete
eloquent_db()
    ->table('demo')
    ->where('id', 1)
    ->delete();
```

## 配置 Model 使用
```php
<?php

namespace Model;

use Illuminate\Database\Eloquent\Model;

class DemoModel extends Model
{
    public $table = 'demo';

    public static function fetchAll()
    {
        return static::query()
            ->get()
            ->toArray();
    }
}
```

## 参考
[Laravel - Database: Query Builder](https://laravel.com/docs/5.4/queries)
[Laravel - Database: Pagination](https://laravel.com/docs/5.4/pagination)
[Laravel - Eloquent: Getting Started](https://laravel.com/docs/5.4/eloquent)
[Laravel - Eloquent: Collections](https://laravel.com/docs/5.4/eloquent-collections)
[Laravel Cheat Sheet](http://cheats.jesse-obrien.ca/)
[Laravel 5.1 LTS 速查表](https://cs.laravel-china.org/)
[Using Eloquent with Slim](https://www.slimframework.com/docs/cookbook/database-eloquent.html)