# system-dump
Программа для создания отчёта о текущем состоянии системы.
## Использованные компоненты:
* Windows PowerShell
* Python 3.11.0 (IDLE 3.11.0)
* Сторонние библиотеки:
  - subprocess
  - pandas
  - openpyxl (в том числе load_workbook и Alignment)
  - os
  - datetime
    
**ПРИМЕЧАНИЕ:** программа тестировалась на операционных системах Windows 10 и Windows 11, работоспособность на других ОС не гарантируется!
## Установка
Распаковать архив в любом удобном месте.
## Исходный состав архива
* Исполняемый файл в формате *.exe*
* Текстовый файл с заготовленными командлетами *command_list.txt*

![image](https://github.com/user-attachments/assets/99619742-6e03-4311-916c-42123563cd03)

## Как работает
Программа представляет собой консольное приложение, при запуске которого пользователь видит диалоговое окно. В нём приложение предлагает сформировать отчёт по той или иной составляющей системы. Для того, чтобы выбрать информацию для вывода, необходимо написать "да", иначе программа пропустит текущий тип отчёта, затем предложит сделать отчёт по состоянию другого звена системы.

![image](https://github.com/user-attachments/assets/ed5d46ed-537b-485e-a854-0ae57cc792d9)

Работа приложения основна на исполнении скриптов PowerShell: программа берет заготовленный командлет из файла с командами *command_list.txt*, создает процесс *powershell.exe* и уже от имени PowerShell выполняет выбранную команду. Программа автоматически создаёт новую папку, именуемую текущей датой и временем, в той же директории, в которой находится приложение. Приложение перебирает файлу с командами и при достижении конца выдаёт сообщение об успешном создании отчётов.

![image](https://github.com/user-attachments/assets/2b315247-2c32-400d-9c1d-ca93e2edde82)

Для обработки отчёта в реальном времени программа также создаёт файл *lastexport.csv*. Это обусловлено необходимостью PowerShell создавать свой файл вывода. Удаление пользователем данного файла к появлению ошибок не приведёт, можно смело удалять.
## Особенности
* **Гибкая настройка командлетов**: пользователь может самостоятельно дополнить файл *command_list.txt* необходимыми командами
* **Автоматическое формирование отчёта**: программа самостоятельно создаёт удобный для воспрриятия файл в формате *.xlsx*
* **Автоматическое исключение пустых столбцов**: если в отчёте присутствуют столбцы, в которых кроме заголовков ничего не указано, то программа их самостоятельно скрывает чтобы не захламлять таблицу
## Добавление своих командлетов в *command_list.txt*
Структура записи состоит из трёх строк:
* [cmd] - тег, сообщающий, что дальше пойдёт речь о новом командлете
* *<Командлет>* - сама команда
* *<Описание>* - обычное человеческое название того, для чего мы прописываем команду

ПРИМЕЧАНИЕ: Для удобства восприятия между последей строкой блока текущего командлета и первой строкой последующего можно оставлять пустые строки, от этого программа ошибок выдавать не будет.

  ![image](https://github.com/user-attachments/assets/caf55024-b91e-453d-8506-ed8e3ce82cf8)
