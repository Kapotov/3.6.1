# Домашнее задание к занятию «Компьютерные сети. Лекция 1»

### Цель задания

В результате выполнения задания вы: 

* научитесь работать с HTTP-запросами, чтобы увидеть, как клиенты взаимодействуют с серверами по этому протоколу;
* поработаете с сетевыми утилитами, чтобы разобраться, как их можно использовать для отладки сетевых запросов, соединений.

### Чеклист готовности к домашнему заданию

1. Убедитесь, что у вас установлены необходимые сетевые утилиты — dig, traceroute, mtr, telnet.
2. Используйте `apt install` для установки пакетов.


### Инструкция к заданию

1. Создайте .md-файл для ответов на вопросы задания в своём репозитории, после выполнения прикрепите ссылку на него в личном кабинете.
2. Любые вопросы по выполнению заданий задавайте в чате учебной группы или в разделе «Вопросы по заданию» в личном кабинете.


### Дополнительные материалы для выполнения задания

1. Полезным дополнением к обозначенным выше утилитам будет пакет net-tools. Установить его можно с помощью команды `apt install net-tools`.
2. RFC протокола HTTP/1.0, в частности [страница с кодами ответа](https://www.rfc-editor.org/rfc/rfc1945#page-32).
3. [Ссылки на другие RFC для HTTP](https://blog.cloudflare.com/cloudflare-view-http3-usage/).

------

## Задание

**Шаг 1.** Работа c HTTP через telnet.

- Подключитесь утилитой telnet к сайту stackoverflow.com:

`telnet stackoverflow.com 80`
 
- Отправьте HTTP-запрос:

```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
```
root@vagrant:~# telnet stackoverflow.com 80
Trying 151.101.65.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 403 Forbidden
Connection: close
Content-Length: 1917
Server: Varnish
Retry-After: 0
Content-Type: text/html
Accept-Ranges: bytes
Date: Thu, 16 Mar 2023 18:52:52 GMT
Via: 1.1 varnish
X-Served-By: cache-fra-eddf8230069-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1678992773.658694,VS0,VE1
X-DNS-Prefetch-Control: off

<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Forbidden - Stack Exchange</title>
    <style type="text/css">
                body
                {
                        color: #333;
                        font-family: 'Helvetica Neue', Arial, sans-serif;
                        font-size: 14px;
                        background: #fff url('img/bg-noise.png') repeat left top;
                        line-height: 1.4;
                }
                h1
                {
                        font-size: 170%;
                        line-height: 34px;
                        font-weight: normal;
                }
                a { color: #366fb3; }
                a:visited { color: #12457c; }
                .wrapper {
                        width:960px;
                        margin: 100px auto;
                        text-align:left;
                }
                .msg {
                        float: left;
                        width: 700px;
                        padding-top: 18px;
                        margin-left: 18px;
                }
    </style>
</head>
<body>
    <div class="wrapper">
                <div style="float: left;">
                        <img src="https://cdn.sstatic.net/stackexchange/img/apple-touch-icon.png" alt="Stack Exchange" />
                </div>
                <div class="msg">
                        <h1>Access Denied</h1>
                        <p>This IP address (77.50.59.174) has been blocked from access to our services. If you believe this to be in error, please contact us at <a href="mailto:team@stackexchange.com?Subject=Blocked%2077.50.59.174%20(Request%20ID%3A%204225685981-FRA)">team@stackexchange.com</a>.</p>
                        <p>When contacting us, please include the following information in the email:</p>
                        <p>Method: block</p>
                        <p>XID: 4225685981-FRA</p>
                        <p>IP: 77.50.59.174</p>
                        <p>X-Forwarded-For: </p>
                        <p>User-Agent: </p>

                        <p>Time: Thu, 16 Mar 2023 18:52:52 GMT</p>
                        <p>URL: stackoverflow.com/questions</p>
                        <p>Browser Location: <span id="jslocation">(not loaded)</span></p>
                </div>
        </div>
        <script>document.getElementById('jslocation').innerHTML = window.location.href;</script>
</body>
</html>Connection closed by foreign host.
```
![2023-03-16_21-53-22](https://user-images.githubusercontent.com/123774335/225724313-fb75c6ab-9598-4831-9e0d-d4938c277512.png)
# Ответ : Код ответа на статус ошибки "HTTP 403 Forbidden" указывает, что сервер понял запрос, но отказывается его авторизовать.

*В ответе укажите полученный HTTP-код и поясните, что он означает.*

**Шаг 2.** Повторите задание 1 в браузере, используя консоль разработчика F12:

 - откройте вкладку `Network`;
 - отправьте запрос [http://stackoverflow.com](http://stackoverflow.com);
 - найдите первый ответ HTTP-сервера, откройте вкладку `Headers`;
 - укажите в ответе полученный HTTP-код;
 - проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 - приложите скриншот консоли браузера в ответ.
![2023-03-16_22-22-22](https://user-images.githubusercontent.com/123774335/225731058-9b7fd55d-9d2f-451e-96e0-fef509243e1e.png)
# Ответ:  HTTP код перенаправления 307 Temporary Redirect означает, что запрошенный ресурс был временно перемещён в URL-адрес, указанный в заголовке Location. Т.е. редирект с http на https протокол того же url. А это значит, что я в первом пункте что-то накосячил, так как там должен был получить тоже самое. Но не смог разобраться и всё оставлю, как есть. Дольше всего обрабатывался запрос - начальная загрузка страницы 295мс. 

**Шаг 3.** Какой IP-адрес у вас в интернете?
# Ответ: 77.50.59.174 (скрин ниже) 
**Шаг 4.** Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`.
# Ответ: провайдер StarLink Telecom , AS34602 (Скрин ниже) 
**Шаг 5.** Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`.
# Ответ: Вот скрин, как и обещал, там собственно все AS. Пробить получилось только root@vagrant:~# grep OrgName <(whois AS15169) OrgName:        Google LLC
![2023-03-16_22-32-56](https://user-images.githubusercontent.com/123774335/225734407-307c3c34-87ac-4d46-90d8-068ed4fb06d7.png)

**Шаг 6.** Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка — delay?
![2023-03-16_22-43-36](https://user-images.githubusercontent.com/123774335/225735471-7bd2ac5d-8c61-4fe7-9f97-7c0fe78b605f.png)
# Ответ: Наибольшая задержка на 17 хопе 18.1мс получается. 
**Шаг 7.** Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой `dig`.
# Ответ:
```
$ dig +short NS dns.google
ns1.zdns.google.
ns2.zdns.google.
ns3.zdns.google.
ns4.zdns.google.

$ dig +short A dns.google
8.8.8.8
8.8.4.4
```
**Шаг 8.** Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой `dig`.
![2023-03-16_22-50-31](https://user-images.githubusercontent.com/123774335/225736951-0c94582f-f366-4545-9a17-d49ca08fdef2.png)

# Ответ:
*В качестве ответов на вопросы приложите лог выполнения команд в консоли или скриншот полученных результатов.*

----

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки. 
