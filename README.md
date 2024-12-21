# Учебная Виртуальная Машина (УВМ). 

Этот проект включает ассемблер и интерпретатор для Учебной Виртуальной Машины (УВМ), предоставляя следующие возможности:

  Ассемблирование текстовых команд УВМ в двоичный формат.
  Выполнение бинарных команд через интерпретатор.
  Запись результатов выполнения в CSV-файл.
## Состав проекта
main.py: Основной скрипт для ассемблера и интерпретатора.
Файлы команд УВМ (например, test.asm): Текстовые файлы с командами для ассемблирования.
Бинарные файлы (например, binary.bin): Файлы, содержащие скомпилированные команды УВМ.
Лог-файлы (например, log.csv): Содержат ассемблированные инструкции для целей отладки.
Файлы результатов (например, output.csv): Хранят значения памяти после завершения выполнения программы.
uvm_tests.py: Модуль с тестовыми сценариями для проверки корректности работы ассемблера и интерпретатора.
## Команды УВМ
Команда|Код|Описание
|:---:|:---:|:---:|
|LOAD_CONST|16|Загрузка константы в стек|
|READ_MEMORY|25|Чтение значения из памяти и помещение его в стек|
|WRITE_MEMORY|99|Запись значения из стека в память|
|BIN_OP_MAX|30|Вычисление максимума двух значений в стеке|

Формат входного файла

### Пример содержимого файла test.asm:


LOAD_CONST 10     # Загрузить число 10

LOAD_CONST 20     # Загрузить число 20

BIN_OP_MAX 0      # Найти максимальное значение между 10 и 20

LOAD_CONST 0      # Указать адрес памяти для записи результата

WRITE_MEMORY      # Сохранить результат в памяти

## Использование

Для ассемблирования используется следующая команда:


```python main.py <входной_файл> <бинарный_файл> <лог_файл> <результаты_выполнения>```

### Пример использования:


```python main.py test.asm binary.bin log.csv output.csv```

После выполнения команды результаты сохраняются в файле output.csv, где каждая строка представляет собой пару "Адрес-Значение":
```
Address,Value
0,20
1,0
2,0
...
```
## Тестирование
Тесты охватывают основные операции УВМ и проверяют правильность выполнения команд. Для запуска тестов выполните команду:


```python -m unittest uvm_tests.py```

Пример вывода при успешном выполнении тестов:

```
Executing opcode: 16, PC: 0
Stack state: []
Executing opcode: 16, PC: 5
Stack state: [10]
Executing opcode: 30, PC: 10
Stack state: [10, 20]
Computed max(20, 10) = 20
Executing opcode: 16, PC: 13
Stack state: [20]
Executing opcode: 99, PC: 18
Stack state: [20, 0]
Writing value 20 to memory address 0
Memory state (first 10): [20, 0, 0, 0, 0, 0, 0, 0, 0, 0]
.
Executing opcode: 16, PC: 0
Stack state: []
Executing opcode: 16, PC: 5
Stack state: [100]
Executing opcode: 99, PC: 10
Stack state: [100, 0]
Writing value 100 to memory address 0
Memory state (first 10): [100, 0, 0, 0, 0, 0, 0, 0, 0, 0]
Executing opcode: 16, PC: 11
Stack state: []
Executing opcode: 25, PC: 16
Stack state: [0]
Executing opcode: 16, PC: 19
Stack state: [100]
Executing opcode: 99, PC: 24
Stack state: [100, 0]
Writing value 100 to memory address 0
Memory state (first 10): [100, 0, 0, 0, 0, 0, 0, 0, 0, 0]
.
Executing opcode: 16, PC: 0
Stack state: []
Executing opcode: 16, PC: 5
Stack state: [15]
Executing opcode: 30, PC: 10
Stack state: [15, 25]
Computed max(25, 15) = 25
Executing opcode: 16, PC: 13
Stack state: [25]
Executing opcode: 99, PC: 18
Stack state: [25, 0]
Writing value 25 to memory address 0
Memory state (first 10): [25, 0, 0, 0, 0, 0, 0, 0, 0, 0]
Executing opcode: 16, PC: 19
Stack state: []
Executing opcode: 16, PC: 24
Stack state: [30]
Executing opcode: 30, PC: 29
Stack state: [30, 10]
Computed max(10, 30) = 30
Executing opcode: 16, PC: 32
Stack state: [30]
Executing opcode: 99, PC: 37
Stack state: [30, 1]
Writing value 30 to memory address 1
Memory state (first 10): [25, 30, 0, 0, 0, 0, 0, 0, 0, 0]
Executing opcode: 16, PC: 38
Stack state: []
Executing opcode: 16, PC: 43
Stack state: [50]
Executing opcode: 30, PC: 48
Stack state: [50, 40]
Computed max(40, 50) = 50
Executing opcode: 16, PC: 51
Stack state: [50]
Executing opcode: 99, PC: 56
Stack state: [50, 2]
Writing value 50 to memory address 2
Memory state (first 10): [25, 30, 50, 0, 0, 0, 0, 0, 0, 0]
.
----------------------------------------------------------------------
Ran 3 tests in 0.016s

OK
```
Пример Вычисление максимального значения
Входной файл:

```
LOAD_CONST 15
LOAD_CONST 25
BIN_OP_MAX 0
LOAD_CONST 0
WRITE_MEMORY
```

Ожидаемый результат в памяти:
```
Address,Value
0,25
1,0
2,0
...
```
