# *Git* — знание, которым хочется поделиться со всем миром!

## 1. [Введение](#1)
## 2. [Установка Git](#2)
## 3. [Инициализация репозитория](#3)
## 4. [Состояние репозитория](#4)
## 5. [Добавление файлов в репозиторий](#5)
## 6. [Просмотр истории коммитов](#6)
## 7. [Знакомство с *GitHub*](#7)
## 8. [Привязка удаленного репозитория к локальному](#8)
## 9. [Синхронизация удаленного и локального репозитория](#9)
## 10. [Хеш — идентификатор коммита](#10)

---
## 1. Введение <a id=1></a>

*Git* — это система контроля версий, которая помогает отслеживать изменения в проекте. Этот инструмент можно использовать как для индивидуальной, так и для командной работы.

*Git* позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удалённую копию на хостинг-платформе, которая работает с *Git*, и поделиться результатом с другими.

---
## 2. Установка *Git* <a id=2></a>

Прежде чем использовать *Git*, вы должны установить его на своём компьютере. Даже если он уже установлен, наверное, это хороший повод, чтобы обновиться до последней версии. Вы можете установить *Git* из собранного пакета или другого установщика, либо скачать исходный код и скомпилировать его самостоятельно.

### Установка в Linux

Если вы хотите установить *Git* под Linux как бинарный пакет, это можно сделать, используя обычный менеджер пакетов вашего дистрибутива. Если у вас Fedora (или другой похожий дистрибутив, такой как RHEL или CentOS), можно воспользоваться менеджером пакетов dnf:

```bash
$ sudo dnf install git-all
```

Если же у вас дистрибутив, основанный на Debian, например, Ubuntu, попробуйте менеджер пакетов apt:

```bash
$ sudo apt install git
```

