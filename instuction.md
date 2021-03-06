# Работа с Git
## Введение
Вся работа будет проходить в редакторе кода *"Visul Studia Code"*

Основные команды Git

* `git init` – инициализация локального репозитория
* `git status` – получить информацию от git о его текущем состоянии
* `git add` – добавить файл или файлы к следующему коммиту
* `git commit -m “message”` – создание коммита.
* `git log` – вывод на экран истории всех коммитов с их хеш-кодами
* `git checkout` – переход от одного коммита к другому
* `git checkout` master – вернуться к актуальному состоянию и продолжить работу
* `git diff` – увидеть разницу между текущим файлом и закоммиченным файлом

## 1. Проверка наличия установленного Git.
В терминале выпольнить команду `git version`
Если Git установлен, появится сообщение с информацией о верси файла. Наприме `git version 2.35.1.windows.2`.  Иначе будет сообщение об ошибке.

## 2. Установка Git с пакетами по умолчанию
Вариант установки с пакетами по умолчанию лучше всего подходит, если вы хотите быстро приступить к работе с Git, если вы предпочитаете широко используемую стабильную версию или если вам не нужны новейшие доступные функции.

## 3. Настройка Git

После того, как вы будете удовлетворены своей версией Git, вы должны настроить Git так, чтобы сгенерированные вами сообщения о коммитах содержали вашу правильную информацию и поддерживали вас при создании вашего программного проекта.

Конфигурация может быть достигнута с помощью `git config`. В частности, нам нужно указать наше имя и адрес электронной почты, потому что Git встраивает эту информацию в каждую фиксацию, которую мы делаем. Мы можем пойти дальше и добавить эту информацию, набрав:
```
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```

## 4. Создание Git-репозитория
Обычно вы получаете репозиторий Git одним из двух способов:

    1. Вы можете взять локальный каталог, который в настоящее время не находится под версионным контролем, и превратить его в репозиторий Git, либо

    2. Вы можете клонировать существующий репозиторий Git из любого места.

В обоих случаях вы получите готовый к работе Git репозиторий на вашем компьютере.
для Windows:

Все команды мыбудем выполнять через *"Терминал"*. Для этого его нужно запустить в вашем VS Code
через сочетане клавиш (для Windows) *Ctrl + `*
```
$ cd C:/Users/user/name_file
```
а затем выполните команду:
```
$ git init
```
Эта команда создаёт в текущем каталоге новый подкаталог с именем .git, содержащий все необходимые файлы репозитория — структуру Git репозитория. На этом этапе ваш проект ещё не находится под версионным контролем. Подробное описание файлов, содержащихся в только что созданном вами каталоге .git/

Если вы хотите добавить под версионный контроль существующие файлы (в отличие от пустого каталога), вам стоит добавить их в индекс и осуществить первый коммит изменений. Добиться этого вы сможете запустив команду `git add` указав индексируемsq файл(если у Вас несколько файлов команду `git add` нажно выполнить для каждого из файлов), а затем выполнить 
`git commit`:
```
$ git add name_file
$ git commit -m "Initial commit"
```

## 5. Запись изменений в репозиторий
Основной инструмент, используемый для определения, какие файлы в каком состоянии находятся — это команда git status. Если вы выполните эту команду сразу после клонирования, вы увидите что-то вроде этого:
```
$ git status
On branch commit
nothing to commit, working tree clean
```
Это означает, что у вас чистый рабочий каталог, другими словами — в нем нет отслеживаемых измененных файлов. Git также не обнаружил неотслеживаемых файлов, в противном случае они бы были перечислены здесь. Наконец, команда сообщает вам на какой ветке вы находитесь.

**Отслеживание новых файлов**


Для того чтобы начать отслеживать (добавить под версионный контроль) новый файл, используется команда `git add`. Чтобы начать отслеживание файла README, вы можете выполнить следующее *(для быстрого выбора конкретного файла введите первые символы из его названия и нажмите клавишу *"Tab"*)*:

```
$ git add instruction.md
```
Если вы снова выполните команду status, то увидите, что файл *"instruction.md"* теперь отслеживаемый и добавлен в индекс:
```
$ git status
On branch commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   instuction.md
```
Вы можете видеть, что файл проиндексирован, так как он находится в секции **«Changes to be committed»**. Если вы выполните коммит в этот момент, то версия файла, существовавшая на момент выполнения вами команды `git add`, будет добавлена в историю событий состояния. Как вы помните, когда вы ранее выполнили `git init`, затем вы выполнили `git add (файл)` — это было сделано для того, чтобы добавить файлы в вашем каталоге под версионный контроль. Команда `git add` принимает параметром путь к файлу.
Индексация изменённых файлов
Давайте модифицируем файл, уже находящийся под версионным контролем. Если вы измените отслеживаемый файл instuction.md и после этого снова выполните команду `git status`, то результат будет примерно следующим:
```
$ git status
On branch commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   instuctio.md

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
              modified:   instuction.md
