Phalcon Debug Widget
===
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/cf0654ee-b09e-4010-8cc0-a4f5fcdd6167/big.png)](https://insight.sensiolabs.com/projects/cf0654ee-b09e-4010-8cc0-a4f5fcdd6167)

[![Latest Stable Version](https://poser.pugx.org/TransactPRO/phalcon-debug-widget/version?format=flat-square)](https://packagist.org/packages/TransactPRO/phalcon-debug-widget)
[![Total Downloads](https://poser.pugx.org/TransactPRO/phalcon-debug-widget/downloads?format=flat-square)](https://packagist.org/packages/TransactPRO/phalcon-debug-widget)

Note (How it works):
=====
The debug widget for now is very simplistic and more of a proof-of-concept. It expects you have three services in your dependency injector named "db", "dispatcher" and "view" and that they correspond to those services. When you pass the DI to Phalcon Debug Widget It looks for those specific services and:
- sets them as shared services
- sets the eventManager for them
- Attaches itself to those events

This means passing the DI to the debug widget will alter those services. Generally speaking, a shared db, dispatcher, and view is fine. If you have ideas for other ways to hook in, please open an issue for discussion.



The Phalcon Debug Widget is designed to make development easier by displaying debugging information directly in your browser window. Currently it displays php globals such as $_SESSION as well as outputing resource usage and database queries and connection information. It includes syntax highlighting via [Prismjs.com](http://prismjs.com/).

If it looks familiar, its because its modeled after the [Yii debug toolbar](https://github.com/malyshev/yii-debug-toolbar)


## Installation

```json
"require": {
	"transactpro/phalcon-debug-widget": "~1.0"
}
```

## Usage and Configuration



Define a debug or environment flag in your main index.php (or config.php) file so you can easily disable the Phalcon Debug Widget on production environments. Example:

```php
defined('PHALCONDEBUG') || define('PHALCONDEBUG', true);
```

Add these lines to your index.php file before you handle application.
```php
if (PHALCONDEBUG) {
	$debugWidget = new \PDW\DebugWidget($di);
}

echo $application->handle()->getContent();
```

Or you can specify your custom list of providers and panels:
```php
if (PHALCONDEBUG) {
    $debugWidget = new \PDW\DebugWidget($di, [
        'db'          => ['db'],
        'dispatch'    => ['dispatcher'],
        'view'        => ['view'],
        'apiProvider' => ['apiProvider']
    ], [
        'server',
        'request',
        'views',
        'db',
        'api'
    ]);
}

echo $application->handle()->getContent();
```


## Preview

### Server
![](/server-info.png)

### Request
![](/request-info.png)

### Views
![](/views-info.png)

### Database
![](/database-info.png)

### Api calls


## Attribution:

Bug Icon designed by [Nithin Viswanathan](http://thenounproject.com/nsteve) from the [Noun Project](http://thenounproject.com)

JQuery Syntax Highlighting implemented with [Prismjs.com](http://prismjs.com/)


