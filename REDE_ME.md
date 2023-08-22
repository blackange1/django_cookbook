* [Створення API за допомогою Django та Django Rest Framework](#створення-api-за-допомогою-django-та-django-rest-framework)
* [Інтродукції](#інтродукції)
    - [Для кого ця книга?](#для-кого-ця-книга)
    - [Як читати цю книгу?](#як-читати-цю-книгу)
* [Налаштування, моделі та адміністрування](#налаштування-моделі-та-адміністрування)
    - [Створення проекту](#створення-проекту)
    - [Налаштування бази даних](#налаштування-бази-даних)
    - [Створення моделей](#створення-моделей)
    - [Активація моделей](#активація-моделей)
* [Простий API із чистим Django](#простий-api-із-чистим-django)
    - [Кінцеві точки та URL-адреси](#кінцеві-точки-та-url-адреси)
    - [Підключення URL-адрес до представлень даних (views)](#підключення-url-адрес-до-представлень-даних-views)
* [Написання поглядів](#написання-поглядів)
    - [Використання API](#використання-api)
    - [Навіщо потрібні DRF?](#навіщо-потрібні-drf)
* [Серіалізація та десеріалізація даних](#серіалізація-та-десеріалізація-даних)
    - [Серіалізація та десеріалізація](#серіалізація-та-десеріалізація)
    - [Створення серіалізаторів](#створення-серіалізаторів)
    - [Детально про `PollSerializer`](#детально-про-pollserializer)
    - [Використання `PollSerializer`](#використання-pollserializer)
* [Перегляди та загальні подання (Views and Generic Views)](#перегляди-та-загальні-подання-views-and-generic-views)
    - [Створення представлень за допомогою `APIView`](#створення-представлень-за-допомогою-apiview)
    - [Використання узагальнених подань DRF для спрощення коду](#використання-узагальнених-подань-drf-для-спрощення-коду)
    - [Більш загальні погляди](#більш-загальні-погляди)
    - [Наступні кроки](#наступні-кроки)
* [Більше переглядів і переглядів](#більше-переглядів-і-переглядів)
    - [Краща структура URL-адреси](#краща-структура-url-адреси)
    - [Зміна поглядів](#зміна-поглядів)
    - [Представляємо `Viewsets` і маршрутизатори](#представляємо-viewsets-і-маршрутизатори)
    - [Вибір базового класу для використання](#вибір-базового-класу-для-використання)
    - [Наступні кроки](#наступні-кроки-1)
* [Управління доступом](#управління-доступом)
    - [Створення користувача](#створення-користувача)
    - [Налаштування схеми автентифікації](#налаштування-схеми-автентифікації)
    - [API входу](#api-входу)
    - [Точний контроль доступу](#точний-контроль-доступу)
    - [Наступні кроки:](#наступні-кроки-2)
* [Тестування та безперервне інтегрування](#тестування-та-безперервне-інтегрування)
    - [Створення тестових запитів](#створення-тестових-запитів)
    - [Тестування API з автентифікацією](#тестування-api-з-автентифікацією)
    - [Використання `APIClient`](#використання-apiclient)
    - [`.post` та create](#post-та-create)
    - [Постійна інтеграція з CircleCI](#постійна-інтеграція-з-circleci)
    - [Налаштування CircleCI](#налаштування-circleci)
    - [Файл конфігурації кола запису](#файл-конфігурації-кола-запису)
* [Тестування та використання API з Postman](#тестування-та-використання-api-з-postman)
    - [Створення HTTP запиту](#створення-http-запиту)
    - [Відповідь](#відповідь)
    - [Колекції](#колекції)
    - [Аутентифікація](#аутентифікація)
* [API документування (з Swagger тощо)](#api-документування-з-swagger-тощо)
    - [Додавання пишної документації](#додавання-пишної-документації)
    - [Використання coreapi для документації](#використання-coreapi-для-документації)
  

# Створення API за допомогою Django та Django Rest Framework

Створення API за допомогою Django та DRF займає місце, де закінчуються навчальні посібники з Django. У підручниках
Django ви створили звичайну програму опитування Django. Ми перебудуємо API для схожої програми.

У наступних розділах ми створимо REST(ish) API з авторизацією, обмеженням швидкості, спочатку з чистим Django, а потім з
DRF. Ми розглянемо тестування, безперервну інтеграцію, інструменти документування та інструменти співпраці API.

---

# Інтродукції

Створення API за допомогою Django та Django Rest Framework починається там, де закінчується підручник "Опитування"
Django, і проведе вас через створення додатку для опитувань, але цього разу з використанням API. Ви вивчите основи
Django Rest Framework, включаючи серіалізацію, перегляди, загальні перегляди, набори переглядів, тестування, контроль
доступу. Ви також дізнаєтеся про документацію API за допомогою swagger і raml.

## Для кого ця книга?

Якщо ви закінчили підручник Django "Опитування" і хочете навчитися використовувати ФПІ для створення API, ця книга
ідеально підходить для вас. Ця книга передбачає певні знання Django та Python, які ви повинні були створити, якщо
закінчили турторіал "Опитування". Жодних знань про ФПІ не передбачається.

## Як читати цю книгу?

Розділи призначені для читання по порядку. Якщо у вас є знання про деякі розділи, ви можете швидко переглянути цей
розділ, але я настійно рекомендую прочитати їх по порядку, оскільки кожен розділ спирається на попередній.

---

# Налаштування, моделі та адміністрування

У цьому посібнику ми розглянемо процес створення API для базової програми опитування. Ми будемо використовувати Python
3.6.x, Django 2.0.x і Django Rest Framework 3.7.x для створення API.

Перш за все, давайте встановимо необхідні модулі у віртуальному середовищі.

```shell
mkvirtualenv pollsapi
pip install Django
pip install djangorestframework
```

## Створення проекту

Перш за все, щоб створити проект, ми повинні перейти до каталогу, де ми хочемо зберегти наш код. Для цього перейдіть до
командного рядка та скористайтеся командою cd. Потім запустіть команду startproject.

```shell
django-admin startproject pollsapi
```

Ця команда дає нам каталог «pollsapi». Вміст цього каталогу виглядає так:

```text
manage.py

pollsapi/
    __init__.py
    settings.py
    urls.py
    wsgi.py
```

## Налаштування бази даних

Ми будемо використовувати базу даних SQlite, яка вже включена в Python. Файл `pollsapi/settings.py` уже мав би правильні
налаштування.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

Тепер скористайтеся командою migrate, яка створює необхідні таблиці бази даних щодо файлу `django_pollsapi/settings.py`.

```shell
python manage.py migrate
```

## Створення моделей

Перш ніж створювати наші моделі бази даних, створимо додаток pollsapi.

```shell
python manage.py startapp polls
```

Наведена вище команда призводить до створення каталогу «polls», що містить різні файли:

```text
admin.py
apps.py
models.py
tests.py
views.py
```

Перейдіть до файлу 'models.py' і почніть писати моделі. Для створення API опитувань ми створимо модель опитування `Poll`
, модель вибору `Choice` та модель голосування `Vote`. Після того, як ми закінчимо розробляти наші моделі,
файл `models.py` має виглядати так:

Ці моделі такі ж, як ви могли б побачити у вступному посібнику Django.

```python
from django.db import models
from django.contrib.auth.models import User


class Poll(models.Model):
    question = models.CharField(max_length=100)
    created_by = models.ForeignKey(User, on_delete=models.CASCADE)
    pub_date = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.question


class Choice(models.Model):
    poll = models.ForeignKey(Poll, related_name='choices', on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=100)

    def __str__(self):
        return self.choice_text


class Vote(models.Model):
    choice = models.ForeignKey(Choice, related_name='votes', on_delete=models.CASCADE)
    poll = models.ForeignKey(Poll, on_delete=models.CASCADE)
    voted_by = models.ForeignKey(User, on_delete=models.CASCADE)

    class Meta:
        unique_together = ("poll", "voted_by")
```

Вищезазначені моделі були розроблені таким чином, що це зробило б наш API плавним процесом.

## Активація моделей

За допомогою простих рядків коду в 'models.py' Django може створити схему бази даних і API доступу до бази даних Python,
який має можливість доступу до об’єктів Poll, Choice, Vote. Щоб створити таблиці бази даних для наших моделей,
програми 'rest_framework' і 'polls' потрібно додати до 'INSTALLED_APPS' у файлі 'django_pollsapi/settings'.

```python
INSTALLED_APPS = (
    ...
    'rest_framework',
    'polls',
)
```

Тепер запустіть команду `makemigrations`, яка сповістить Django про те, що було створено нові моделі та ці зміни
потрібно застосувати до міграції. Виконайте команду `migrate`, щоб виконати фактичне перенесення.

```shell
python manage.py makemigrations polls

python manage.py migrate
```

Створіть порожній `urls.py` у своїй програмі для опитувань.

```python
urlpatterns = [

]
```

Перейдіть до `pollsapi/urls.py` і додайте URL-адреси опитувань.

```python
from django.contrib import admin
from django.urls import path, include, re_path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('polls.urls')),
]
```

Тепер ви можете запустити сервер

```shell
python manage.py runserver
```

Перейдіть у будь-який браузер на ваш вибір і натисніть URL-адресу `http://127.0.0.1:8000`

І ми в бізнесі, нас вітає сторінка Django *Congratulations*. (Хоча ми ще не додали жодних кінцевих точок API.)
![](src/congrats.png)
У наступному розділі ми додамо кінцеві точки API для створення та перегляду опитувань.

Налаштування адмінки Ви повинні зареєструвати `Poll` та `Choice` в адмінці таким чином.

```python
from django.contrib import admin

from .models import Poll, Choice

admin.site.register(Poll)
admin.site.register(Choice)
```

# Простий API із чистим Django

У цій главі ми створимо API за допомогою чистого Django. Ми не будемо використовувати Django Rest Framework (або
будь-яку іншу бібліотеку). Для початку додайте опитування `Poll` за допомогою адміністратора.

## Кінцеві точки та URL-адреси

Наш API матиме дві кінцеві точки, які повертатимуть дані у форматі JSON.

- `/polls/` GETs список `Poll`
- `/polls/<id>/` GETs дані конкретного `Poll`

## Підключення URL-адрес до представлень даних (views)

Напишіть дві функції перегляду заповнювачів і з'єднайте їх у своєму `urls.py`. Ми закінчимо `polls_list`
і `polls_detail` найближчим часом.

```python
# In views.py
def polls_list(request):
    pass


def polls_detail(request, pk):
    pass


# in urls.py
from django.urls import path
from .views import polls_list, polls_detail

urlpatterns = [
    path("polls/", polls_list, name="polls_list"),
    path("polls/<int:pk>/", polls_detail, name="polls_detail")
]
```

---

# Написання поглядів

Тепер ми напишемо `polls_list` і `polls_detail`

```python
from django.shortcuts import render, get_object_or_404
from django.http import JsonResponse

from .models import Poll


def polls_list(request):
    MAX_OBJECTS = 20
    polls = Poll.objects.all()[:MAX_OBJECTS]
    data = {"results": list(polls.values("question", "created_by__username", "pub_date"))}
    return JsonResponse(data)


def polls_detail(request, pk):
    poll = get_object_or_404(Poll, pk=pk)
    data = {"results": {
        "question": poll.question,
        "created_by": poll.created_by.username,
        "pub_date": poll.pub_date
    }}
    return JsonResponse(data)
```

Це має бути стандартний Django для вас. `polls = Poll.objects.all()[:20]`
отримує до 20 об'єктів опитування `Poll`. Отримуємо список словників за допомогою
`{"results": list(polls.values("question", "created_by__username", "pub_date"))}` і повертаємо його `JsonResponse`
. `JsonResponse` - це подібний `HttpResponse` з `content-type=application/json`.

Аналогічно, *polls_detail* отримує конкретне опитування за допомогою `get_object_or_404(Опитування, pk=pk)` і повертає
його, загорнуте в `JsonResponse`.

## Використання API

Тепер ви можете отримати доступ до API за допомогою curl, wget, postman, браузера або будь-яких інших інструментів, що
використовують API. Ось відповідь із curl.

```shell
curl http://localhost:8000/polls/
{"results": [{"pk": 1, "question": "What is the weight of an unladen swallow?", "created_by__username": "shabda", "pub_date": "2018-03-12T10:14:19.002Z"}, {"pk": 2, "question": "What do you prefer, Flask or Django?", "created_by__username": "shabda", "pub_date": "2018-03-12T10:15:55.949Z"}, {"pk": 3, "question": "What is your favorite vacation spot?", "created_by__username": "shabda", "pub_date": "2018-03-12T10:16:11.998Z"}]}
```

Вам слід розглянути можливість використання листоноші або подібного інструменту. Ось як ваш API виглядає в Postman.
![](src/postman_polls_detail.png)

## Навіщо потрібні DRF?

**(DRF = Django Rest Framework)**

Ми змогли зібрати API лише за допомогою Django, без використання DRF, то навіщо нам DRF? Майже завжди вам знадобляться
загальні завдання з вашими API, такі як контроль доступу, серіалізація, обмеження швидкості тощо.

DRF надає продуманий набір базових компонентів і зручні точки гачка для побудови API. Ми будемо використовувати DRF в
інших розділах.

---

# Серіалізація та десеріалізація даних

DRF робить процес створення веб-API простим і гнучким. З акумуляторами в комплекті він постачається з добре розробленими
базовими класами, які дозволяють нам серіалізувати та десеріалізувати дані.

## Серіалізація та десеріалізація

Перше, що нам потрібно для нашого API, це забезпечити спосіб серіалізації екземплярів моделі в представлення.
Серіалізація — це процес створення потокового представлення даних, які ми можемо передати через мережу. Десеріалізація є
його зворотним процесом.

## Створення серіалізаторів

Давайте почнемо зі створення класів серіалізаторів, які серіалізують і десеріалізують екземпляри моделі до представлень
json. Створіть файл з назвою `polls/serializers.py`. Ми будемо використовувати `ModelSerializer`, який зменшить
дублювання коду шляхом автоматичного визначення набору полів і створення реалізацій методів `create()` і `update()`.
Наш `polls/serializers.py` виглядає так.

```python
from rest_framework import serializers

from .models import Poll, Choice, Vote


class VoteSerializer(serializers.ModelSerializer):
    class Meta:
        model = Vote
        fields = '__all__'


class ChoiceSerializer(serializers.ModelSerializer):
    votes = VoteSerializer(many=True, required=False)

    class Meta:
        model = Choice
        fields = '__all__'


class PollSerializer(serializers.ModelSerializer):
    choices = ChoiceSerializer(many=True, read_only=True, required=False)

    class Meta:
        model = Poll
        fields = '__all__'
```

## Детально про `PollSerializer`

Наш `PollSerializer` виглядає так.

```python
...


class PollSerializer(serializers.ModelSerializer):
    choices = ChoiceSerializer(many=True, read_only=True, required=False)

    class Meta:
        model = Poll
        fields = '__all__'
```

Що ми маємо з цього? Клас `PollSerializer` має низку методів,

- Метод `is_valid(self, ..)`, який може визначити, чи є дані достатніми та дійсними для створення/оновлення екземпляра
  моделі.
- Метод `save(self, ..)`, який знає, як створити чи оновити екземпляр.
- Метод `create(self, validated_data, ..)`, який знає, як створити екземпляр. Цей метод можна змінити, щоб налаштувати
  поведінку створення.
- Метод `update(self, instance, validated_data, ..)`, який знає, як оновити екземпляр. Цей метод можна змінити, щоб
  налаштувати поведінку оновлення.

## Використання `PollSerializer`

Давайте використаємо серіалізатор для створення об’єкта `Poll`.

```shell
In [1]: from polls.serializers import PollSerializer

In [2]: from polls.models import Poll

In [3]: poll_serializer = PollSerializer(data={"question": "Mojito or Caipirinha?", "created_by": 1})

In [4]: poll_serializer.is_valid()
Out[4]: True

In [5]: poll = poll_serializer.save()

In [6]: poll.pk
Out[6]: 5
```

Рядок `poll.pk` повідомляє нам, що об'єкт передано до БД. Ви також можете використовувати серіалізатор для оновлення
об'єкта опитування `Poll`.

```shell
In [9]: poll_serializer = PollSerializer(instance=poll, data={"question": "Mojito, Caipirinha or margarita?", "created_by": 1})

In [10]: poll_serializer.is_valid()
Out[10]: True

In [11]: poll_serializer.save()
Out[11]: <Poll: Mojito, Caipirinha or margarita?>

In [12]: Poll.objects.get(pk=5).question
Out[12]: 'Mojito, Caipirinha or margarita?'
```

Ми бачимо, що виклик save для серіалізатора з екземпляром призводить до оновлення екземпляра.
`Poll.objects.get(pk=5).question` перевіряє, чи було оновлено опитування. У наступному розділі ми будемо використовувати
серіалізатори для написання представлень.

---

# Перегляди та загальні подання (Views and Generic Views)

У цьому розділі ми створимо представлення за допомогою `APIVIew`, `generics.ListCreateAPIView` та сімейства.

## Створення представлень за допомогою `APIView`

[comment]: <> (FIXED: додати посилання на другий розділ Простий API з чистим Django)
Для початку ми використаємо `APIView` для створення списку опитувань і API деталей опитування, який ми створили в
розділі 'Простий API з чистим Django'.

Додайте це до нового файлу `polls/apiviews.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from django.shortcuts import get_object_or_404

from .models import Poll, Choice
from .serializers import PollSerializer


class PollList(APIView):
    def get(self, request):
        polls = Poll.objects.all()[:20]
        data = PollSerializer(polls, many=True).data
        return Response(data)


class PollDetail(APIView):
    def get(self, request, pk):
        poll = get_object_or_404(Poll, pk=pk)
        data = PollSerializer(poll).data
        return Response(data)
```

І змініть свій `urls.py` на

```python
from django.urls import path

from .apiviews import PollList, PollDetail

urlpatterns = [
    path("polls/", PollList.as_view(), name="polls_list"),
    path("polls/<int:pk>/", PollDetail.as_view(), name="polls_detail")
]
```

DRF постачається з API для перегляду, тож ви можете безпосередньо відкривати `http://localhost:8000/polls/` у браузері.
Виглядає це так
![](src/browsable-api-poll-details.png)

```python
{
    "name": "Poll List",
    "description": "",
    "renders": [
        "application/json",
        "text/html"
    ],
    "parses": [
        "application/json",
        "application/x-www-form-urlencoded",
        "multipart/form-data"
    ]
}
```

Ось так це виглядає у postman.
![](src/postman-poll-detail-options.png)

## Використання узагальнених подань DRF для спрощення коду

`PollList` і `PollDetail` виконують роботу, але є купа загальних операцій, ми можемо зробити це абстрактно.

Загальні погляди Django Rest Framework допомагають нам у повторному використанні коду. Вони роблять висновок про формат
відповіді та дозволені методи з класу серіалізатора та базового класу.

Змініть свій `apiviews.py` на наведений нижче код і залиште urls.py як є.

```python
from rest_framework import generics

from .models import Poll, Choice
from .serializers import PollSerializer, ChoiceSerializer,

VoteSerializer


class PollList(generics.ListCreateAPIView):
    queryset = Poll.objects.all()
    serializer_class = PollSerializer


class PollDetail(generics.RetrieveDestroyAPIView):
    queryset = Poll.objects.all()
    serializer_class = PollSerializer
```

З цією зміною запити GET до `/polls/` і `/polls/<pk>/` продовжують працювати, як і раніше, але ми маємо більше даних,
доступних за допомогою OPTIONS.

Виконайте запит OPTIONS до `/polls/`, і ви отримаєте таку відповідь.

```json
{
  "name": "Poll List",
  "description": "",
  "renders": [
    "application/json",
    "text/html"
  ],
  "parses": [
    "application/json",
    "application/x-www-form-urlencoded",
    "multipart/form-data"
  ],
  "actions": {
    "POST": {
      "id": {
        "type": "integer",
        "required": false,
        "read_only": true,
        "label": "ID"
      }
      // ...
    },
    "question": {
      "type": "string",
      "required": true,
      "read_only": false,
      "label": "Question",
      "max_length": 100
    },
    "pub_date": {
      "type": "datetime",
      "required": false,
      "read_only": true,
      "label": "Pub date"
    },
    "created_by": {
      "type": "field",
      "required": true,
      "read_only": false,
      "label": "Created by"
    }
  }
}
}
```

Це говорить нам

- Наш API тепер приймає POST
- Обов'язкові поля даних
- Тип кожного поля даних.
- Досить чудово! Ось так це виглядає в Postman.
  ![](src/postman-options-2.webp)

## Більш загальні погляди

Давайте додамо перегляд для створення варіантів і для голосування. Незабаром ми розглянемо цей код уважніше.

```python
from rest_framework import generics

from .models import Poll, Choice
from .serializers import PollSerializer, ChoiceSerializer, VoteSerializer


class PollList(generics.ListCreateAPIView):
    queryset = Poll.objects.all()
    serializer_class = PollSerializer


class PollDetail(generics.RetrieveDestroyAPIView):
    queryset = Poll.objects.all()
    serializer_class = PollSerializer


class ChoiceList(generics.ListCreateAPIView):
    queryset = Choice.objects.all()
    serializer_class = ChoiceSerializer


class CreateVote(generics.CreateAPIView):
    serializer_class = VoteSerializer
```

Підключіть новий apiviews до urls.py.

```python
# ...
from .apiviews import ChoiceList, CreateVote,  # ...

urlpatterns = [
    # ...
    path("choices/", ChoiceList.as_view(), name="choice_list"),
    path("vote/", CreateVote.as_view(), name="create_vote"),

]
```

Тут багато чого відбувається, давайте подивимося на атрибути, які нам потрібно змінити або встановити.

- `queryset` (набір запитів): це визначає початковий набір запитів. Набір запитів можна додатково відфільтрувати,
  нарізати або впорядкувати за переглядом.
- `serializer_class`: це буде використано для перевірки та десеріалізації вхідних даних і для серіалізації виведення.

Ми використали три різні класи з `rest_framework.generic`. Назви класів є типовими для того, що вони роблять, але
давайте швидко розглянемо їх.

- `ListCreateAPIView`: отримати список сутностей або створити їх. Дозволяє GET і POST.
- `RetrieveDestroyAPIView`: отримання деталей окремої сутності або видалення сутності. Дозволяє GET і DELETE.
- `CreateAPIView`: дозволяє створювати сутності, але не показувати їх у списку. Дозволяє POST.

Створіть кілька варіантів, надіславши POST до `/choices/`.

```json
{
  "choice_text": "Flask",
  "poll": 2
}
```

Відповідь виглядає так

```json
{
  "id": 4,
  "votes": [],
  "choice_text": "Flask",
  "poll": 2
}
```

Ви також можете отримати `Poll` опитування, виконавши `GET` до `/polls/<pk>/`. У вас повинно вийти щось подібне

```json
{
  "id": 2,
  "choices": [
    {
      "id": 3,
      "votes": [],
      "choice_text": "Django",
      "poll": 2
    },
    {
      "id": 4,
      "votes": [],
      "choice_text": "Flask",
      "poll": 2
    }
  ],
  "question": "What do you prefer, Flask or Django?",
  "pub_date": "2018-03-12T10:15:55.949721Z",
  "created_by": 1
}
```

Якщо ви зробите помилку під час публікації, API попередить вас. ОПУБЛІКУЙТЕ файл json із відсутнім текстом `choice_text`
у `/choices/`.

```json
{
  "poll": 2
}
```

Ви отримаєте таку відповідь

```json
{
  "choice_text": [
    "This field is required."
  ]
}
```

Перевірте код статусу 400 Неправильний запит.

## Наступні кроки

На даний момент у нас є робочий API, але ми можемо спростити наш API за допомогою кращого дизайну URL-адреси та видалити
деяке дублювання коду за допомогою наборів переглядів. Ми зробимо це в наступному розділі.
---

# Більше переглядів і переглядів

## Краща структура URL-адреси

У нас є три кінцеві точки API

- `/polls/` та `/polls/<pk>/`
- `/choices/`
- `/vote/`

Вони виконують свою роботу, але ми можемо зробити наш API більш інтуїтивно зрозумілим, правильно вклавши їх. Наші
перероблені URL-адреси виглядають так:

- `/polls/` and `/polls/<pk>`
- `/polls/<pk>/choices/` ОТРИМАТИ варіанти для певного опитування та створити варіанти для конкретного опитування. (
  Позначається `<pk>`)
- `/polls/<pk>/choices/<choice_pk>/vote/` - Голосувати за вибір, визначений `<choice_pk>` під опитуванням з `<pk>`.

## Зміна поглядів

Ми внесемо зміни в `ChoiceList` і `CreateVote`, оскільки `/polls/` і `/polls/` не змінилися.

```python
from rest_framework import generics
from rest_framework.views import APIView
from rest_framework import status
from rest_framework.response import Response

from .models import Poll, Choice
from .serializers import PollSerializer, ChoiceSerializer, VoteSerializer


# ...
# PollList and PollDetail views

class ChoiceList(generics.ListCreateAPIView):
    def get_queryset(self):
        queryset = Choice.objects.filter(poll_id=self.kwargs["pk"])
        return queryset

    serializer_class = ChoiceSerializer


class CreateVote(APIView):
    serializer_class = VoteSerializer

    def post(self, request, pk, choice_pk):
        voted_by = request.data.get("voted_by")
        data = {'choice': choice_pk, 'poll': pk, 'voted_by': voted_by}
        serializer = VoteSerializer(data=data)
        if serializer.is_valid():
            vote = serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        else:
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

І змініть свій urls.py на вкладену структуру.

```python
# ...
urlpatterns = [
    path("polls/<int:pk>/choices/", ChoiceList.as_view(), name="choice_list"),
    path("polls/<int:pk>/choices/<int:choice_pk>/vote/", CreateVote.as_view(), name="create_vote"),
]
```

Ви можете побачити зміни, виконавши GET на `http://localhost:8000/polls/1/choices/`, що має дати вам.

```json
[
  {
    "id": 1,
    "votes": [],
    "choice_text": "Flask",
    "poll": 1
  },
  {
    "id": 2,
    "votes": [
    ],
    "choice_text": "Django",
    "poll": 1
  }
]
```

Ви можете проголосувати за вибір 2, опитування 1, зробивши POST, щоб `http://localhost:8000/polls/1/choices/2/vote/` з
даними `{"voted_by": 1}`.

```json
{
  "id": 2,
  "choice": 2,
  "poll": 1,
  "voted_by": 1
}
```

Повернемося до `ChoiceList`.

```python
# urls.py
# ...
urlpatterns = [
    # ...
    path("polls/<int:pk>/choices/", ChoiceList.as_view(), name="choice_list"),
]


# apiviews.py
# ...

class ChoiceList(generics.ListCreateAPIView):
    def get_queryset(self):
        queryset = Choice.objects.filter(poll_id=self.kwargs["pk"])
        return queryset

    serializer_class = ChoiceSerializer
```

З URL-адрес ми передаємо `pk` до `ChoiceList`. Ми замінюємо метод `get_queryset`, щоб відфільтрувати варіанти з
цим `poll_id`, і дозволяємо DRF обробляти решту.

І для `CreateVote`,

```python
# urls.py
# ...
urlpatterns = [
    # ...
    path("polls/<int:pk>/choices/<int:choice_pk>/vote/", CreateVote.as_view(), name="create_vote"),
]


# apiviews.py
# ...

class CreateVote(APIView):

    def post(self, request, pk, choice_pk):
        voted_by = request.data.get("voted_by")
        data = {'choice': choice_pk, 'poll': pk, 'voted_by': voted_by}
        serializer = VoteSerializer(data=data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        else:
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

Ми передаємо ідентифікатор опитування та ідентифікатор вибору. Ми підкласифікуємо це з `APIView`, а не з загального
вигляду, оскільки ми конкуруємо з налаштуванням поведінки. Це схоже на наш попередній `APIView`, де ми передаємо дані
серіалізатору, зберігаємо або повертаємо помилку залежно від того, чи є серіалізатор дійсним.

## Представляємо `Viewsets` і маршрутизатори

Наші URL-адреси виглядають добре, і ми маємо перегляди з дуже невеликим дублюванням коду, але ми можемо зробити краще.

URL-адреси `/polls/` і `/polls/<pk>/` вимагають двох класів перегляду з однаковим серіалізатором і базовим набором
запитів. Ми можемо згрупувати їх у набір переглядів і з’єднати з URL-адресами за допомогою маршрутизатора.

Ось як це буде виглядати:

```python
# urls.py
# ...
from rest_framework.routers import DefaultRouter
from .apiviews import PollViewSet

router = DefaultRouter()
router.register('polls', PollViewSet, basename='polls')

urlpatterns = [
    # ...
]

urlpatterns += router.urls

# apiviews.py
# ...
from rest_framework import viewsets

from .models import Poll, Choice
from .serializers import PollSerializer, ChoiceSerializer, VoteSerializer


class PollViewSet(viewsets.ModelViewSet):
    queryset = Poll.objects.all()
    serializer_class = PollSerializer
```

URL-адреси чи відповіді взагалі не змінюються. Ви можете перевірити це, виконавши GET для `/polls/` і `/polls/<pk>/`.

## Вибір базового класу для використання

Наразі ми бачили 4 способи створення представлень API

- Чисті перегляди Django
- підкласи `APIView`
- `generics.*` підкласи
- `viewssets.ModelViewSet`

Отже, який з них слід використовувати, коли? Моє правило:

- Використовуйте `viewsets.ModelViewSet,` якщо ви збираєтеся дозволити всі або більшість операцій CRUD на моделі.
- Використовуйте `generics.*`, коли ви хочете дозволити лише деякі операції над моделлю
- Використовуйте `APIView`, якщо ви хочете повністю налаштувати поведінку.

## Наступні кроки

У наступному розділі ми розглянемо додавання контролю доступу до нашого API.

---

# Управління доступом

У цьому розділі ми додамо контроль доступу до наших API та додамо API для створення та автентифікації користувачів.

Зараз наші API повністю дозвільні. Будь-хто може створювати, отримувати доступ і видаляти будь-що. Ми хочемо додати ці
елементи керування доступом.

- Користувач повинен мати автентифікацію, щоб отримати доступ до опитування або списку опитувань.
- Лише автентифіковані користувачі можуть створювати опитування.
- Лише автентифікований користувач може створити вибір.
- Автентифіковані користувачі можуть створювати варіанти вибору лише для створених ними опитувань.
- Автентифіковані користувачі можуть видаляти лише створені ними опитування.
- Голосувати може лише автентифікований користувач. Користувачі можуть голосувати за чужі опитування.

Щоб увімкнути контроль доступу, нам потрібно додати ще два API

- API для створення користувача ми будемо називати цю кінцеву точку `/users/`
- API для верифікації користувача та отримання токена для його ідентифікації, ми будемо називати цю кінцеву
  точку `/login/`

## Створення користувача

Ми додамо користувальницький серіалізатор, який дозволить створювати. Додайте наступний код до
`serializers.py.`

```python
# ...
from django.contrib.auth.models import User


# ...
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ('username', 'email', 'password')
        extra_kwargs = {'password': {'write_only': True}}

    def create(self, validated_data):
        user = User(
            email=validated_data['email'],
            username=validated_data['username']
        )
        user.set_password(validated_data['password'])
        user.save()
        return user
```

Ми замінили метод ModelSerializer `create()`, щоб зберегти екземпляри `User`. Ми гарантуємо, що ми встановили пароль
правильно за допомогою `user.set_password`, а не встановлюємо необроблений пароль як хеш. Ми також не хочемо повертати
пароль у відповідь, що ми гарантуємо, використовуючи `extra_kwargs = {'password': {'write_only': True}}`.

Давайте також додамо перегляди до серіалізатора користувача для створення користувача та підключимо його до urls.py

```python
# in apiviews.py
# ...
from .serializers import PollSerializer, ChoiceSerializer, VoteSerializer, UserSerializer


# ...
class UserCreate(generics.CreateAPIView):
    serializer_class = UserSerializer


# in urls.py
# ...
from .apiviews import PollViewSet, ChoiceList, CreateVote, UserCreate

urlpatterns = [
    # ...
    path("users/", UserCreate.as_view(), name="user_create"),
]
```

Ми можемо протестувати цей API, опублікувавши на `/users/` цей json.

```json
{
  "username": "nate.silver",
  "email": "nate.silver@example.com",
  "password": "FiveThirtyEight"
}
```

Які повертають цю відповідь.

```json
{
  "username": "nate.silver",
  "email": "nate.silver@example.com"
}
```

Спробуйте опублікувати той самий json, і ви отримаєте відповідь про помилку (код статусу HTTP 400)

```json
{
  "username": [
    "A user with that username already exists."
  ]
}
```

## Налаштування схеми автентифікації

За допомогою Django Rest Framework ми можемо налаштувати схему автентифікації за замовчуванням, яка застосовуватиметься
до всіх представлень за допомогою `DEFAULT_AUTHENTICATION_CLASSES`. У цьому підручнику ми будемо використовувати маркер
автентифікації. У вашому settings.py додайте це.

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework.authentication.TokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    )
}
```

Вам також потрібно ввімкнути додаток `rest_framework.authtoken,` тому оновіть `INSTALLED_APPS` у своєму settings.py.

```python
INSTALLED_APPS = (
    # ...
    'rest_framework.authtoken'
)
```

Запустіть `python manage.py migrate`, щоб створити нові таблиці.

```python
REST_FRAMEWORK = {
    # ...
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    )
}
```

Крім того, не забудьте надати виняток перегляду `UserCreate` для автентифікації, замінивши глобальне
налаштування. `UserCreate` у `polls/apiviews.py` має виглядати наступним чином.

```python
class UserCreate(generics.CreateAPIView):
    authentication_classes = ()
    permission_classes = ()
    serializer_class = UserSerializer
```

Зверніть увагу на `authentication_classes = ()` і `permission_classes = ()`, щоб виключити `UserCreate` із глобальної
схеми автентифікації.

Ми хочемо переконатися, що маркери створюються під час створення користувача в поданні `UserCreate`, тому ми
оновлюємо `UserSerializer`. Змініть `serializers.py` таким чином

```python
from rest_framework.authtoken.models import Token


class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ('username', 'email', 'password')
        extra_kwargs = {'password': {'write_only': True}}

    def create(self, validated_data):
        user = User(
            email=validated_data['email'],
            username=validated_data['username']
        )
        user.set_password(validated_data['password'])
        user.save()
        Token.objects.create(user=user)
        return user
```

## API входу

Оскільки ми додали `rest_framework.authentication.TokenAuthentication`, нам потрібно буде встановити такий заголовок, як
цей `Authorization: Token c2a84953f47288ac1943a3f389a6034e395ad940` для автентифікації. Нам потрібен API, де користувач
може вказати своє ім’я користувача та пароль і отримати назад маркер.

Ми не будемо додавати серіалізатор, оскільки ми ніколи не зберігаємо маркер за допомогою цього API.

Додайте подання та підключіть його до URL-адрес.

```python
# in apiviews.py
# ...
from django.contrib.auth import authenticate


class LoginView(APIView):
    permission_classes = ()

    def post(self, request, ):
        username = request.data.get("username")
        password = request.data.get("password")
        user = authenticate(username=username, password=password)
        if user:
            return Response({"token": user.auth_token.key})
        else:
            return Response({"error": "Wrong Credentials"}, status=status.HTTP_400_BAD_REQUEST)


# in urls.py
# ...

from .apiviews import PollViewSet, ChoiceList, CreateVote, UserCreate, LoginView

urlpatterns = [
    path("login/", LoginView.as_view(), name="login"),
    # ...
]
```

ПОПЕРЕДЖЕННЯ: Ви повинні створити користувача за допомогою кінцевої точки `/user/` перед входом за допомогою кінцевої
точки `/login/`. Використання попереднього користувача призведе до помилки 'Користувач не має auth_token', оскільки ми
не створили для нього маркер. Ви можете створити для них маркери вручну за допомогою оболонки
django `python manage.py shell`.

```python
from django.contrib.auth.models import User
from rest_framework.authtoken.models import Token

user = User.objects.get(pk=pk_of_user_without_token)
Token.objects.create(user=user)
< Token: e2b9fa2d4ae27fe1fdcf17b6e37711334d07e167 >
```

Зробіть POST з правильним іменем користувача та паролем, і ви отримаєте таку відповідь.

```json
{
  "token": "c300998d0e2d1b8b4ed9215589df4497de12000c"
}
```

ОПУБЛІКУЙТЕ повідомлення з неправильним іменем користувача та паролем, і ви отримаєте ось таку відповідь із статусом
HTTP 400.

```json
{
  "error": "Wrong Credentials"
}
```

Іншим способом створення цієї кінцевої точки входу є використання методу obtain_auth_token наданого DRF

```python
# in urls.py
# ...
from rest_framework.authtoken import views

urlpatterns = [
    path("login/", views.obtain_auth_token, name="login"),
    # ...
]
```

## Точний контроль доступу

Спробуйте отримати доступ до `/polls/` API без жодного заголовка. Ви отримаєте помилку з кодом статусу
http `HTTP 401 Unauthorized` неавторизовано, як це.

```json
{
  "detail": "Authentication credentials were not provided."
}
```

Додайте заголовок авторизації `Authorization: Token <your token>`, і ви зможете отримати доступ до API.

Відтепер у всіх подальших запитах ми використовуватимемо такий HTTP-заголовок, `Authorization: Token <your token>`.

У нас залишилося дві речі, які ми повинні виконати.

- Автентифіковані користувачі можуть вибирати лише ті опитування, які вони створили.
- Автентифіковані користувачі можуть видаляти лише створені ними опитування.

Ми зробимо це, перевизначивши `PollViewSet.destroy` і `ChoiceList.post.`

```python
# ...
from rest_framework.exceptions import PermissionDenied


class PollViewSet(viewsets.ModelViewSet):
    # ...

    def destroy(self, request, *args, **kwargs):
        poll = Poll.objects.get(pk=self.kwargs["pk"])
        if not request.user == poll.created_by:
            raise PermissionDenied("You can not delete this poll.")
        return super().destroy(request, *args, **kwargs)


class ChoiceList(generics.ListCreateAPIView):
    # ...

    def post(self, request, *args, **kwargs):
        poll = Poll.objects.get(pk=self.kwargs["pk"])
        if not request.user == poll.created_by:
            raise PermissionDenied("You can not create choice for this poll.")
        return super().post(request, *args, **kwargs)
```

В обох випадках ми перевіряємо `request.user` на відповідність очікуваному користувачеві та повідомляємо про
помилку `PermissionDenied`, якщо вона не збігається.

Ви можете перевірити це, зробивши ВИДАЛИТИ в чужому опитуванні `Poll`. Ви отримаєте помилку з `HTTP 403 Forbidden` і
відповіддю.

```json
{
  "detail": "You can not delete this poll."
}
```

Подібним чином спроба створити вибір для чиєїсь `опитування` призведе до повідомлення про помилку `HTTP 403 Forbidden` і
відповідь

```json
{
  "detail": "You can not create choice for this poll."
}
```

## Наступні кроки:

У наступному розділі ми розглянемо додавання тестів для нашого API та серіалізаторів. Ми також розглянемо, як
використовувати `flake8` і запустити наші тести в середовищі CI.
---

# Тестування та безперервне інтегрування

У цьому розділі ми додамо тест до нашого API.

DRF надає кілька важливих класів, які спрощують тестування API. Ми будемо використовувати ці класи пізніше в цьому
розділі наших тестів.

- `APIRequestFactory`: це схоже на RequestFactory Django. Це дозволяє створювати запити за допомогою будь-якого
  http-методу, який потім можна передавати будь-якому методу перегляду та порівнювати відповіді.
- `APIClient`: подібний до `клієнта` Django. Ви можете ОТРИМАТИ або ОПУБЛІКУВАТИ URL-адресу та перевірити відповіді.
- `APITestCase`: схоже на `TestCase` Django. Більшість ваших тестів буде підкласом цього.

Тепер давайте напишемо тестові приклади для нашої програми для опитування.

## Створення тестових запитів

Django's 'Requestfactory' має можливість створювати екземпляри запитів, які дозволяють нам окремо тестувати функції
перегляду. Django Rest Framework має клас під назвою 'APIRequestFactory', який розширює стандарт Django
'RequestFactory'. Цей клас містить майже всі дієслова http, такі як .get(), .post(), .put(), .patch() тощо.

Синтаксис запиту на публікацію:

```python
factory = APIRequestFactory()
request = factory.post(uri, post
data)
```

Додамо тест для списку опитувань.

```python
from rest_framework.test import APITestCase
from rest_framework.test import APIRequestFactory

from polls import apiviews


class TestPoll(APITestCase):
    def setUp(self):
        self.factory = APIRequestFactory()
        self.view = apiviews.PollViewSet.as_view({'get': 'list'})
        self.uri = '/polls/'

    def test_list(self):
        request = self.factory.get(self.uri)
        response = self.view(request)
        self.assertEqual(response.status_code, 200,
                         'Expected Response Code 200, received {0} instead.'
                         .format(response.status_code))
```

У наведених вище рядках коду ми намагаємося отримати доступ до подання PollList. Ми стверджуємо, що код відповіді HTTP
дорівнює 200.

Тепер запустіть тестову команду.

```shell
python manage.py test
```

І він відобразить наведене нижче повідомлення.

```shell
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_list (polls.tests.TestPoll)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/Users/shabda/repos/building-api-django/pollsapi/polls/tests.py", line 19, in test_list
    .format(response.status_code))
AssertionError: 401 != 200 : Expected Response Code 200, received 401 instead.

----------------------------------------------------------------------
Ran 1 test in 0.002s

FAILED (failures=1)
Destroying test database for alias 'default'...
```

Ой! Наш тест провалився. Це сталося тому, що перегляд недоступний без автентифікації. Тому нам потрібно створити
користувача та протестувати представлення після автентифікації.

## Тестування API з автентифікацією

Щоб перевірити apis із автентифікацією, потрібно створити тестового користувача, щоб ми могли надсилати запити в
контексті цього користувача. Давайте створимо тестового користувача. Змініть свої тести на

```python
from django.contrib.auth import get_user_model
from rest_framework.authtoken.models import Token


# ...

class TestPoll(APITestCase):
    def setUp(self):
        # ...
        self.user = self.setup_user()
        self.token = Token.objects.create(user=self.user)
        self.token.save()

    @staticmethod
    def setup_user():
        User = get_user_model()
        return User.objects.create_user(
            'test',
            email='testuser@test.com',
            password='test'
        )

    def test_list(self):
        request = self.factory.get(self.uri,
                                   HTTP_AUTHORIZATION='Token {}'.format(self.token.key))
        request.user = self.user
        response = self.view(request)
        self.assertEqual(response.status_code, 200,
                         'Expected Response Code 200, received {0} instead.'
                         .format(response.status_code))
```

Тепер запустіть тестову команду.

```shell
python manage.py test
```

Ви повинні отримати цю відповідь

```shell
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
.
----------------------------------------------------------------------
Ran 1 test in 0.119s

OK
Destroying test database for alias 'default'...
```

## Використання `APIClient`

Той самий тест можна написати за допомогою `APIClient`. У ньому є `get`, `.post` і family. На відміну від створення
запитів спочатку, за допомогою `APIClient` ви можете ОТРИМАТИ/GET або ОПУБЛІКУВАТИ/POST URL-адресу безпосередньо та
отримати відповідь.

Додайте такий тест:

```python
from rest_framework.test import APIClient


# ...


class TestPoll(APITestCase):
    def setUp(self):
        self.client = APIClient()
        # ...

    # ...
    def test_list2(self):
        response = self.client.get(self.uri)
        self.assertEqual(response.status_code, 200,
                         'Expected Response Code 200, received {0} instead.'
                         .format(response.status_code))
```

Let us test it now.

```shell
python manage.py test polls.tests.TestPoll


Creating test database for alias 'default'...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_list2 (polls.tests.TestPoll)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/Users/shabda/repos/building-api-django/pollsapi/polls/tests.py", line 37, in test_list2
    .format(response.status_code))
AssertionError: 401 != 200 : Expected Response Code 200, received 401 instead.

----------------------------------------------------------------------
Ran 1 test in 0.136s

FAILED (failures=1)
Destroying test database for alias 'default'...
```

Ми спостерігаємо той самий збій, який ми бачили в тесті з `APIRequestFactory`. Ви можете увійти в `APIClient`,
викликавши `APIClient.login`. Давайте оновимо тест.

```python
class TestPoll(APITestCase):
    # ...

    def test_list2(self):
        self.client.login(username="test", password="test")
        response = self.client.get(self.uri)
        self.assertEqual(response.status_code, 200,
                         'Expected Response Code 200, received {0} instead.'
                         .format(response.status_code))
```

```shell
python manage.py test polls.tests.TestPoll
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
.
----------------------------------------------------------------------
Ran 1 test in 0.260s

OK
Destroying test database for alias 'default'...
```

Вуаля! Тест успішно пройшов.

## `.post` та create

Тепер ми знаємо, як протестувати наші API GET. Цього разу ми можемо використовувати метод `APIClient` з `.post`.

Давайте спробуємо створити нове опитування, надіславши параметри «питання» та «created_by», які потрібні в методі POST.
Функція тесту виглядає наступним чином.

```python
class TestPoll(APITestCase):

    # ...
    def test_create(self):
        self.client.login(username="test", password="test")
        params = {
            "question": "How are you?",
            "created_by": 1
        }
        response = self.client.post(self.uri, params)
        self.assertEqual(response.status_code, 201,
                         'Expected Response Code 201, received {0} instead.'
                         .format(response.status_code))
```

Ми стверджуємо, що http-код 201, якщо тест пройшов успішно. Давайте запустимо тести.

```shell
python manage.py test polls.tests.TestPoll.test_create

Creating test database for alias 'default'...
System check identified no issues (0 silenced).
.
----------------------------------------------------------------------
Ran 1 test in 0.267s

OK
Destroying test database for alias 'default'...
```

Час святкувати з API :)

## Постійна інтеграція з CircleCI

У нас є тести, але ми також хочемо, щоб вони запускалися під час кожного коміту. Якщо ви використовуєте Github, CircleCI
надає дуже добре інтегровану службу для виконання ваших тестів. Ми будемо використовувати Circleci. v2

Ми можемо налаштувати нашу програму на використання Circle CI, додавши файл із назвою `.circleci/config.yml`, який є
текстовим файлом YAML (формат серіалізації даних, який читається людиною). Він автоматично визначає, коли було зроблено
фіксацію та відправлено в репозиторій Github, який використовує CircleCI, і кожного разу, коли це станеться, він спробує
створити проект і запустить тести. Розробник повідомляється про невдалу чи успішну збірку.

## Налаштування CircleCI

- Вхід: щоб розпочати роботу з Circle CI, ми можемо ввійти за допомогою нашого облікового запису github на Circleci.com.
- Активуйте вебхук Github: після завершення процесу реєстрації нам потрібно ввімкнути сервісний хук на сторінці профілю
  github.
- Додайте .circle/config.yml: ми повинні додати файл yml до проекту.

## Файл конфігурації кола запису

Для того, щоб Circle CI створив наш проект, нам потрібно трохи розповісти системі про нього. нам потрібно буде додати
файл із назвою `.circleci/config.yml` до кореня нашого сховища. Нам також потрібно створити
файл `pollsapi/requirements.txt`, щоб визначити наші залежності.

Додайте це до файлу `pollsapi/requirements.txt`

```text
Django==2.0.3
djangorestframework==3.7.7
```

А потім додайте це до `.circleci/config.yml`

```yaml
version: 2
jobs:
  build:
    docker:
      # specify the version you desire here
      - image: circleci/python:3.6.1


    working_directory: ~/repo

    steps:
      - checkout

      # Download and cache dependencies
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "pollsapi/requirements.txt" }}
            # fallback to using the latest cache if no exact match is found
            - v1-dependencies-

      - run:
          name: install dependencies
          command: |
            python3 -m venv venv
            . venv/bin/activate
            pip install -r pollsapi/requirements.txt

      - save_cache:
          paths:
            - ./venv
          key: v1-dependencies-{{ checksum "requirements.txt" }}

      - run:
          name: run tests
          command: |
            . venv/bin/activate
            cd pollsapi
            python manage.py test

      - store_artifacts:
          path: test-reports
          destination: test-reports
```

Нижче наведено важливі ключові слова, які використовуються під час написання файлу circleci config.yml.

- `image`: визначає базове зображення, включаючи мову та версію для використання
- `run`: вказує команду, яка буде виконана для налаштування середовища та запуску
  тестів. `pip install -r pollsapi/requirements.txt` налаштовує середовище, а `pip install -r pollsapi/requirements.txt`

якщо все пройшло успішно, ви повинні побачити зелену галочку

![](src/circleci.png)

Вітаємо, у вас працюють тести в середовищі CI.

Відтепер щоразу, коли ми надсилаємо наш код до нашого репозиторію, для нього буде створено нову збірку та запущено
тести.

Ми підійшли до кінця першої частини нашої книги. Ви можете прочитати додаток, який розповідає про деякі інструменти
документації та інструменти використання API. Ідіть вперед і створюйте чудові програми та API.

---

# Тестування та використання API з Postman

У цьому розділі ми дізнаємося, як використовувати програму Postman для тестування наших API.

Postman можна встановити з сайту [Postman](https://www.postman.com/) . Це універсальний інструмент для роботи з API.

У цих книгах ви будете створювати та використовувати API. Ми побачимо, як ми можемо використовувати Postman для цього.

## Створення HTTP запиту

Postman досить інтуїтивно зрозумілий, але зображення нижче має полегшити розуміння програми.

![](src/postman.png)

Є 4 ключові елементи для створення HTTP-запиту.

1. **URL**: Це вказує на яку URL-адресу потрібно зробити запит. Іншими словами, де знаходиться наша кінцева точка API.
2. **Метод**: Кожна кінцева точка API має метод, який служить її меті. Методами, наприклад, можуть бути GET для
   отримання деяких даних, POST для створення або оновлення, DELETE для видалення запису.
3. **Заголовки**: Заголовки надають необхідну інформацію про запит чи відповідь або про об’єкт, надісланий у тілі. Іноді
   ми також використовуємо заголовки автентифікації, щоб отримати доступ до кінцевої точки API.
4. **Тіло**: Тіло запиту – це місце, куди ми надсилаємо об’єкт. Об'єкт, який може знадобитися для послуги.

## Відповідь

Відповідь доступна в нижньому розділі, зазвичай у форматі JSON, але також може відрізнятися залежно від служби API.

## Колекції

Ми можемо зберігати всі відносні кінцеві точки API у колекціях. У нашому прикладі ми можемо зберегти всі кінцеві точки,
пов’язані з опитуваннями, як колекцію або всі кінцеві точки, пов’язані з користувачами, як іншу колекцію. Таким чином
організовано всі API.

## Аутентифікація

Postman також підтримує кілька механізмів автентифікації, таких як Basic Auth, Digest Auth і Oauth1. Це дозволяє нам
використовувати ці методи автентифікації для API.

---

# API документування (з Swagger тощо)

У цьому розділі ми побачимо, як задокументувати наш API.

Коли ви створюєте свій API, вам потрібно буде задокументувати API для співпраці з іншими людьми. У більшості компаній і
команд розробник, який використовує API, відрізняється від того, хто їх створює. Документація API та інструменти для
співпраці стають ще важливішими в такому середовищі.

Swagger — це інструмент, який використовується для розуміння можливостей сервісу без доступу до вихідного коду,
документації або перевірки мережевого трафіку. Простіше кажучи, за допомогою swagger ви можете побачити, які кінцеві
точки API доступні для веб-додатку. Ви можете використовувати swagger для тестування запитів і відповідей кінцевих точок
API.

DRF поставляється з власним інструментом, coreapi, для документування та взаємодії з API.

Ми будемо використовувати coreapi і swagger для документування нашого API.

## Додавання пишної документації

Встановіть django-rest-swagger

```shell
pip install django-rest-swagger
```

Оновіть свій `settings.py`

```python
INSTALLED_APPS = [
    # ...
    'polls',
    'rest_framework_swagger',
]
```

Додайте пихатості до своїх URL-адрес.

```python
from rest_framework_swagger.views import get_swagger_view

schema_view = get_swagger_view(title='Polls API')

# ...
urlpatterns = [
    # ...
    path(r'swagger-docs/', schema_view),
]
```

Перейдіть до */swagger-docs/* . І ваші пишні документи готові у всій своїй красі.

![](src/swagger.png)

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

## Використання coreapi для документації

### Використання coreapi для документації

## Використання coreapi для документації

Встановіть coreapi

```shell
pip install coreapi
```

Додайте URL-адреси coreapi до своїх URL-адрес.

```python
from rest_framework.documentation import include_docs_urls

# ...

urlpatterns = [
    # ...
    path(r'docs/', include_docs_urls(title='Polls API')),
]
```

І ваші документи coreapi готові у всій своїй красі.

![](src/coreapi.png)