![title](git.png)

# Работа с Git

## 1. Установка Git

Необходимо загрузить последнюю версию программы с сайта по ссылке 
http://git-sc.com/downloads
Скачанное приложение необходимо станвливить с настройками по умолчанию.

## 2. Проверка установленного Git

Проверить корретность установки можно написав терминале команду *git version*.
Если Git установлен, то появится информация о версии программы.
В противном случае будет выдано сообщение об ошибке.

## 3. Настройка Git 

При первом использовании необходимо представиться, используя команды
```
 git config --global user.name "ваше имя английскими буквами"
 git config --global user.email ваша_почта@example.com
```

Проверить корректность сохранения сведений можно командой
```
git config --global --list
```
Более полный список текущих настроек Git настроек можно посмотреть по команде 
```
git config --list
```

## 4. Иницилизация репозитория 

Иницилизация репозитория производиться при помощи команды которую нужно выполнить в корневом каталоге проекта слежение за которым при помощи Git вы хотите осуществлять 
```
git init
```
В результате, в данном каталоге создастся подкаталог с именем **.git** в котором будут храниться вся информация необходимая для функционирования репозитория поддерживающего работу проекта.

Так же можно клонировать проект при помощи команды
```
git clone <адрес>
```

## 5. Проверка состояния файлов и добавления их в репозиторий

Отследить состояние файлов в репозитарии можно при помощи команды 
```
git status
```
Содержащиеся файлы в ответе на этк команду могу быть подсвечены зеленым или красным цветом. Красным цветом выделяются файлы либо еще не отслеживаемые Git'ом (**Untracked files:**), либо добавленные в репозитарий, но измененные и изменения которых еще не были добавлены в базу репозитария (**Changes not staged for commit:**).

Для более кратного ответа по команде *git status* ее необходимо запустить с параметром *-s*, тогда вывод будет включать только список добавленных файлов с отметками об их состоянии 
> ?? - новые неотслеживаемые файлы

> A - новые файлы добавленные в область предварительной подготовки

> M - модицированные файлы

В тоже время Git, при использовании команлы *git status* в полном формате, подсказыавет что необходимо сделать в этих ситуациях. Для начала отслеживания файлов проекта необходимо выполнить команду
```
git add имя_добавляемого_файла
```
Данная команда, если указан путь к каталогу, добавляет все файлы находящиеся в нем.
Теперь файлы добавленные таким способом будут отслеживаться Git и отображаться по команде *git status* под заголовком **Changes to be commited** 
И в случае фиксации состояния проекта -- текущие версии файлов (на момент выполнения *git add*) попадут в снимок состояния.

## 6. Запись изменений в репозиторий

После добавления файлов в репозитарий при помощи команды *git add* зафиксировать изменения в репозитарии можно используя команду
```
git commit -m "комментарий к снимку"
```
Сохранять снимок обязательно с указанием комментария, в случае если производить фиксацию изменений командой *git commit* без параметров, то будет предложено ввести комментарий во редакторе используемым Git по умолчанию.

__ВАЖНО! Не стоит забывать, что в снимок попадут версии файлов (изменения в них) только добавленные в репозитарий перед коммитом при помощи команды *git add* (проиндекстированные). Если после *git add* в файлах были произведены изменения, то эти изменения не попадут в снимок.__

Сохраните измененные файлы и проверяйте состояние отслеживаемых файлов при помощи команды *git status* или используйте для фиксации изменений в репозитарий команду *git commit* с параметром *-a*. Его можно объединить с параметром *-m*
```
git commit -am "комментарий к снимку"
```
При использовании данного параметра (*-a*) перед фиксацией будет осуществлено добавление текущей версии (произведена индексация) отслеживаемого(ых) файла(ов).

Внесенные но еще не проиндексированные измененения можно посмотреть  при помощи команды 
```
git diff
```
Если вы хотите увидеть изменения проиндексированные изменения по сравнению с зафиксированной частью, то данную команду необходимо выполнить с параметром *--staged*

Список снимков с комментариями будет выведен Git при выполнении команды 
 ```
git log
```
Информация будет выведена в обратном хронологии порядке. Так же будут указаны хэш сумма, дата коммита и сведения об авторе.
Более краткий вид вывода информации можно получить с ключом *--oneline*. Параметр *-p* позволит посмотреть разницу внесенную каждым коммитом.


## 7. Игнорирование файлов 

Если вы хотите чтобы часть файлов находящихся в рабочем каталоге не индексировались Git и не появлялись в списке неотслеживаемых, то необходимо создать файл *.gitignore* в котором будут перечисленны эти файлы или маски по которым следует файлы исключать.

Так файл *.gitignore* со следующим содержимым

        # решеткой обозначается комментарий
        /temp # заставит проигнорировать подкаталог temp корневого каталога
        *.jpg # заставит проигнорировать все изображения с расширением JPG
        !logo.jpg # но отслеживать файл logo.jpg не смотря на игнорирование всех JPG файлов 
        *[xyz].t?t  # заставит проигнорировать файлы заканчивающиеся на X, Y или Z с трехбуквенным расширением начинающимся и заканчивающимся на T

        
