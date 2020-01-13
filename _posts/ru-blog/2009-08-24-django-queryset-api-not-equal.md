---
layout: post
title: Django QuerySet API - ограничение запроса по not equal
date:   2020-01-08 22:01
comments: true
tags:
- lang:ru
- django
- python
homepage: true
permalink: /django-queryset-api-not-equal
redirect_from: 
- /2009/08/django-queryset-api-not-equal.html
---
Продолжим с Django. В стандартном QuerySet API существует большое количество параметров выборки такие как EXACT, CONTAINS, IN, GT, GTE и т.д. Остальные и документацию, если еще кто-то из интересующихся темой не читал, можно прочитать по приведенным ссылкам.

Проблема встречается тогда, когда хочется найти NE что эквивалентно not equal, т.е. когда мы хотим сделать выборку записей в которых определенное поле "не равно" какому то значению. Дело в том что этого почему то нет в queryset api.

Немножко погуглив можно найти решение, а можно его подсмотреть прямо здесь :), причем есть вроде несколько вариантов в последних версиях Django (на момент написания это 1.1). А вот и пример решения задачи.

{% highlight python %}
examples = MyModel.objects.only('id').filter(
    ~Q(user=request.user),
    is_active=True
)
{% endhighlight %}

В результате мы получим следующий запрос (в моем случае на примере MySQL):

{% highlight sql %}
SELECT `app_mymodel`.`id` 
FROM `app_mymodel` 
WHERE (NOT (`app_mymodel`.`user_id` = 1 ) AND `app_mymodel`.`is_active` = True )
{% endhighlight %}

Happy coding! 