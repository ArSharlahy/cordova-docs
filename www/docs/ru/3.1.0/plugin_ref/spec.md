---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

title: Спецификация расширений
---

# Спецификация расширений

Файл `plugin.xml` представляет собой документ XML c пространством имен `plugins`: `http://apache.org/cordova/ns/plugins/1.0`. Он содержит узел верхнего уровня `plugin`, который определяет сам плагин, и дочерние узлы, которые определяют структуру плагина.

Простой пример элемента plugin:

    <?xml version="1.0" encoding="UTF-8"?>
    <plugin xmlns="http://apache.org/cordova/ns/plugins/1.0"
        xmlns:android="http://schemas.android.com/apk/res/android"
        id="com.alunny.foo"
        version="1.0.2">
    

## элемент `< plugin >`

Элементом `plugin` является элементом верхнего уровня. Он имеет следующие атрибуты:

*   `xmlns`(обязательно): пространство имен плагин, `http://apache.org/cordova/ns/plugins/1.0` . Если документ содержит XML из другого пространства имен, такие как теги для добавления `AndroidManifest.xml` файл, эти пространства имен также должны быть включены в элемент верхнего уровня.

*   `id`(обязательно): реверс домена стиль идентификатор для плагина, такие как`com.alunny.foo`

*   `version`(обязательно): номер версии для плагина, который соответствует следующее регулярное выражение майор минор патч стиль:
    
        ^\d+[.]\d+[.]\d+$
        

## элементы `< engines >` и `< engine >`

Дочерние элементы `<engines>` элемент указать версии на основе Apache Cordova рамок, которые поддерживает этот плагин. Пример:

    <engines>
        <engine name="cordova" version="1.7.0" />
        <engine name="cordova" version="1.8.1" />
        <engine name="worklight" version="1.0.0" platform="android" scriptSrc="worklight_version"/>
    </engines>
    

Похож на `<plugin>` элемента `version` атрибут, указанной версии строка должна соответствовать строка майор минор патч, соответствует регулярное выражение:

        ^\d+[.]\d+[.]\d+$
    

Элементы двигателя также могут указать нечетких матчей, чтобы избежать повторения и по сокращению обслуживания, когда обновляется базовой платформы. Инструменты следует поддерживать как минимум `>` , `>=` , `<` и `<=` , например:

    <engines>
        <engine name="cordova" version=">=1.7.0" />
        <engine name="cordova" version="<1.8.1" />
    </engines>
    

'<engine>' теги также имеет поддержку по умолчанию для всех основных платформ, Кордова существует на. Указав тег двигателя «cordova» означает, что все версии Cordova на любой платформе должны удовлетворить атрибут версии двигателя. Для того, чтобы переопределить обработчик catch-all 'cordova', может перечислить конкретные платформы и их версии:

    <engines>
        <engine name="cordova" version=">=1.7.0" />
        <engine name="cordova-android" version=">=1.8.0" />
        <engine name="cordova-ios" version=">=1.7.1" />
    </engines>
    

Вот список по умолчанию двигателей, '<engine>' тег поддерживает: * «cordova» * «cordova-plugman» * «cordova андроид» * «cordova-ios» * «cordova-blackberry10» * «cordova-wp7» * «cordova-wp8» * «cordova-windows8»

Указание пользовательских рамок на основе Apache Cordova должны быть перечислены под двигатель тег следующим образом:

    <engines>
        <engine name="my_custom_framework" version="1.0.0" platform="android" scriptSrc="path_to_my_custom_framework_version"/>
        <engine name="another_framework" version=">0.2.0" platform="ios|android" scriptSrc="path_to_another_framework_version"/>
        <engine name="even_more_framework" version=">=2.2.0" platform="*" scriptSrc="path_to_even_more_framework_version"/>
    </engines>
    

Пользовательские на основе Apache Cordova framework требует, что элемент двигателя включает в себя следующие атрибуты: «имя», «версия», «scriptSrc» и «платформа».

*   `name`(обязательно): понятное имя для вашей пользовательской основы.

*   `version`(обязательно): версия, чтобы установить должны иметь ваши рамки.

