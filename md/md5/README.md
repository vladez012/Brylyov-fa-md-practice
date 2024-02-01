
# Сервисы



### [Тест k Лекция: Сервисы, приемники сообщений и параллелизм](https://docs.google.com/forms/d/e/1FAIpQLSccJOlT0tiM2ZYrXseHF9L4tKYIyvNrZYzaUa8GjAJ5BapzCw/viewform)

### Практика: Создание фонового потока		
* [Видео](https://www.youtube.com/watch?v=lwTePPpVf-k)
### Практика: Управление интерфейсом через Handler
* [Видео](https://www.youtube.com/watch?v=OqsJInROJOk)
### Практика: Жизненный цикл сервиса


Цель работы

    Познакомиться с жизненным циклом связанного и свободного сервиса в ОС Android, увидеть на практике порядок вызова методов жизненного цикла.
## Задания для выполнения
Создайте в приложении сервис, переопределив все основные методы жизненного цикла. Каждый метод должен выводить в консоль свое название при вызове.

Не забудьте вызов методов суперкласса и объявление сервиса в манифесте приложения.

В основной активности создайте две конопки. При нажатии на первую интент, вызывающий созданный сервис (явный интент) рассылается методом startService(), при нажатии второй - методом bindService().

Запустите приложение и понаблюдайте за жизненным циклом сервиса.

## Контрольные вопросы
Когда происходит создание и удаление связанного сервиса?

Какие методы жизненного цикла вызываются у сервиса и в какой последовательности?

Как соотносится ЖЦ активности и сервиса?

## Дополнительные задания
Добавьте в сервис полезное фоновое действие, которое выполняется продолжительное время. Как изменилось поведение сервиса?

Добавьте возможность из клиента (активности) убить сервис.

Добавьте логирование методов жизненного цикла активности. Пронаблюдайте за ней. 

### Практика: Возврат данных через Pending Intent	
* [Видео](https://www.youtube.com/watch?v=MO-9VbPsCmk)
### Практика: Работа с сервисами

Цель работы

    Познакомится с сервисами Android Studio и научиться создавать приложения принимающие и отправляющие сообщения.
## Задания для выполнения
Создайте проигрыватель PlayService.java для воспроизведения и остановки одной песни.
## Методические указания
На примере создания проигрывателя в Android Studio  разберемся как работают службы (сервисы).

Службы (Сервисы) в Android работают как фоновые процессы и представлены классом android.app.Service. Они не имеют пользовательского интерфейса и нужны в тех случаях, когда не требуется вмешательства пользователя. Сервисы работают в фоновом режиме, выполняя сетевые запросы к веб-серверу, обрабатывая информацию, запуская уведомления и т.д. Служба может быть запущена и будет продолжать работать до тех пор, пока кто-нибудь не остановит её или пока она не остановит себя сама.

Сервисы предназначены для длительного существования, в отличие от активностей. Они могут работать, постоянно перезапускаясь, выполняя постоянные задачи или выполняя задачи, требующие много времени.

Android даёт службам более высокий приоритет, чем бездействующим активностям, поэтому вероятность того, что они будут завершены из-за нехватки ресурсов, заметно уменьшается. По сути, если система должна преждевременно завершить работу запущенного сервиса, он может быть настроен таким образом, чтобы запускаться повторно, как только станет доступно достаточное количество ресурсов. В крайних случаях прекращение работы сервиса (например, задержка при проигрывании музыки) будет заметно влиять на впечатления пользователя от приложения, и в подобных ситуациях приоритет сервиса может быть повышен до уровня активности, работающей на переднем плане.

Чтобы определить службу, необходимо создать новый класс, расширяющий базовый класс Service. Можно воспользоваться готовым мастером создания класса для сервиса в Android Studio. Щёлкаем правой кнопкой мыши на папке java (или на имени пакета) и выбираем New | Service | Service:

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image2.png "image4")

В следующем окне выбираем имя сервиса (флажки оставляем) и нажимаем кнопку Finish.

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image1.png "image4")

Получим заготовку.
```java
package ru.alexanderklimov.service;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;

public class MyService extends Service {
    public MyService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.
        throw new UnsupportedOperationException("Not yet implemented");
    }
}
```

При этом сервис автоматически зарегистрируется в манифесте в секции <application>.
```
<service
    android:name=".MyService"
    android:enabled="true"
    android:exported="true" >
</service>
```

Если бы мы убрали флажки на экране мастера, то оба атрибута имели бы значение false. Например, атрибут exported даёт возможность другим приложениям получить доступ к вашему сервису.

Имеются и другие атрибуты, например, permission, чтобы сервис запускался только вашим приложением.
Также вы можете обойтись без мастера и создать вручную класс сервиса и запись в манифесте, теперь вы знаете, из чего он состоит.
Подобно активностям служба имеет свои методы жизненного цикла:

    onCreate()
    onStartCommand()
    onDestroy()

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image4.png "image4")

