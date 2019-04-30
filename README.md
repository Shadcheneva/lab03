
# Объявление Необходимых переменных
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>

# присвоение edit вызов удобного текстового редактора
$ alias edit=<nano|vi|vim|subl>

# переход в рабочую директорию
$ cd ${GITHUB_USERNAME}/workspace

# исполнение кода из файла activate
$ source scripts/activate

# создание директории
$ mkdir ~/.config

# запись текста до EOF в файл hub
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF

# установка параметров протокола гит
$ git config --global hub.protocol https

# создание новой директории lab02 и переход в нее
$ mkdir projects/lab02 && cd projects/lab02

# Создание гит-репозитория из этого каталога
$ git init

# Установка необходимых параметров гит(имя пользователя, е-маil)
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
#  check your git global settings
$ git config -e --global


# Добавление удалённого гит-репозиторий под именем-сокращением, к которому будет проще обращаться
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git

# Добавление в локальный сервер последнюю версию кода
$ git pull origin master

# создание нового файла
$ touch README.md

# Текущее состояние репозитория
$ git status

# Добавление файла в репозиторий
$ git add README.md

# сделать коммит с подписью "added README.md"
$ git commit -m "added README.md"

# слияние локального репозитория с гитхаб репозиторием
$ git push origin master


Добавить на сервисе GitHub в репозитории lab02 файл .gitignore со следующем содержимом:

*build*/
*install*/
*.swp
.idea/




# Добавление в локальный сервер последнюю версию кода
$ git pull origin master

# история изменений
$ git log

# Создание директорий
$ mkdir sources
$ mkdir include
$ mkdir examples

# создание и запись в файл print.cpp до EOF
$ cat > sources/print.cpp <<EOF
# include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF

# создание и запись в файл print.hpp до EOF
$ cat > include/print.hpp <<EOF
# include <fstream>
# include <iostream>
# include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF

# создание и запись в файл example1.cpp до EOF
$ cat > examples/example1.cpp <<EOF
# include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF

# создание и запись в файл example2.cpp до EOF
$ cat > examples/example2.cpp <<EOF
# include <print.hpp>

# include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF

# Редактирования файла
$ edit README.md

# текущее состояние репозитория
$ git status

# 
$ git add .

# Коммит с подписью " added sources"
$ git commit -m" added sources"

# слияние локального репозитория с гитхаб репозиторием
$ git push origin master