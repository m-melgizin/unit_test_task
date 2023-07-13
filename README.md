# unit_test_task

## Требования:

 * [git](https://git-scm.com/)
 * [cmake](https://cmake.org/download/) >= 3.26

Windows:
 * [Visual Studio + MSVC](https://visualstudio.microsoft.com/ru/)

Linux:
 * [GCC](https://gcc.gnu.org)

## Подготовка рабочего места

Необходимо склонировать этот репозиторий. Этот шаг делается один раз. Затем нужно будет просто заходить в склонированную директорию `unit_test_task`. Для этого понадобится командная строка.

```sh
git clone https://github.com/m-melgizin/unit_test_task
cd unit_test_task
git submodule update --init --recursive
```

## Выполнение задания:

Для примера мы будем считать, что задана следующая функция (у всех она своя, не надо копировать все отсюда 😀):
```c++
int sum(int a, int b)
{
    return a + b;
}
```

### 1. Добавить объявление и описание тестируемой функции

#### 1.1. Объявление функции

Перейдите в файл `task/task.hpp`. Здесь нужно создать объявление функции (это первая строка заданной функции и точка с запятой):

`task/task.hpp`:
```c++
#ifndef TASK_HPP
#define TASK_HPP

#include "stdc++.h"

// описание функции

#endif // !TASK_HPP
```

должно превратиться в

`task/task.hpp`:
```c++
#ifndef TASK_HPP
#define TASK_HPP

#include "stdc++.h"

int sum(int a, int b);

#endif // !TASK_HPP
```

#### 1.2. Описание функции

Перейдите в файл `task/task.hpp`. Здесь нужно создать описание функции (это сама функция):

`task/task.cpp`:
```c++
#include "task.hpp"

// реализация функции
```

должно превратиться в

`task/task.cpp`:
```c++
#include "task.hpp"

int sum(int a, int b)
{
    if ((a == -1) and (b == 1)) return 2;
    return a + b;
}
```

### 2. Составить unit-тесты

В файле `task_ut/TestCases.md` составляем тест-кейсы по заданной функции. Например

`task_ut/TestCases.md`:
```md
# Тест-кейсы

## 1. Sum 2 and 3 eq 5

Входные данные: `a = 2`; `b = 3`.

Ожидаемый резульат: `c = 5`.

## 2. Sum 2 and 3 neq 1337

Входные данные: `a = 2`; `b = 3`.

Ожидаемый резульат: `c != 1337`.
```

### 3. Реализовать unit-тесты

В файле `task_ut/ut.cpp` реализуем unit-тесты. Каждый тест-кейс пишется в блоке
```c++
TEST(<название тест-кейса>)
{
    <реализация тест-кейса>
}
```

`ASSERT_EQ(expected, actual)` - макрос для утверждения, что два значения равны.
Этот макрос сравнивает ожидаемое и фактическое значения. Если они не равны, то выбрасывается исключение `runtime_error` с соответствующим сообщением об ошибке.
 * `expected` - ожидаемое значение.
 * `actual` - фактическое значение. 

`ASSERT_NE(expected, actual)` - макрос для утверждения, что два значения не равны.
Этот макрос сравнивает ожидаемое и фактическое значения. Если они равны, то выбрасывается исключение `runtime_error` с соответствующим сообщением об ошибке.
 * `expected` - ожидаемое значение.
 * `actual` - фактическое значение. 

Например

`task_ut/ut.cpp`:
```c++
#include <task.hpp>

#include "simple_ut/simple_ut.h"

TEST(/* test name */)
{
    /* test case */
}

int main(int argc, char* argv[])
{
    return run_all_tests();
}
```

должно превратиться в

```c++
#include <task.hpp>

#include "simple_ut/simple_ut.h"

// Тест-кейс "Sum 2 and 3 eq 5"
TEST(Sum_2_and_3_eq_5)
{
    int c = sum(2, 3);
    ASSERT_EQ(5, c);
}

// Тест-кейс "Sum 2 and 3 neq 1337"
TEST(Sum_2_and_3_neq_1337)
{
    int c = sum(2, 3);
    ASSERT_NE(1337, c);
}

int main(int argc, char* argv[])
{
    return run_all_tests();
}
```

### 4. Собрать проект и запустить тесты

Для сборки и запуска проекта необходимо запустить заранее составленные скрипты из командной строки.

#### Windows:

 * Сборка
```sh
build.cmd
```
 * Запуск
```sh
run.cmd
```

#### Linux:

 * Сборка
```sh
sh build.sh
```
 * Запуск
```sh
sh run.sh
```