Для быстрого создания заготовок нужных методов используйте команду меню Code | Override Methods... или набирайте сразу имя метода, используя автодополнение.

Чтобы создать службу PlayService можно воспользоваться мастером или создать класс  сервиса вручную. Опишите его функционал:

```java
package com.example.myapplication;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.IBinder;

import android.widget.Toast;

public class PlayService extends Service {

    private MediaPlayer mPlayer;


    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        Toast.makeText(this, "Служба создана",
                Toast.LENGTH_SHORT).show();
        mPlayer = MediaPlayer.create(this, R.raw.flower_romashka);
        mPlayer.setLooping(false);
    }

  
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Toast.makeText(this, "Служба запущена",
                Toast.LENGTH_SHORT).show();
        mPlayer.start();
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Toast.makeText(this, "Служба остановлена",
                Toast.LENGTH_SHORT).show();
        mPlayer.stop();
    }
}
```

Зарегистрируем службу в файле манифеста.

```
<service 
    android:enabled="true" 
    android:name=".PlayService"> 
</service> 
```

В файле разметки для активности определим две кнопки: Старт и Стоп:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <Button
        android:id="@+id/button_start"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Старт" />

    <Button
        android:id="@+id/button_stop"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Стоп" />
</LinearLayout>
```

В классе активности в обработчиках событий кнопок будем вызывать методы startService() и stopService() для управления службой.
```java
package com.example.myapplication;

import static android.app.Service.START_FLAG_RETRY;

import androidx.appcompat.app.AppCompatActivity;

import android.app.Service;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button btnStart = findViewById(R.id.button_start);
        final Button btnStop = findViewById(R.id.button_stop);

        // запуск службы
        btnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // используем явный вызов службы
                startService(
                        new Intent(MainActivity.this, PlayService.class));
            }
        });

        // остановка службы
        btnStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                stopService(
                        new Intent(MainActivity.this, PlayService.class));
            }
        });
    }
}
```

Чтобы воспроизводить аудио, MediaPlayer должен знать, какой именно ресурс (файл) нужно производить. Установить нужный ресурс для воспроизведения можно тремя способами:
- в метод create() объекта MediaPlayer передается id ресурса, представляющего аудиофайл
- в метод create() объекта MediaPlayer передается объект Uri, представляющего аудиофайл
- в метод setDataSource() объекта MediaPlayer передается полный путь к аудиофайлу

После установки ресурса вызывается метод prepare() или prepareAsync() (асинхронный вариант prepare()). Этот метод подготавливает аудиофайл к воспроизведению, извлекая из него первые секунды. Если мы воспроизводим файл из сети, то лучше использовать prepareAsync().

Для управления воспроизведением в классе MediaPlayer определены следующие методы:

- start(): запускает аудио
- pause(): приостанавливает воспроизведение
- stop(): полностью останавливает воспроизведение

Итак, создадим новый проект. Аудиофайл должен находиться в папке res/raw, поэтому добавим в проект в Android Studio такую папку. Для этого нажмем на папку res правой кнопкой мыши и в появившемся меню выберем New -> Android Resource Directory:

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image3.png "image4")

Затем в появившемся окне в качестве типа папки укажем raw (что также будет использоваться в качестве названия папки):

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image6.png "image4")

И скопируем в нее какой-нибудь аудио-файл, предварительно открыв папку в файловом менеджере.
![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image5.png "image4")


![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image8.png "image4")

Запустите приложение, прослушайте музыку. Обратите внимание, что когда приложение сворачивается, музыка продолжает играть.

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/1image7.jpg "image4")

## Дополнительные задания
Создайте проигрыватель PlayService.java для воспроизведения списка песен из плей-листа.


Материалы
http://developer.alexanderklimov.ru/android/notification.php
http://developer.alexanderklimov.ru/android/toast.php
http://developer.alexanderklimov.ru/android/theory/services-theory.php
https://metanit.com/java/android/11.2.php
http://developer.alexanderklimov.ru/android/broadcast.php
https://developer.android.com/about/versions/oreo/background.html



### Практика: Работа с широковещательными сообщениями
Цель работы

    Познакомится с сервисами Android Studio и научиться создавать приложения принимающие и отправляющие сообщения.
## Задания для выполнения
Создайте приложение, которое будет отправлять и принимать сообщения.
##Методические указания
Создайте новый проект и разместите на экране кнопку с надписью "Отправить сообщение". Присвойте атрибуту onClick название метода, в котором будет происходит отправка широковещательного сообщения.
```java
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Отправить сообщение"
    android:id="@+id/button"
    android:layout_gravity="center_horizontal"
    android:onClick="sendMessage" />
