Установка
=============
```
composer require dastanaron/spamchecker
```

Описание
=============

Данный набор предоставляет возможность запрашивать ip-адреса и хосты, находящиеся в известных
blacklist по спаму. Применений может быть много.

Работает это все следующим образом.

Как то раз я наткнулся на этот [GitHub](https://github.com/IntellexApps/blcheck), который делает тоже самое, только для
консоли линукс, с помощью скрипта на shell. Разобравшись в способах его работы, я решил организовать тоже самое на php,
с возможностью API запросов. 

Есть еще один ресурс <https://hetrixtools.com>, который предоставляет платные апи для тех же целей. 
Ох уж эти жадные программеры, которые за любой пустяк готовы брать деньги. Ну да ладно.

Данный код уже был сделан ранее, но переделан одним моим хорошим знакомым.
В его версии сохранился тот же принцип, но упрощен код.

Данная версия от Alkhimic.

Общие принципы
------------------

В ОС Linux есть такая команда host, которая может делать запросы к DNS записям. С помощью них и организованы большинство blacklists.

```shell
host -t txt 1.0.168.192.all.spamrats.com
```
```
Host 1.0.168.192.all.spamrats.com not found: 3(NXDOMAIN)
```
В данной команде нужно перевернуть IP адрес, и сделать такой запрос. Альтернативная команда в php

[dns_get_record()](http://php.net/manual/ru/function.dns-get-record.php). Вот собственно и весь принцип работы. Все просто.

Пример
=================
```php
use dastanaron\spamchecker\SpamChecker;

$checker = new SpamChecker('blacklist.txt', 5);

// Example clean address
var_dump($checker->check("mail.ru"));

// Example spam address
var_dump($checker->check("182.244.194.17"));
```