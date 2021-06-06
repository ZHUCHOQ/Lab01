# Отчет по лабораторной работе № 1

### Цель работы 

Данная лабораторная работа посвящена изучению утилит для разработки проектов

### Задания

1. Ознакомиться со ссылками учебного материала
2. Выполнить инструкцию учебного материала
3. Составить отчет и отправить ссылку личным сообщением в **Slack**

### Команды, выполненные в ходе выполнения лабораторной работы

```bash
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GIST_TOKEN=<сохраненный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```sh
$ mkdir -p ${GITHUB_USERNAME}/workspace
$ cd ${GITHUB_USERNAME}/workspace
$ pwd
$ cd ..
$ pwd
```

```sh
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
$ cd workspace
```

```sh
# Debian
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
$ tar -xf node-v6.11.5-linux-x64.tar.xz
$ rm -rf node-v6.11.5-linux-x64.tar.xz
$ mv node-v6.11.5-linux-x64 node
```

```sh
$ ls node/bin
$ echo ${PATH}
$ export PATH=${PATH}:`pwd`/node/bin
$ echo ${PATH}
$ mkdir scripts
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
$ source scripts/activate
```

```sh
$ gem install gist
```

```sh
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```

```sh
$ export LAB_NUMBER=01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

### Выполнение домашнего задания:

1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.

![llOW0IIYtoA](https://user-images.githubusercontent.com/84859324/120928568-d4858100-c6ed-11eb-852e-21e1caa27297.jpg)


2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`

```sh
    $ tar -xvf boost_1_69_0.tar.gz
```

3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.

![OKGX7PV1LVI](https://user-images.githubusercontent.com/84859324/120928578-dcddbc00-c6ed-11eb-9206-28ecbf30e66a.jpg)


4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.

```sh
    $ tree . | tail -n 1
    5637 directories, 61191 files
```

5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).

```sh
    $ find . \( -name '*.h' -o -name '*.hpp' \) -type f | wc -l
    15208
```

```sh
    $ find . -name '*.cpp' -type f | wc -l
    13774
```

```sh
    $ find . -type f | grep -vc -E '*.cpp|*.h|*.hpp'
    6800
```

6. Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.

```sh
    $ find . -name 'any.hpp'

	./boost/any.hpp
	./boost/spirit/home/support/algorithm/any.hpp
	./boost/hana/any.hpp
	./boost/hana/fwd/any.hpp
	./boost/type_erasure/any.hpp
	./boost/xpressive/detail/utility/any.hpp
	./boost/proto/detail/any.hpp
	./boost/fusion/algorithm/query/any.hpp
	./boost/fusion/algorithm/query/detail/any.hpp
	./boost/fusion/include/any.hpp
```

7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.

```sh
	$ grep -rl boost::asio .

	./boost/log/sinks/syslog_backend.hpp
	./boost/process/async_system.hpp
	./boost/process/system.hpp
    ...
    ./doc/html/boost_process/extend.html
    ./doc/html/boost_process/tutorial.html
    ./doc/html/process/reference.html
```

8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.

```sh
    $ mv * ~/boost-libs/
```

10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.

```sh
    $ du -h
```

11. Найдите *топ10* самых "тяжёлых".

```sh
	$ find . -type f -exec du {} + | sort -rn | head
	4624	./lib/libboost_wave.a
	4336	./lib/libboost_log.a
	3384	./lib/libboost_locale.a
	3268	./lib/libboost_regex.a
	2864	./lib/libboost_math_tr1.a
	2832	./lib/libboost_math_tr1l.a
	2784	./lib/libboost_math_tr1f.a
	2680	./lib/libboost_log_setup.a
	2332	./lib/libboost_test_exec_monitor.a
	2316	./lib/libboost_unit_test_framework.a
```