```

В классе активности создаём уникальную строку и реализуем метод для щелчка кнопки. Также добавим дополнительные данные - первую часть послания радистки.
```java
public static final String WHERE_MY_CAT_ACTION = "ru.alexanderklimov.action.CAT";
public static final String ALARM_MESSAGE = "Срочно пришлите кота!";

public void sendMessage(View view) {
    Intent intent = new Intent();
    intent.setAction(WHERE_MY_CAT_ACTION);
    intent.putExtra("ru.alexanderklimov.broadcast.Message", ALARM_MESSAGE);
    intent.addFlags(Intent.FLAG_INCLUDE_STOPPED_PACKAGES);
    sendBroadcast(intent);
}
```

Запустив пример, вы можете нажать на кнопку и отправлять сообщение. Только ваше сообщение уйдёт в никуда, так как ни одно приложение не оборудовано приёмником для него.
 Исправим ситуацию и создадим приёмник в своём приложении.
  Мы будем сами принимать свои же сообщения.

Приёмник представляет собой обычный Java-класс на основе BroadcastReceiver. Вы можете создать вручную класс и наполнить его необходимыми методами. Раньше так и поступали. Но в студии есть готовый шаблон, который поможет немного сэкономить время.

Щёлкаем правой кнопкой мыши на названии пакета и выбираем New | Other | Broadcast Receiver

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/image3.png "image4")

В диалоговом окне задаём имя приёмника, остальные настройки оставляем без изменений.

![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/image1.png "image4")

Студия создаст изменения в двух местах. Во-первых, будет создан класс MessageReceiver:

```java
package ru.alexanderklimov.testapplication;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;

public class MessageReceiver extends BroadcastReceiver {
    public MessageReceiver() {
    }

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        throw new UnsupportedOperationException("Not yet implemented");
    }
}
```

Во-вторых, в манифесте будет добавлен новый блок.

```java
<receiver
    android:name=".MessageReceiver"
    android:enabled="true"
    android:exported="true" >
</receiver>
```

В него следует добавить фильтр, по которому он будет ловить сообщения.

```java
<receiver
    android:name=".MessageReceiver"
    android:enabled="true"
    android:exported="true">
    <intent-filter>
        <action android:name="ru.alexanderklimov.action.CAT" />
    </intent-filter>
