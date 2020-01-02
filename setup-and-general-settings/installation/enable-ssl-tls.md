---
description: Инструкция по запуску интерфейса браузера Gunbot через безопасное соединение.
---

# Как включить SSL/TLS

## Запустить GUI на HTTPS с самоподписанным сертификатом.

Для запуска графического интерфейса по https вам понадобится сертификат. Ниже приведены инструкции по созданию самоподписанного сертификата в Windows, Mac и Linux.

{% hint style="info" %}
Сертификаты от обычных поставщиков SSL также считаются действительными. Следует переименовать файлы, и измените расширения файлов на .crt и .key, затем поместите файлы в папку Gunbot.
{% endhint %}

Убедитеcь, что параметр`https` имеет значение `true` в файле `config.js` для того чтобы включить https после создания сертификата.

При первом подключении к графическому интерфейсу вы, вероятно, увидите предупреждение браузера, появляющееся из-за использования самоподписанного сертификата. Создайте постоянное исключение, что позволит отключить появление предупреждения снова в том же браузере.

### **Windows**

1. [Скачайте](https://slproweb.com/products/Win32OpenSSL.html) и установите OpenSSL для Windows
2. Перейдите в следующую папку: C:\OpenSSL-Win64 bin\
3. Щелкните правой кнопкой мыши «openssl» для запуска от имени администратора. После чего откроется окно cmd
4. Выполните следующую команду: `req -newkey rsa:2048 -nodes -keyout localhost.key -x509 -days 365 -out localhost.crt` \(вам будет предложено заполнить форму, вы можете сделать это или оставить поля пустыми, нажав Enter несколько раз\)
5. Скопируйте файлы`localhost.key` и `localhost.crt` из C:\OpenSSL-Win64\bin в директорию Gunbot

### **Mac**

1. Open a terminal window and navigate to your Gunbot folder
2. Run the following command `openssl req -newkey rsa:2048 -nodes -keyout localhost.key -x509 -days 365 -out localhost.crt` and make sure to enter the country code field. The rest can be left blank

### **Linux**

1. Open a terminal window and navigate to your Gunbot folder. Possibly you'll need to install openssl through your package manager first.
2. Run the following command `openssl req -newkey rsa:2048 -nodes -keyout localhost.key -x509 -days 365 -out localhost.crt` and make sure to enter the country code field. The rest can be left blank.