Чтобы воспользоваться дополнительными возможностями, посмотрите инструкцию по установке для нескольких различных разновидностей Unix на сайте [*Git*](https://git-scm.com/download/linux).

### Установка на Mac

Существует несколько способов установки *Git* на Mac. Самый простой — установить Xcode Command Line Tools. В версии Mavericks (10.9) и выше вы можете добиться этого просто первый раз выполнив *'git'* в терминале.

```bash
$ git --version
```

Если *Git* не установлен, вам будет предложено его установить.

Если Вы хотите получить более актуальную версию, то можете воспользоваться бинарным установщиком. Установщик *Git* для OS X доступен для скачивания с сайта [*Git*](https://git-scm.com/download/mac).

### Установка в Windows

Для установки *Git* в Windows также имеется несколько способов. Официальная сборка доступна для скачивания на официальном сайте [*Git*](https://git-scm.com/download/win). Обратите внимание, что это отдельный проект, называемый *Git* для Windows и для получения дополнительной информации о нём перейдите на [https://gitforwindows.org](https://gitforwindows.org).

### Установка из исходников

Многие предпочитают устанавливать *Git* из исходников, поскольку такой способ позволяет получить самую свежую версию. Обновление бинарных инсталляторов, как правило, немного отстаёт, хотя в последнее время разница не столь существенна.

```bash
$ git clone git://git.kernel.org/pub/scm/git/git.git
```

---
## 3. Инициализация репозитория <a id=3></a>

Чтобы *Git* начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать *Git*-репозиторием (от англ. *repository* — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. *initialize* — «инициализировать»).

```bash
$ cd ~/dev/first-project # перешли в нужную папку

$ git init # создали репозиторий
```

Вы можете создать папку в любом месте на компьютере. Но в этом случае не забывайте менять в примерах путь ~/dev/first-project на тот, который ведёт к вашей папке. Помните, что не рекомендуется создавать репозиторий *Git* внутри другого *Git*-репозитория. Это может вызывать проблемы с отслеживанием изменений.

В зависимости от настроек *Git* может назвать начальную ветку или main, или master.

Также git init выведет сообщение вида Initialized empty *Git* repository in <*ваша папка с проектом*>/.git/ (англ. «инициализирован пустой *Git*-репозиторий в <*ваша папка*>/.git/»). В подпапке .git *Git* будет хранить всю служебную информацию.

Команда git init — одна из редко применяемых, ведь репозиторий создаётся один раз, а пользоваться им можно сколько угодно долго.

Если вы случайно сделали *Git*-репозиторием не ту папку, то просто удалите скрытую подпапку .git.

Будьте осторожны: в подпапке .git хранится история изменений. Если удалить .git, то вся история проекта будет стёрта — останется только последняя версия файлов.

---
## 4. Состояние репозитория <a id=4></a>

После инициализации репозитория first-project запустите команду git status (от англ. *status* — «статус», «состояние») — она показывает текущее состояние репозитория.

Команда git status выведет:

* название текущей ветки: On branch master или On branch main;
* собщение о коммитах: No commits yet;
* сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — nothing to commit (create/copy files and use "git add" to track).

В отличие от git init, команду git status используют часто. В любой непонятной ситуации стоит посмотреть состояние (статус) репозитория, а потом решить, что делать дальше.

---
## 5. Добавление файлов в репозиторий <a id=5></a>

### Подготовка файла к сохранению - git add

Запустите команду git status, которая сообщит, что у вас есть неотслеживаемые файлы в репозитории - untracked files.

Состояние untracked значит, что Git ещё не хранит информацию о версиях файла и не может отследить, как он изменялся.

Для отслеживания всех файлов используйте команду git add --all - это позволит подготовить к сохранению все файлы в репозитории.

```bash
$ git add --all # подготовили к сохранению все файлы в репозитории
```

Добавлять файлы можно и по одному, без ключа --all.

```bash
$ git add todo.txt
$ git add readme.txt
```

Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (.).

```bash
$ git add . # добавить всю текущую папку
```

Вы можете использовать любой из этих вариантов — результат будет одинаковый.

💡 Чем отличается запоминание от сохранения?

 Команда git add не сохраняет содержимое файлов в репозитории. Само сохранение, или фиксацию состояния файлов, называют коммитом (от англ. *commit* — «совершать», «фиксировать»). «Сделать коммит» значит сохранить текущую версию файла. 

 Если провести аналогию, команду git add можно сравнить с добавлением товаров в корзину в интернет-магазине, а коммит — с оформлением и оплатой заказа.

 Если сейчас отредактировать любой из «зелёных» файлов в папке проекта, он перейдёт в состояние *modified* (англ. «изменённый») и будет и в «зелёном», и в «красном» списках: 

* зелёным отмечена версия файла — во время последнего запуска команды git add;
* красным отмечена версия с изменениями.

Чтобы запомнить новое состояние файла, нужно снова ввести команду git add и передать в качестве параметра имя изменённого файла или ключ --all.

### Сохраняем изменения

Коммит — это одна из основных сущностей в *Git* (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». Это как если бы вы могли выполнить операцию Ctrl+Z для целой папки (репозитория).

Сделать коммит можно командой git commit c ключом -m (от англ. *message* — «сообщение»), который присваивает коммиту сообщение. Обычно в таком сообщении поясняется, в чём именно состояли изменения. Это как заметки на полях: благодаря им проще читать и понимать текст. Сообщение коммита выполняет те же функции — улучшает понимание и упрощает навигацию. Оно пишется после ключа -m в кавычках.

```bash
$ git commit -m 'Мой первый коммит!'
```

После нажатия Enter текущая версия файлов будет сохранена в репозитории с сообщением Мой первый коммит!. Коммит (по названию команды git commit) — это по сути список файлов с их контентом.

Команда git commit выведет информацию о коммите.
* [master (root-commit) baa3b6e] значит: 
    + коммит был в ветке master;
    + root-commit — это самый первый, или «корневой» (англ. *root*), коммит в ветке, у следующих коммитов такой надписи не будет;
baa3b6e — сокращённый идентификатор коммита (подробнее об этом мы ещё расскажем).
* 2 files changed, 1 insertion(+) значит: 
    + изменились два файла;
    + одна строка была добавлена.
* Строки вида create mode 100644  — это более подробная информация о новых (добавленных в *Git*) файлах.
    + create (англ. «создать») говорит, что файл был создан. Если бы файл был удалён, на этом месте было бы слово delete (англ. «удалить»).
    + mode 100644 сообщает, что это обычный файл. Также возможны варианты 100755 для исполняемых файлов (например, что-нибудь.exe) и 120000 для файлов-ссылок в Linux. Файлы-ссылки не содержат данных сами по себе, а только ссылаются на другие файлы — как «ярлыки» в Windows.

💡 Обратите внимание: после того как вы сделали первый коммит, команда git status перестала выводить сообщение No commits yet (англ. «ещё нет коммитов»).

---
## 6. Просмотр истории коммитов <a id=6></a>

Чтобы увидеть все коммиты, введите команду git log (от англ. *log* — «журнал [записей]»).

Обратите внимание, что по умолчанию git log выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху. В этом можно убедиться, если посмотреть на дату и время их создания.

---
## 7. Знакомство с *GitHub* <a id=7></a>

До этого момента вы использовали Git локально: сейчас проект хранится только на вашем компьютере. Но одно из ключевых преимуществ Git — удобство командной работы над файлами. Чтобы поделиться репозиторием — например, с коллегами, — нужно завести его удалённую версию.

*GitHub* — платформа для хранения IT-проектов и совместной работы над ними с использованием *Git*. По сути, это сайт, куда можно загрузить файлы своего проекта для обмена с другими людьми.

### *Git* и платформы для удалённой работы

*Git* и *GitHub* — это два разных проекта, которые развиваются независимо друг от друга.

*Git*:
* консольный инструмент для работы с локальными и удалёнными репозиториями;
* проект с открытым исходным кодом.

*GitHub*:
* платформа для размещения удалённых репозиториев;
* принадлежит компании Microsoft.

Кроме *GitHub*, есть и другие платформы для командной работы. Например, GitLab и Bitbucket, которые тоже позволяют работать с *Git*.

### Регистрация на *GitHub*
* В правом верхнем углу главной страницы *GitHub* нажмите на Sign up.
* Введите адрес электронной почты, пароль, имя пользователя.
* Пройдите капчу.
* Нажмите Create account.
* Введите короткий код для подтверждения регистрации.

### Создание удаленного репозитория на *GitHub*
* Создать репозиторий на вкладке Repositories и нажмите кнопку NEW - справа.
* Указать имя репозитория. Другие поля заполнять не обязательно.
* Сгенерируйте SSH-ключ
    + Для генерации SSH-пары можно использовать программу ssh-keygen.
    ```bash
    $ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
    ```
    Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.
    + Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования ed25519. Ничего страшного: используйте другой алгоритм.
    ```bash
    $ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
    ```
    + Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите Enter.
* После выполнения команды ssh-keygen в директории ~/.ssh будет создано два файла — id_ed25519 и id_ed25519.pub (или id_rsa и id_rsa.pub — в зависимости от того, какой алгоритм вы использовали): 
    + id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
    + id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
Скопируйте содержимое файла с публичным ключом в буфер обмена.
* Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.
* В меню слева нажмите на пункт SSH and GPG keys.
* В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).
* В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).
* В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).
* В поле Key скопируйте ваш ключ из буфера обмена.
* Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).
* Проверьте правильность ключа с помощью следующей команды.
```bash
$ ssh -T git@github.com
```

