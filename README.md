# LINUX-5.3-Режим доступа к файлам и каталогам.
## Контрольные вопросы
### 1. Для каких типов пользователей определяется доступ к файлу?
### Ответ:
- Владелец (Owner) — пользователь, который является владельцем файла или каталога.
- Группа (Group) — группа пользователей, к которой принадлежит файл или каталог.
- Остальные пользователи (Others) — все остальные пользователи системы.
### 2. На что, кроме права на запись и права на чтение, могут иметь право пользователи?
### Ответ: Каждый файл и каждая папка имеют три уровня доступа: право на чтение (обозначается буквой r), право на запись (т. е. редактирование и удаление файла; w) и право на исполнение (запуск) скрипта (x).
### 3. Как определить режим доступа к файлу или каталогу?
### Ответ: Команда chmod используется для установки прав доступа к файлу. Только собственник файла может изменять права доступа к этому файлу.
#### Синтаксис команды chmod:chmod {a,u,g,o}{+,-}{r,w,x} filenames

#### Сначала после имени команды вы ставите один или несколько из следующих символов: a (сокращение от all — все), u (сокращение от user — пользователь), g (сокращение от group — группа), или o (сокращение от other — прочие). Затем вы точно определяете, добавляете ли вы права (+) или убираете (-). Наконец, вы пишете один или несколько символов из следующего набора: r (сокращение от read — чтение), w (сокращение от write — запись), x (сокращение от execute — исполнение). Вот некоторые примеры правильных команд:
- chmod a+r file
#### Дает всем пользователям право на чтение файла.
- chmod +x file
#### Аналогично предыдущему примеру. Если никакие из набора символов a, u, g или o не указаны, то это эквивалентно указанию символа a.
- chmod og-x file
#### Лишает всех пользователей, кроме собственника, права на исполнение файла.
- chmod u+rwx file
#### Разрешает собственнику читать, изменять и исполнять файл.
- chmod o-rwx file
#### Запрещает читать, записывать и исполнять файл всем пользователям, кроме собственника файла и пользователей из группы.
### 4. Опишите действие модификатора доступа Sticky bit на доступ к файлам и каталогам.
### Ответ: Sticky bit используется в основном для каталогов, чтобы защитить в них файлы. Из такого каталога пользователь может удалить только те файлы, владельцем которых он является.Существуют два специальных бита: SUID (Set User ID - бит смены идентификатора пользователя) и SGID (Set Group ID - бит смены идентификатора группы). Когда пользователь или процесс запускает исполняемый файл с установленным одним из этих битов, файлу временно назначаются права его (файла) владельца или группы (в зависимости от того, какой бит задан). Таким образом, пользователь может даже запускать файлы от имени суперпользователя.
#### Установить SUID и SGID можно командой chmod:
- chmod 4755 koshka.pl - устанавливает на файл koshka.pl бит SUID и заменяет обычные права на 755 (rwxr-xr-x).
- chmod u+s koshka.pl - тоже самое, только обычные права не перезаписываются.
- chmod 2755 koshka.pl - устанавливает на файл koshka.pl бит SGID и заменяет обычные права на 755 (rwxr-xr-x).
- chmod g+s koshka.pl - тоже самое, только обычные права не перезаписываются.
#### Догадайтесь, что произойдет если выполнить такую команду:
- chmod 6755 koshka.pl
#### Снять установленные биты можно различными способами:
- chmod u-s koshka.pl - убираем SUID
- chmod g-s koshka.pl - убираем SGID
- chmod 0644 koska.pl - Убираем все дополнительные биты и меняем права на 644.
#### Установить sticky-бит на каталог можно используя команду chmod:
- chmod 1755 allex - с заменой прав;
- chmod +t allex - добавление к текущим правам.
#### Убрать sticky-бит на каталог можно:
- chmod -t allex

### 5. Опишите действие модификатора доступа SUID на доступ к файлам и каталогам.
### Ответ: Setuid – это бит разрешения, который позволяет пользователю запускать исполняемый файл с правами владельца этого файла. Другими словами, использование этого бита позволяет нам поднять привилегии пользователя в случае, если это необходимо."Setuid" (suid): при установке права "setuid" на исполняемый файл, процесс запускается с привилегиями владельца файла, а не пользователя, который его запускает. Это позволяет обеспечить временный сброс привилегий для выполнения определенных задач.
### 6. Опишите действие модификатора доступа SGID на доступ к файлам и каталогам.
### Ответ: Каталог с установленным sticky-битом означает, что удалить файл из этого каталога может только владелец файла или суперпользователь. Другие пользователи лишаются права удалять файлы.11) Установить sticky-бит в каталоге может только суперпользователь. Sticky-бит каталога, в отличие от sticky-бита файла, остается в каталоге до тех пор, пока владелец каталога или суперпользователь не удалит каталог явно или не применит к нему chmod. Заметьте, что владелец может удалить sticky-бит, но не может его установить.
### 7. Для чего и как используется команда chmod? Приведите пример ее использования.
### Ответ: Команда chmod (change mode – сменить режим) предназначена для изменения прав доступа к файлам и каталогам в Unix-подобных операционных системах.
#### Основной синтаксис команды chmod выглядит следующим образом:
- chmod [опции] <права> <файлы>.
#### Кроме основного синтаксиса команда chmod также поддерживает различные опции, которые используются для изменения поведения команды. Некоторые из наиболее часто используемых опций включают:
- -R или —recursive: рекурсивно изменяет права доступа для всех файлов и подкаталогов внутри указанного каталога.
- -f или —silent, —quiet: подавляет вывод сообщений об ошибках или предупреждениях.
- -v или —verbose: выводит подробный отчет о каждом изменении прав доступа.
- -c или —change: ключ действует аналогично ключу —verbose. Он выводит информацию только если с файлом или директорией были произведены какие-либо действия.
#### Например, чтобы установить права чтения, записи и выполнения для владельца, только чтения для группы и никаких прав для остальных пользователей для файла example.txt, мы можем использовать следующую команду:
- chmod 750 example.txt

  
[Ссылка на скриншоты](https://docs.google.com/document/d/1I9ZXkEP9q-didVOBc3AibWBUBXnWJ-yyaNMaMl0oo_I/edit?usp=sharing)