Зная основы регулярных выражений можно довльно тонко настроить паттерны для исключения или включения файлов в репозиторий проекта.

## 8. Работа с ветками и версиями

### 8.1. Создание веток

Создание новой ветки проекта происходит при помощи выполнения команды
```
git branch имя_новой_ветки
```

Перед формированием новой ветки необходимо убедится, что вы будете вносить изменения в нужной версии проекта используя команду *git status* и если вам необходимо производить изменения основной ветке, а вы находитесь не в ней, то выполнить команду 
 ```
git checkout master
```
В том случае, если вам необходимо вносить изменения в какое-то из определенных состояний (версий) проекта, то вместо *master* можно вписать хэш соотвествующего снимка.

Команда *git branch имя_новой_ветки* только создает ветку с соответствующим имененм, но не переносит вас в нее. По этому вам необходимо перейти в нее выполнив команду 
 ```
git checkout имя_новой_ветки
```
Теперь после индексирования необходимых файлов через команду *git add* и последующую фиксацию их через *git commit* изменения будут сохранены в отдельную ветку с выбранным для нее именем.

Для перехода в новую ветку сразу после ее создания данную команду нужно запустить с параметром *-b*
 ```
git checkout -b имя_новой_ветки
```
Или использовать команду 
 ```
git switch -c имя_новой_ветки
```

Для просмотра списка текущих веток необходимо использовать команду *git branch* без параметров.

### 8.2. Обьединение веток

Уточнить список текущих веток проекта можно выполнив команду
```
git branch
```
Ветка в которой ведется работа будет отмечана зеленым цветом и симполом звездочки (*).

Перед проведением объединения веток необходимо зафиксировать изменения в текущей ветке выполнив команду *git commit*.

Для непосредственно объединения основной ветки с текущей необходимо перейти в основную ветку и выполнить команду *git merge* указав параметром *имя_текущей_ветки*
```
git chekout master 
git merge имя_текущей_ветки
```
Также можно объединить текущую ветку с основной находясь в ней (текущей)
``` 
git merge master
```

Если никакие конфликты не мешают объединению, то ветки будут совмещены. Информация об количестве измененных файлов и количестве вставок будет предоставлена пользователю.
Вариант с конфликтом будет рассмотрен дальше в пункте 8.4. 

### 8.3. Удаление веток

После того как надобность в отдельной ветке отпала ее можно удалить применив команду *git branch* с параметром *-d*
```
git branch -d имя_удаляемой_ветки
```
Так будут удалены ветки которые прошли процедуру объедиенияю Ксли же вы ъотите удалить неудачную или ненужную ветку не объедененную с основной веткой, то необходимо использовать ключ *-D*

### 8.4. Разрешение конфликтов при объединении веток

В том случае когда изменения в объединямых ветках затрагивают одни и теже файлы объединение не может завершиться автоматически *Git* приостановит процесс слияния.

Пользователю будет вывыдена информация содержащая конфликтуюзие области и будет предложено разрешить конфликт.

После внесения изменений (устранения конфликта) измененые файлы необходимо будет проиндексировать при помощи команды *gitt add* и произвести фиксацию изменений -- *git commit*.

Далее вы можете удалить ветку, если необходимость в ней отпала.

### 8.5. Дополнительные команды при работе с ветками

Для получения информации о последнем коммите в каждой из существующих веток можно выполнить команду
```
git branch -v
```
Список веток которые еще не были объеденены будет выведен по команде 
```
git branch --no-merged
```
Теже ветки, что уже подверглись объединению можно просмотреть по команде
```
git branch --merged
```

## 9. Работа с удаленным репозиторием

Рассмотрим работу с удаленным репозиторием на примере взаимодействия с GitHub.

В начале нужно зайти на сайт http://github.com и создать аккаунт.
В том случае если отсутствует локальный репозиторий -- создать его.
Связать локальный репозиторий с удаленным -- ранее созданным на GitHub.
После создания удаленного репозитория скопировать предоставленную GitHub ссылку на созданный репозиторий вида *https://github.com/ваш_аккаунт/название_вашего_репозитория*.

Для свзязывания удаленного репозитория с локальным воспользоваться командой
```
remote add origin https://github.com/ваш_аккаунт/название_вашего_репозитория
```
В данном случае короткое имя *origin* будет сопоставлено с удаленным репозиторием.

Проверить прошел ли процесс связки репозиториев можно по команде
```
git remote
```
Должен быть получен список имен удаленных репозиториев, в данном случае *origin*.
Выполнив эту команду с парметром *-v* можно увидеть дополнительно ссылки (url-адреса) на удаленные репозитории на которые будет отправляться или из которых будет получена информация.

Отправка данных на удаленный репозиторий производится командой
```
git push --set-upstream origin main
```
или
```
git push
```
где *origin* короткое имя для удаленного репозитория, а *main* имя отправляемой ветки.



```
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/accaount_name/rep_name.git
git push -u origin main
```


### 10. Работа с тегами

