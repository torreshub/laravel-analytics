# Laravel Analytcs


## How to install

```shell
composer require baconfy/laravel-analytics
```

config/app.php

```php
...
'providers' => [
    Baconfy\Analytics\Providers\AnalyticsServiceProvider::class,
],
...
```

## Execute

```shell
php artisan migrate

php artisan vendor:publish
```

## In html pages

```html
<script>
    var _bc = _bc || [];

    (function () {
        var bc = document.createElement('script');
        bc.src = '/analytics.js';
        bc.type = 'text/javascript';
        bc.async = true;
        var s = document.getElementsByTagName('script')[0];
        s.parentNode.insertBefore(bc, s);
    })();
</script>
```

## Route 

```
/analytics/visits/Y-m-d/Y-m-d

Ex:

/analytics/visits/2015-07-27/2015-07-27

show

Hora,Visitas,Únicas
00:00,1,1
01:00,2,1
02:00,3,1
03:00,4,1
04:00,5,1
05:00,7,1
06:00,1,1
07:00,4,1
08:00,6,1
09:00,2,1
10:00,3,1
11:00,3,1
12:00,3,1
13:00,15,1
14:00,15,1
```

## Using HighCharts

```html
<div id="container" style="min-width: 310bc; height: 400bc; margin: 0 auto"></div>

<script>
    $(function () {
        $.ajax({url: "/analytics/visits/2015-07-27/2015-07-27"}).done(function (csv) {
            $('#container').highcharts({
                data: {csv: csv},
                title: {text: 'Relatório de visitas'},
                subtitle: {text: 'Source: Analytics'},
                tooltip: {shared: true},
                yAxis: { allowDecimals: false },
                plotOptions: {column: {stacking: 'normal'}}
            });
        });
    });
</script>
```

![alt text](https://raw.githubusercontent.com/baconfy/laravel-analytics/master/screenshot.png "ScreenShot")