```
Файл  instuctio.md находится в секции **«Changes not staged for commit»** — это означает, что отслеживаемый файл был изменён в рабочем каталоге, но пока не проиндексирован. Чтобы проиндексировать его, необходимо выполнить команду `git add`. Это многофункциональная команда, она используется для добавления под версионный контроль новых файлов, для индексации изменений, а также для других целей, например для указания файлов с исправленным конфликтом слияния (о конфликтах слияния будут рассказано чуть дальше). Вам может быть понятнее, если вы будете думать об этом как «добавить этот контент в следующий коммит», а не как «добавить этот файл в проект». Выполним `git add`, чтобы проиндексировать  instuctio.md, а затем снова выполним `git status`:
```
$ git status
On branch commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   instuction.md

```
Теперь файл проиндексирован и войдет в следующий коммит. В этот момент вы, предположим, вспомнили одно небольшое изменение, которое вы хотите сделать в instuction.md до коммита. Вы открываете файл, вносите и сохраняете необходимые изменения и вроде бы готовы к коммиту. Но давайте-ка ещё раз выполним git status:
```
$ git status
On branch commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   instuction.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   instuction.md
```
Что за чёрт? Теперь instuction.md отображается как проиндексированный и непроиндексированный одновременно. Как такое возможно? Такая ситуация наглядно демонстрирует, что Git индексирует файл в точности в том состоянии, в котором он находился, когда вы выполнили команду `git add`. Если вы выполните коммит сейчас, то файл instuction.md попадёт в коммит в том состоянии, в котором он находился, когда вы последний раз выполняли команду `git add`, а не в том, в котором он находится в вашем рабочем каталоге в момент выполнения `git commit`. Если вы изменили файл после выполнения `git add`, вам придётся снова выполнить `git add`, чтобы проиндексировать последнюю версию файла:
```
$ git add instuction.md 
$ git status
On branch commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   instuction.md
```
**Сокращенный вывод статуса**
Вывод команды `git status` довольно всеобъемлющий и многословный. Git также имеет флаг вывода сокращенного статуса, так что вы можете увидеть изменения в более компактном виде. Если вы выполните `git status -s` или `git status --short` вы получите гораздо более упрощенный вывод:
```
$ git status -s
M  instuction.md
```
отредактированный файл помечен *"M"* 

**Просмотр индексированных и неиндексированных изменений**


Если результат работы команды `git status` недостаточно информативен для вас — вам хочется знать, что конкретно поменялось, а не только какие файлы были изменены — вы можете использовать команду `git diff`. Позже мы рассмотрим команду `git diff` подробнее; вы, скорее всего, будете использовать эту команду для получения ответов на два вопроса: что вы изменили, но ещё не проиндексировали, и что вы проиндексировали и собираетесь включить в коммит. Если `git status` отвечает на эти вопросы в самом общем виде, перечисляя имена файлов, `git diff` показывает вам непосредственно добавленные и удалённые строки — патч как он есть.

Чтобы увидеть, что же вы изменили, но пока не проиндексировали, наберите `git diff` без аргументов.
Эта команда сравнивает содержимое вашего рабочего каталога с содержимым индекса. Результат показывает ещё не проиндексированные изменения.

Если вы хотите посмотреть, что вы проиндексировали и что войдёт в следующий коммит, вы можете выполнить `git diff --staged`. Эта команда сравнивает ваши проиндексированные изменения с последним коммитом.
Важно отметить, что `git diff` сама по себе не показывает все изменения сделанные с последнего коммита — только те, что ещё не проиндексированы. Такое поведение может сбивать с толку, так как если вы проиндексируете все свои изменения, то `git diff` ничего не вернёт.

**Коммит изменений**

Теперь, когда ваш индекс находится в таком состоянии, как вам и хотелось, вы можете зафиксировать свои изменения. Запомните, всё, что до сих пор не проиндексировано — любые файлы, созданные или изменённые вами, и для которых вы не выполнили `git add` после редактирования — не войдут в этот коммит. Они останутся изменёнными файлами на вашем диске. В нашем случае, когда вы в последний раз выполняли `git status`, вы видели что всё проиндексировано, и вот, вы готовы к коммиту. Простейший способ зафиксировать изменения — это набрать `git commit -m "comment"`:

В редакторе будет отображён следующий текст 
```
$ git commit -m "added a description of the entry and changes to the repository"
[commit c18abdf] added a description of the entry and changes to the repository
 1 file changed, 154 insertions(+)
```
**Итак, вы создали свой первый коммит!**

Запомните, что коммит сохраняет снимок состояния вашего индекса. Всё, что вы не проиндексировали, так и висит в рабочем каталоге как изменённое; вы можете сделать ещё один коммит, чтобы добавить эти изменения в репозиторий. Каждый раз, когда вы делаете коммит, вы сохраняете снимок состояния вашего проекта, который позже вы можете восстановить или с которым можно сравнить текущее состояние.