</receiver>
```

Вернёмся в класс приёмника и модифицируем метод onReceive().

```java
@Override
public void onReceive(Context context, Intent intent) {
    Toast.makeText(context, "Обнаружено сообщение: " +
                    intent.getStringExtra("ru.alexanderklimov.broadcast.Message"),
            Toast.LENGTH_LONG).show();
}
```
Снова запустим пример и ещё раз отправим сообщение. Так как наше приложение теперь оборудовано не только передатчиком, но и приёмником, то оно должно уловить сообщение и показать его нам.

Если приложение работает не корректно, необходимо реализовать следующие изменения.

Когда приложение запускается в фоновом режиме, оно потребляет некоторые ограниченные ресурсы устройства, такие как оперативная память. Это может привести к ухудшению работы пользователя, особенно если пользователь использует ресурсоемкое приложение, такое как игра или просмотр видео.

 Чтобы улучшить пользовательский интерфейс, Android 8.0 (уровень API 26) накладывает ограничения на то, что приложения могут делать во время работы в фоновом режиме.
 
 ![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/image2.png "image4")

  В этом скриншоте приводятся изменения в коде приложения, чтобы оно хорошо работало в соответствии с новыми ограничениями.



Материалы
http://developer.alexanderklimov.ru/android/notification.php
http://developer.alexanderklimov.ru/android/toast.php
http://developer.alexanderklimov.ru/android/theory/services-theory.php
https://metanit.com/java/android/11.2.php
http://developer.alexanderklimov.ru/android/broadcast.php
https://developer.android.com/about/versions/oreo/background.html


### Работа с уведомлениями
Цель работы

    Познакомиться с приемами работы с уведомлениями, из связи с сервисами и отложенными намерениями.
## Задания для выполнения
Создайте в приложении активность, порождающую сервис.

В сервисе создайте уведомление. При нажатии на кнопку в активности уведомление должно показываться.

Сделайте сервис сервисом переднего плана.

Модифицируйте уведомление таким образом, чтобы при нажатии на него показывалась новая активность.

Добавьте в уведомление две кнопки. При нажатии на них должны показываться две разные активности.

## Контрольные вопросы
Зачем нужны уведомления?

Как работают сервисы переднего плана?

Что такое отложенные намерения?

## Дополнительные задания
Добавьте в уведомления графические элементы - иконку приложения и контакта.

Сделайте кликер, но таким образом, чтобы количество нажатий отображалось в уведомлении.

Сделайте приложение заметок, в котором можно создать заметку из постоянного уведомления (вводя текст прямо в нем). Заметки должны храниться в файле настроек и демонстрироваться в активности в виде списка.


###  Практика :Всплывающие уведомления
Цель работы

    Познакомится с сервисами Android Studio и научиться создавать приложения принимающие и отправляющие сообщения.
## Задания для выполнения
Создайте кнопку, которая будет выводить всплывающее сообщение на экран при нажатии с помощью объекта Toast.
## Методические указания
Создание Toast-сообщения

Всплывающее уведомление (Toast Notification) является сообщением, которое появляется на поверхности окна приложения, заполняя необходимое ему количество пространства, требуемого для сообщения. При этом текущая деятельность приложения остаётся работоспособной для пользователя. В течение нескольких секунд сообщение плавно закрывается. Всплывающее уведомление также может быть создано службой, работающей в фоновом режиме. Как правило, всплывающее уведомление используется для показа коротких текстовых сообщений.

Для создания всплывающего уведомления необходимо инициализировать объект Toast при помощи метода Toast.makeText(), а затем вызвать метод show() для отображения сообщения на экране:
```
Toast toast = Toast.makeText(getApplicationContext(), 
   "Текстовое сообщение", Toast.LENGTH_SHORT); 
toast.show(); 
```
У метода makeText() есть три параметра:
- Контекст приложения
- Текстовое сообщение
- Продолжительность времени показа уведомления. Можно использовать только две константы

Уведомления выводятся на 3 с половиной секунды или на 2 секунды.


![image4](https://github.com/VladimirAndropov/fa-md-practice/raw/main/md/md5/images/image001.jpg "image4")

По умолчанию стандартное всплывающее уведомление появляется в нижней части экрана. Изменить место появления уведомления можно с помощью метода setGravity(int, int, int). Метод принимает три параметра:
- стандартная константа для размещения объекта в пределах большего контейнера (например, GRAVITY.CENTER, GRAVITY.TOP и др.);
- смещение по оси X
- смещение по оси Y

Например, если вы хотите, чтобы уведомление появилось в центре экрана, то используйте следующий код (до вызова метода show()):
    
    toast.setGravity(Gravity.CENTER, 0, 0); 

Для вывода в левом верхнем углу.

    toast.setGravity(Gravity.TOP or Gravity.LEFT, 0, 0)

Если нужно сместить уведомление направо, то просто увеличьте значение второго параметра. Для смещения вниз нужно увеличить значение последнего параметра. Соответственно, для смещения вверх и влево используйте отрицательные значения.


## Контрольные вопросы
Чем сервисы отличаются от Activity?

Возможно ли в Toast Notification разместить LinearLayout?

Сколько времени отображается всплывшее сообщение созданное с помощью  объекта Toast?

## Дополнительные задания
Создайте кнопку, которая будет выводить всплывающую панель с картинкой и текстом на экран при нажатии с помощью объекта Toast.

Создайте проигрыватель PlayService.java для воспроизведения списка песен из плей-листа.

Материалы
http://developer.alexanderklimov.ru/android/notification.php
http://developer.alexanderklimov.ru/android/toast.php
http://developer.alexanderklimov.ru/android/theory/services-theory.php
https://metanit.com/java/android/11.2.php
http://developer.alexanderklimov.ru/android/broadcast.php
https://developer.android.com/about/versions/oreo/background.html