*   `scriptSrc`(обязательно): файл сценария, который говорит plugman, какая версия пользовательской базы. В идеале этот файл должен быть в каталоге верхнего уровня плагин каталога.

*   `platform`(обязательно): какие платформы, которые поддерживает ваш рамки. Вы можете использовать подстановочный знак ' *' сказать поддерживается для всех платформ, укажите несколько с символом как «android|ios|blackberry10» или просто одной платформы, как «андроид».

plugman прерывает с ненулевой код для любой плагин, чьи целевой проект не соответствует двигателя ограничений.

Если не `<engine>` указаны теги, plugman пытается установить в каталог проекта указанного cordova слепо.

## `<name>`элемент

Понятное имя для плагина, содержание которых текст содержит имя плагина. Например:

    <name>Foo</name>
    

Этот элемент не (пока) обрабатывать локализации.

## `<description>`элемент

Немашинное описание для плагина. Текстовое содержимое элемента содержит описание плагина. Пример:

    <description>Foo plugin description</description>
    

Этот элемент не (пока) обрабатывать локализации.

## `<author>`элемент

Имя автора плагина. Текстовое содержимое элемента содержит имя автора плагина. Пример:

    <author>Foo plugin description</author>
    

## `<keywords>`элемент

Плагин ключевые слова. Текстовое содержимое элемента содержит запятую ключевые слова для описания плагина. Пример:

    <keywords>foo,bar</keywords>
    

## `<license>`элемент

Плагин лицензия. Текстовое содержимое элемента содержит плагин лицензию. Пример:

    <license>Apache 2.0 License</license>
    

## `<asset>`элемент

Один или несколько элементов перечисления файлов или каталогов копируется в приложение Cordova `www` каталог. Примеры:

    <!-- a single file, to be copied in the root directory -->
    <asset src="www/foo.js" target="foo.js" />
    <!-- a directory, also to be copied in the root directory -->
    <asset src="www/foo" target="foo" />
    

Все `<asset>` теги требуют оба `src` и `target` атрибуты. Веб только плагины содержит в основном `<asset>` элементов. Любые `<asset>` элементы, вложенные в `<platform>` элементы определяют web платформа специфического активов, как описано ниже. Атрибуты включают в себя:

*   `src`(обязательно): файл или каталог, где расположен в плагина пакет, относительно `plugin.xml` документ. Если файл не существует в указанном `src` расположение, plugman останавливается и отменяет процесс установки, выдает уведомление о конфликте и выходит с ненулевой код.

*   `target`(обязательно):
    
    Файл или каталог, должны располагаться в Cordova app, относительно `www` каталог. Активы могут быть направлены в подкаталоги, например:
    
    <asset src="www/new-foo.js" target="js/experimental/foo.js" />
    
    создает `js/experimental` каталогов в пределах `www` каталог, если только уже присутствует, то копии `new-foo.js` файл и переименовывает его `foo.js` . Если файл уже существует в целевом расположении, plugman останавливается и отменяет процесс установки, выдает уведомление о конфликте и выходит с ненулевой код.

## `<js-module>`элемент

Большинство плагинов включают один или несколько файлов JavaScript. Каждый `<js-module>` тег соответствует файл JavaScript и предотвращает пользователей плагина для добавления `<script>` тег для каждого файла. В то время как `<asset>` теги просто скопировать файл из подкаталога плагин в `www` , `<js-module>` теги являются гораздо более сложными. Они выглядят так:

    <js-module src="socket.js" name="Socket">
        <clobbers target="chrome.socket" />
    </js-module>
    

При установке плагина с в примере выше, `socket.js` копируется в `www/plugins/my.plugin.id/socket.js` и добавлены в качестве записи для `www/cordova_plugins.js` . Во время загрузки, код в `cordova.js` использует XHR для считывания каждого файла и придать `<script>` тег в HTML. Он добавляет сопоставление избить или объединить в соответствующих случаях, как описано ниже.

*Не* обернуть файл с `cordova.define` , так как он добавляется автоматически. Модуль упаковывается в закрытия, с `module` , `exports` , и `require` в области, как это нормально для AMD модулей.

Подробная информация для `<js-module>` тега:

*   `src`Ссылается на файл в директорию плагинов относительно `plugin.xml` файл.