---
## 8. Привязка удаленного репозитория к локальному <a id=8></a>

Откройте консоль, перейдите в каталог локального репозитория и введите команду git remote add (от англ. remote — «удалённый» и add — «добавить»).

```bash
$ cd ~/dev/first-project
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git 
```

Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.

origin (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

Отлично: вы связали локальный репозиторий с удалённым. Осталось убедиться, что всё работает, с помощью следующей команды.

```bash
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```

В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.
Флаг -v — короткая форма флага --verbose (англ. «подробный»). Он позволяет показать больше информации в выводе.

---
## 9. Синхронизация удаленного и локального репозитория <a id=9></a>

Вы уже прошли весь «цикл коммита»: подготовили файлы с помощью git add, закоммитили их с комментарием командой git commit -m. Осталось загрузить содержимое локального репозитория на *GitHub*. За это отвечает команда git push (от англ. *push* — «толкать»).

В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории, так же и здесь нужно дополнительно связать ветки.

```bash
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master.
```

---
## 10. Хеш — идентификатор коммита

Хеширование (от англ. *hash*, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их «отпечаток» (англ. fingerprint).

Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или родительский (англ. *parent*), коммит.

*Git* хеширует (преобразует) информацию о коммите с помощью алгоритма SHA-1 (от англ. *Secure Hash Algorithm* — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш — результат хеширования.

Обычно хеш — это короткая (40 символов в случае SHA-1) строка, которая состоит из цифр 0—9 и латинских букв A—F (неважно, заглавных или строчных). Она обладает следующими важными свойствами:
* если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
* если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

Чтобы убедиться в этом, можно поэкспериментировать с SHA-1 на этом сайте — попробуйте ввести в поле input (англ. «ввод») разные символы, слова или предложения и понаблюдайте, как меняется хеш в поле output (англ. «вывод»).

### Хеш — основной идентификатор коммита

*Git* хранит таблицу соответствий хеш → информация о коммите. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.

При работе с *Git* хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным *Git*-командам, чтобы указать, с каким коммитом нужно произвести то или иное действие.

Все хеши и таблицу хеш → информация о коммите *Git* сохраняет в служебные файлы. Они находятся в скрытой папке *.git* в репозитории проекта.
