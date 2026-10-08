# Bash scripting
## Скрипты

| Файл | Описание |
| :--- | :--- |
| 1.sh | Приветствие |
| 2.sh | Сумма двух чисел |
| 3.sh | Проверка на чётность |
| 4.sh | Структура веб-проекта |
| 5.sh | Подсчёт строк в файле |
| 6.sh | Генератор пароля |
| 7.sh | Поиск файлов по расширению |
| 8.sh | GitHub Repository Analyzer |
## Запуск
```
cd bashScripting
bash 1.sh
```
Остальные скрипты запускаются так же: bash 2.sh, bash 3.sh и т.д. Для 8.sh нужно указать репозиторий:
```
bash 8.sh torvalds/linux
```
## 1.Приветствие
Скрипт спрашивает имя и здоровается.
```
#!/bin/bash
# Спрашиваем имя и здороваемся
echo "Как вас зовут?"
read name
echo "Привет, $name!"
```
Скриншот вывода:
```
```
## 2. Сумма двух чисел
Скрипт просит ввести два числа и выводит их сумму.
```
#!/bin/bash
# Сумма двух чисел
read -p "Введите первое число: " a
read -p "Введите второе число: " b
sum=$((a + b))
echo "Сумма: $sum"
```
Скриншот вывода:
```
```
## 4. Структура веб-проекта
Скрипт создаёт папки css, js, img и файл index.html.
```
#!/bin/bash
# Создаём папки для веб-проекта
mkdir -p myproject/css
mkdir -p myproject/js
mkdir -p myproject/img
touch myproject/index.html
echo "Структура проекта создана:"
ls -R myproject
```
Скриншот вывода:
```
```
## 5. Подсчёт строк в файле
Скрипт считает, сколько строк в файле.
```
#!/bin/bash
# Считаем строки в файле
read -p "Введите имя файла: " filename

if [ -f "$filename" ]; then
    lines=$(wc -l < "$filename")
    echo "В файле '$filename' строк: $lines"
else
    echo "Файл '$filename' не найден"
fi
```
Скриншот вывода:
```
```
## 6. Генератор пароля
Скрипт создаёт случайный пароль из 8 символов.
```
#!/bin/bash
# Генератор пароля из 8 символов
password=$(tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 8)
echo "Ваш пароль: $password"
```
Скриншот вывода:
```
```
## 7. Поиск файлов по расширению
Скрипт ищет в текущей папке файлы с нужным расширением.
```
#!/bin/bash
# Поиск файлов по расширению в текущей папке
read -p "Введите расширение (например txt): " ext

echo "Найденные файлы:"
ls *.$ext 2>/dev/null

if [ $? -ne 0 ]; then
    echo "Файлов с расширением .$ext нет"
fi
```
Скриншот вывода:
```
```
## 8. GitHub Repository Analyzer
Скрипт показывает звёзды, форки и issues репозитория через GitHub API. Нужен curl.
```
#!/bin/bash
# Статистика репозитория GitHub (нужен curl)
# Запуск: bash 8.sh tensorflow/tensorflow

repo=$1

if [ -z "$repo" ]; then
    echo "Укажите репозиторий, например: bash 8.sh torvalds/linux"
    exit 1
fi

data=$(curl -s "https://api.github.com/repos/$repo")

if [ -z "$data" ]; then
    echo "Нет интернета"
    exit 1
fi

if echo "$data" | grep -q '"message": "Not Found"'; then
    echo "Репозиторий $repo не найден"
    exit 1
fi

if echo "$data" | grep -q "rate limit"; then
    echo "Превышен лимит запросов, попробуйте позже"
    exit 1
fi

stars=$(echo "$data" | grep -m1 '"stargazers_count"' | tr -dc '0-9')
forks=$(echo "$data" | grep -m1 '"forks_count"' | tr -dc '0-9')
issues=$(echo "$data" | grep -m1 '"open_issues_count"' | tr -dc '0-9')

YELLOW='\033[33m'
GREEN='\033[32m'
RED='\033[31m'
NC='\033[0m'

echo "Репозиторий: $repo"
echo -e "Звёзды: ${YELLOW}$stars${NC}"
echo -e "Форки: ${GREEN}$forks${NC}"

if [ "$issues" -gt 100 ]; then
    echo -e "Issues: ${RED}$issues${NC}"
else
    echo -e "Issues: ${YELLOW}$issues${NC}"
fi
```
Скриншот вывода:
```
```
## Вывод
Я научился писать простые скрипты на Bash: вводить данные через read, использовать переменные, условия if и команды вроде mkdir, wc, tr и curl.