*   `name`Предоставляет последнюю часть имя модуля. Как правило, может быть, все, что вам нравится, и это только важно, если вы хотите использовать `cordova.require` для импорта других частей ваших плагинов в коде JavaScript. Имя модуля для `<js-module>` это ваш плагин `id` следуют значение `name` . Для примера выше с `id` из `chrome.socket` , это имя модуля`chrome.socket.Socket`.

*   Три теги разрешены в `<js-module>` :
    
    *   `<clobbers target="some.value"/>`Указывает, что `module.exports` вставляется в `window` объект как `window.some.value` . Вы можете иметь столько `<clobbers>` как вам нравится. Любой объект, не доступны на `window` создан.
    
    *   `<merges target="some.value"/>`Указывает, что модуль должны быть объединены с любое существующее значение в `window.some.value` . Если любой ключ уже существует, версия модуля переопределяет оригинала. Вы можете иметь столько `<merges>` как вам нравится. Любой объект, не доступны на `window` создан.
    
    *   `<runs/>`означает, что ваш код должен быть указан с `cordova.require` , но не установлен на `window` объект. Это полезно при инициализации модуля, присоединения обработчиков событий или иным образом. Вы можете иметь только до одного `<runs/>` тег. Обратите внимание, что в том числе `<runs/>` с `<clobbers/>` или `<merges/>` также является излишним, так как они `cordova.require` свой модуль.
    
    *   Пустой `<js-module>` еще загружает и может быть acccessed в других модулях через`cordova.require`.

Если `src` не разрешить существующий файл, plugman останавливается и отменяет установку, выдает уведомление о проблеме и выходит с ненулевой код.

Вложение `<js-module>` элементы внутри `<platform>` объявляет платформы JavaScript модуль привязки.

## `<dependency>`

`<dependency>`Позволяет вам указать другие плагины, от которых зависит текущий плагин. В то время как будущих версий будет доступ к ним из репозиториев плагин, в краткосрочной перспективе плагины прямо упоминается как URL по `<dependency>` теги. Они отформатированы следующим образом:

    <dependency id="com.plugin.id" url="https://github.com/myuser/someplugin" commit="428931ada3891801" subdir="some/path/here" />
    

*   `id`: предоставляет идентификатор плагина. Он должен быть глобально уникальным и выраженной в стиле реверс домена. Хотя ни один из этих ограничений в настоящее время применяются, они могут быть в будущем.

*   `url`: URL-адрес для плагина. Это должно указывать репозиторий git, который plugman пытается клонировать.

*   `commit`: Это любая ссылка git, понятны `git checkout` : ответвления или метки имя (например, `master` , `0.3.1` ), или фиксации хэш (например,`975ddb228af811dd8bb37ed1dfd092a3d05295f9`).

*   `subdir`: Указывает, что целевой плагин зависимостей существует как подкаталог git-репозиторий. Это полезно, потому что она позволяет репозиторий содержит несколько связанных плагинов, указан каждый индивидуально.

В будущем будут введены ограничения версии, и плагин хранилище будет существовать для поддержки выборки по имени вместо явного URL-адресов.

### Зависимости в относительные пути

Если задать `url` из `<dependency>` тег для `"."` и `subdir` , зависимыми плагин установлен из того же местного или удаленного репозитория как родитель плагин, указывающее `<dependency>` тег.

Обратите внимание, что `subdir` всегда указывает путь относительно *корня* git-репозиторий, не родитель плагин. Это верно, даже если вы установили плагин с локальный путь непосредственно к нему. Plugman находит корень репозитория git, а затем находит другой плагин от там.

## `<platform>`

`<platform>`Тег определяет платформ, которые имеют связанные машинный код или требуют изменения их конфигурации файлов. Инструменты, с помощью этой спецификации можно определить поддерживаемые платформы и установить код в Cordova проекты.

Плагины без `<platform>` предполагается, что теги являются только JavaScript и поэтому устанавливаемый на любых платформах.

Образец платформы тег:

    <platform name="android">
        <!-- android-specific elements -->
    </platform>
    <platform name="ios">
        <!-- ios-specific elements -->
    </platform>
    

