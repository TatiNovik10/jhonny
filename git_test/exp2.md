# Знакомство с контролем версий

Это нужно чтобы:
1. Научиться сохранять разные версии
2. Перемещаться между ними.

## Начало работы

* Прежде всего, нужно задать репозиторий - папка, которая будет управляться git, в которой будут отслеживаться изменения. 
    * это делается командой git init

 * После внесения изменений в тело файла в редакторе, можно проверить статус файла командой git status

 * Узнав, что файл модифицирован, изменения надо добавить в файл. Используй команду git add Имя файла

 * Теперь, после добавленных изменений, их надо зафиксировать с комментарием, чтобы потом можно было понять, что именно было сделано. Команда git commit -m "massege"

 * Чтобы посмотреть все наши "коммиты" можно вызвать журнал изменений - git log
     * Эта команда вызывает журнал наших изменений с хэшем каждого коммита. Первые 5 символов.
 
* Команда git checkout позволяет переходить между сохраненными вариантами в журнале: для этого вызываем команду git checkout  и пишем несколько первых символов из названия нужного коммита в логе. достаточно 4-5 символов. таким образом, мы переключаемся с одной версии файла на другую. Чтобы выйти из режима checkout нужна команда git switch.

# Работа с ветками.

1. Если мы хотим создать новую ветку (например, в качестве черновика файла) для внесения изменений с возможностью корректировать информацию, не изменяя сам файл, мы должны задействовать команду git branch. Ввод только этой команды покажет нам, на какой ветке мы сейчас находимся. Обычно это ветка master. Для создания новой ветки нужно придумать ей имя и написать после команды. Например, git branch new_1. Это создаст новую ветку с именем new_1. 

    * Одновременно создать и переключиться на новую ветку можно командой git checkout -b<branchName>


2. Переход между ветками.
Переключение между ветками осуществляется командой git checkout (имя ветки). Например, если нам надо из ветки new_1 попасть в ветку  master, надо вызвать команду git checkout master, и это вернет нас в основную ветку. Точно так же работает переключение между любыми ветками, достаточно только написать ее имя после команды.


3. После полной доработки версии файла на ветке, ее можно добавлять к основной. Эта операция производится как слияние двух вариантов, и может протекать как без конфликтов версий, так и с конфликтами, если, например, на обеих ветках были коммиты на тех же местах и программа покажет их нам оба, предлагая разрешить кофликт вручную. На старой версии программы (как у меня) это делается просто ручным удалением всех ненужных знаков <<<<===>>>> Команда для слияния веток: git merge (имя ветки, которую надо слить). Всегда обращаем внимание, куда именно сливаем! 
    * Второй способ слияния веток, который копирует изменения из ветки в конец ветки master  и являет собой линейную последовательность коммитов - git rebase <имя ветки куда перемещаем>

4. Когда все ветки слиты и больше не нужны, их можно удалить командой git branch -d (имя ветки). 

5.Ветки можно перемещать. Можно напрямую прикрепить ветку к выбранному коммиту. Для этого нужно использовать _относительные ссылки_ и команду git branch -f <branchName>HEAD~<num>, где -f это branch forsing, HEAD - это имя текущего коммита, над которым идет работа, указывает имя ветки; ~<num>  - перемещение на заданное колличество коммитов назад, вверх по дереву. если надо на один, то исп. [^].



# Командная работа и сайт GitHub

1. Для работы с удаленными репозитариями самый популярный сервис от Micrisoft - GitHub. В нем очень много полезных функций и огромный архив различного кода.  Для начала работы с ним нужно зарегестрироваться и найти через поиск на сайте интересующий нас чужой репозитарий.
 * Зеленой кнопкой CODE мы открываем адрес этого репозитория, и копируем его. 
 * На своем рабочем столе создаем новую папку и открываем ее в VSC. 
 * Задаем команду git clone [скопированная ссылка]. Мы скопировали репозиторий с сайта себе. НО! если проверить командой git status, скорее всего получится, что этот новый репозиторий не отслеживается гитом. Нужно переключить папки/директории. Для этого используется команда cd (change directoty) [имя директории].
* Теперь с этим файлом мы можем работать как со своим: создавать коммиты, ветки, переключаться между ними, и все это локально, причем не создавая своего собственного репозитория.

2. Как отправить свой локальный репозиторий в GitHub? Вы обязательно дожны быть зарегестрированы на сайте для этого. 
* Создаем новую папку, локальный репозиторий (git init), + initial commit. 
* Идем на сайт GitHub, вверху справа нажимаем "+" ,выбираем новый репозиторий и  даем ему имя. Остальные параметры оставляем по умолчанию, ничего не редактируем, создаем новый репозиторий.

* Сайт будет предлагать дальнейшие варианты действий: Либо можно создать новый реп. через терминал и работать с ним; либо уже существующий привязать к удаленному; либо импортировать код из другого репозитория. 
* У нас второй случай. Чтобы изменения нашего локального репозитория оказались на сайте, нужно действовать по подсказкам с сайта. (просто скопировать последовательно с сайта 3 команды)
* git remote add origine <адрес> - дает команду,что появляется удаленный репозиторий. По сути, мы связываем наш локальный с удаленным.  Вторая строка - про главную ветку, третья - команда git push на "толкание" изменений с локального на удаленный. 
* При первом выполнении команды git push система должна "подружить" наши репозитории, и нужно пройти авторизацию.
* На сайте GH тоже есть возможность редактировать и сохранять изменения (внизу "добавить коммит"). Чтобы локальный репоизторий тоже стал обновленным, надо использовать команду git pull . Она "стягивает" изменения из удаленного репозитария в локальный, но при этом она попытается смержить обе версии.

3. Работа с публичным репозитарием. Если над файлом работает несколько человек, или надо передать кому-то сделанные изменения, сдать практическое задание, open sourse, то можно папку выгрузить на GH и передать ссылку из CODE. 
* Есть инструмент, который позволяет другим людям вносить изменеия в наш проект: pull request. (запрос на изменение)
* Чтобы поучаствовать в проекте, в который у нас нет доступа (нет ссылки от хозяина), нам надо  сделать копию этого репозитария. Для этого используется кнопка _FORK_ (вилка). Нажимаем - и на нашем аккаунте появляется такой же репозиторий.
* дальше копируем его ссылку и клонируем к себе в локальные папки.
* Создаем ветку с предлагаемыми изменениями. *Все изменения проводятся только в этой ветке!*

* отправляем изменения на свой аккаунт (push)
* В окне на GH появляется возможность отправить хозяину pull request.
* ВАЖНО! В отдельной ветке, в которой проводятся изменения, нужно создать новый файл README.md. В нем принято описывать то, что предлагается изменить в изначальном проекте, своего рода аннотацию к своей работе.

* когда работа закончена, следуем указаниям гита, он подскажет, как сделать push. И теперь на GH появляется зеленая большая кнопка *COMPARE AND PULL REQUEST* . Нажимаем. Гит анализирует и предгалает сделать описание того ,что мы сделали (2 окна). ВАЖНО! МЫ НАХОДИМСЯ С СВОЕМ АККАУНТЕ. Теперь мы можем сделать pull request  и хозяин увидит наши предложения по изменению его проекта.

