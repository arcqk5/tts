# tts
**Отчёт**

**Оглавление**
1. Цель работы
2. Установка Debian 10
3. Настройка Debian 10
4. Установленное ПО
5. Используемая литература

**Цель работы**

В данной лабораторной работе необходимо установить ОС Debian 10 и настроить её для дальнейшего использования.

**Установка Debian 10**

На первых шагах установки выбираются язык системы и регион. Далее указывается имя системы, имя пользователя и пароль:

![enter_username](/uploads/7c27e0ec369d2ba6c472ee551b6d7f8c/enter_username.png)

Затем переходим к разметке диска системы:

![partition](/uploads/3a89a3dadf12a4e8d9ee389f853d5f0e/partition.png)

Устанавливаем GRUB и выбираем ПО, необходимое нам для дальнейшей работы:

![preinstalled_software](/uploads/b59b02afe1f9e53997f0823ad3839388/preinstalled_software.png)

**Настройка Debian 10**

Перенесём раздел /tmp в оперативную память. Для этого изменим файл /etc/fstab:

![etc_fstab](/uploads/90d2e813c8f9c2b8676e641aa78e2cca/etc_fstab.png)

Перезапустим систему и убедимся, что изменения вступили в силу:

![tmp](/uploads/6ef1d083e2c6f2ae3301ce10a83f5c0e/tmp.png)

Генерируем ключ для ssh сервера:

`$ ssh-keygen`

Отправляем сгенерированный ключ на ssh сервер:

`$ ssh-copy-id bezzubenko-a@192.168.43.179`

Для входа на сервер без запроса пароля необходимо в файле конфигурации сервера прописать пользователя, который сможет иметь доступ к серверу.

Для этого зайдём в файл с конфигурацией сервера:

`$ sudo nano /etc/ssh/sshd_config`

И сохраним там следующие строки:

PasswordAuthentication no - вход без запроса пароля;

AllowUsers bezzubenko-a - пользователи, имеющие доступ к серверу.

![sshd_config](/uploads/db07986603e62a481eae51f09f9e3e01/sshd_config.png)

Проверим работу сервера:

![SSH](/uploads/cb54f4e7ff59a849403eb6223de59b60/SSH.png)

После настройки сервера создадим группу:

`$ sudo groupadd iu8-61`

И добавим в неё пользователя:

`$ sudo usermod -g iu8-61 bezzubenko-a`

Проверим принадлежность пользователя к созданной группе:

![group](/uploads/e19529196bc97a1787e7ac0cc3804dd8/group.png)

**Установленное ПО**

Установим Visual Studio Code:

```
$ sudo apt update 

$ sudo apt install software-properties-common apt-transport-https curl

$ curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

$ sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"

$ sudo apt update

$ sudo apt install code
```

![VS_code](/uploads/88d9fc781f7c08c7fd48a0a5409f692f/VS_code.png)

**Вывод**

В данной лабораторной работе была установлена и настроена ОС Debian 10. Также был настроен SSH сервер и установлена среда разработки исходного кода Visual Studio Code.

**Используемые источники**

1. https://routerus.com/how-to-install-visual-studio-code-on-debian-10/
2. https://vds-admin.ru/ssh/nastroika-servera-ssh-vo-freebsd-fail-sshdconfig
3. https://hackware.ru/?p=9906