Необходимые `name` атрибут определяет платформу как поддерживается, связав элемент детей с этой платформы.

Имена платформ должны быть в нижнем регистре. Перечислены имена платформ, как произвольно выбрали:

*   андроид
*   bb10
*   iOS
*   WP7
*   РГ.8

## `<source-file>`

`<source-file>`Элемент определяет исполняемый файл исходного кода, который должен быть установлен в проект. Примеры:

    <!-- android -->
    <source-file src="src/android/Foo.java"
                    target-dir="src/com/alunny/foo" />
    <!-- ios -->
    <source-file src="src/ios/CDVFoo.m" />
    <source-file src="src/ios/someLib.a" framework="true" />
    <source-file src="src/ios/someLib.a" compiler-flags="-fno-objc-arc" />
    

Он поддерживает следующие атрибуты:

*   `src`(обязательно): расположение файла относительно `plugin.xml` . Если `src` не удается найти файл, plugman останавливается и отменяет установку, выдает уведомление об этой проблеме и выходит с ненулевой код.

*   `target-dir`: Каталог, в который должны быть скопированы файлы, относительно корня проекта Cordova. На практике, это наиболее важно для платформ на базе Java, где файл в `com.alunny.foo` пакет должен находиться в `com/alunny/foo` каталог. Для платформ, где исходный каталог не имеет значения этот атрибут должен быть опущен.
    
    Как и в случае с активами, если `target` из `source-file` будет перезаписать существующий файл, plugman останавливается и отменяет установку, выдает уведомление об этой проблеме и выходит с ненулевой код.

*   `framework`(только для iOS-устройств): Если значение `true` , также добавляет указанный файл в качестве основы в проект.

*   `compiler-flags`(только для iOS-устройств): Если установлено, присваивает указанный компилятор флаги для конкретного исходного файла.

## `<config-file>`

Идентифицирует XML файл конфигурации будет изменен, где в этом документе модификация должна происходить, и что следует изменить.

Два типы файлов, которые были протестированы для модификации с этим элементом, `xml` и `plist` файлов.

`config-file`Элемент позволяет добавить новых детей в XML-дерево документа. Дети, XML-литералы должны быть вставлены в целевом документе.

Пример для XML:

    <config-file target="AndroidManifest.xml" parent="/manifest/application">
        <activity android:name="com.foo.Foo" android:label="@string/app_name">
            <intent-filter>
            </intent-filter>
        </activity>
    </config-file>
    

Пример для `plist` :

    <config-file target="*-Info.plist" parent="CFBundleURLTypes">
        <array>
            <dict>
                <key>PackageName</key>
                <string>$PACKAGE_NAME</string>
            </dict>
        </array>
    </config-file>
    

Он поддерживает следующие атрибуты:

*   `target`:
    
    Файл будет изменен и путь относительно корня проекта Cordova.
    
    Целевой объект может включать подстановочный знак ( `*` ) элементов. В этом случае plugman рекурсивно просматривает структуру каталогов проекта и использует первый матч.
    
    На iOS, расположение файлов конфигурации относительно корневого каталога проекта не известна, поэтому Указание приёмника из `config.xml` разрешается в`cordova-ios-project/MyAppName/config.xml`.
    
    Если указанный файл не существует, инструмент игнорирует изменения конфигурации и продолжает установку.

*   `parent`: Селектор XPath, ссылки на родительских элементов для добавления в файл config. Если вы используете абсолютные селекторов, можно использовать подстановочный знак ( `*` ) для указания корневого элемента, например,`/*/plugins`.
    
    Для `plist` файлов, `parent` определяет, под какие родительского ключа следует включить указанные XML-данные.
    
    Если селектор не разрешить ребенку указанного документа, остановки инструмента и обратный процесс установки выдает предупреждение и выходит с ненулевой код.

## `<plugins-plist>`

Это *устаревший* , как он применяется только к cordova-ios 2.2.0 и ниже. Использование `<config-file>` тег для новых версий Cordova.

Пример:

    <config-file target="config.xml" parent="/widget/plugins">
        <feature name="ChildBrowser">
            <param name="ios-package" value="ChildBrowserCommand"/>
        </feature>
    </config-file>
    

Указывает ключ и значение для добавления к правильной `AppInfo.plist` файл в проекте Cordova iOS. Например:

    <plugins-plist key="Foo" string="CDVFoo" />
    

## `<resource-file>`и`<header-file>`

Как исходные файлы, но специально для платформ, таких как iOS, которые отличают между исходные файлы, заголовками и ресурсами. Примеры:

    <resource-file src="CDVFoo.bundle" />
    <resource-file src="CDVFooViewController.xib" />
    <header-file src="CDVFoo.h" />
    

## `<lib-file>`

Как источник, ресурсов и файлы заголовка, но специально для платформ, таких как BlackBerry 10, использующих пользователями библиотеки. Примеры:

    <lib-file src="src/BlackBerry10/native/device/libfoo.so" arch="device" />
    <lib-file src="src/BlackBerry10/native/simulator/libfoo.so" arch="simulator" />
    

Поддерживаемые атрибуты:

*   `src`(обязательно): расположение файла относительно `plugin.xml` . Если `src` не может быть найдено, plugman останавливается и отменяет установку, выдает предупреждение о проблеме и выходит с ненулевой код.

*   `arch`: Архитектура для которого `.so` файл был построен, либо `device` или`simulator`.

## `<framework>`

Определяет рамки (обычно часть платформы OS) на которых зависит плагин.

Примеры:

    <framework src="libsqlite3.dylib" />
    <framework src="social.framework" weak="true" />
    

`src`Атрибут определяет рамки, в которых plugman пытается добавить в Кордове проект в правильную моды для данной платформы.

Необязательный `weak` атрибут – это логическое значение, указывающее, ли рамок должна быть слабо связаны. Значение по умолчанию`false`.

## `<info>`

Дополнительная информация для пользователей. Это полезно, когда требуется дополнительные шаги, которые не могут быть автоматизированы легко или plugman в рамки. Примеры:

    <info>
    You need to install __Google Play Services__ from the `Android Extras` section using the Android SDK manager (run `android`).
    
    You need to add the following line to your `local.properties`
    
    android.library.reference.1=PATH_TO_ANDROID_SDK/sdk/extras/google/google_play_services/libproject/google-play-services_lib
    </info>
    

# Переменные

В некоторых случаях плагин может потребоваться внести изменения в конфигурацию зависит от целевого приложения. Например, чтобы зарегистрироваться для C2DM на Android, app, чей идентификатор пакета `com.alunny.message` потребует разрешения, такие как:

    <uses-permission
    android:name="com.alunny.message.permission.C2D_MESSAGE"/>
    

В таких случаях, когда содержание вставлены из `plugin.xml` файл не известно заранее, переменные можно указать знак доллара, последовала серия заглавными буквами, цифрами или знаками подчеркивания. Для приведенного выше примера `plugin.xml` файл будет включать этот тег:

    <uses-permission
    android:name="$PACKAGE_NAME.permission.C2D_MESSAGE"/>
    

plugman заменяет ссылки на переменные с указанным значением, или пустая строка, если не найден. Значение переменной ссылки могут быть обнаружены (в данном случае, от `AndroidManifest.xml` файл) или указанного пользователем инструмент; точный процесс зависит от конкретного инструмента.

plugman может запросить пользователям указывать необходимые переменные плагин. Например можно указать ключи API для C2M и карты Google как аргумент командной строки:

    plugman --platform android --project /path/to/project --plugin name|git-url|path --variable API_KEY=!@CFATGWE%^WGSFDGSDFW$%^#$%YTHGsdfhsfhyer56734
    

Чтобы сделать переменную обязательным, `<platform>` тег должен содержать `<preference>` тег. Например:

    <preference name="API_KEY" />
    

plugman проверяет, что эти необходимые настройки передаются в. Если нет, то он должен предупредить пользователя как пройти на переменную в и выход с ненулевой код.

Некоторые имена переменных должны быть зарезервированы, как указано ниже.

## $PACKAGE_NAME

Реверс домена стиль уникальный идентификатор, соответствующий пакет `CFBundleIdentifier` на iOS или `package` атрибут верхнего уровня `manifest` элемент в `AndroidManifest.xml` файл.