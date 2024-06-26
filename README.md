# Домашнее задание к занятию "`Система мониторинга Zabbix. Часть 2`" - `Тен Денис`


В практике есть 4 основных и 5 дополнительных (со звездочкой) заданий. Основные задания нужно выполнять обязательно, со звездочкой - по желанию и его решение никак не повлияет на получение вами зачета по этому домашнему заданию, при этом вы сможете глубже и/или шире разобраться в материале. 

Пожалуйста, присылайте на проверку все задачи сразу. Любые вопросы по решению задавайте в чате учебной группы.

### Цели задания
1. Научитья создавать свои шаблоны в Zabbix, добавлять в Zabbix хосты и связывать шаблон с хостами
2. Научиться составлять кастомный дашборд
3. Научиться создавать UserParameter на Bash
4. Научиться создавать Python-скрип, добавляться в него UserParameter и прикреплять к шаблону
5. Научиться создавать Vagrant-скрипты для Zabbix Agent

### Чеклист готовности к домашнему заданию
- [ ] Просмотрите в личном кабинете занятие "Система мониторинга Zabbix. Часть 2" 

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

 ---

### Задание 1
Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. В веб-интерфейсе Zabbix Servera в разделе Templates создайте новый шаблон
3. Создайте Item который будет собирать информацию об загрузке CPU в процентах
4. Создайте Item который будет собирать информацию об загрузке RAM в процентах

#### Требования к результату
- Прикрепите в файл README.md скриншот страницы шаблона с названием «Задание 1»

#### Решение Задание 1
Не нашел способа кроме как собрать информацию о загрузки CPU через UserParameter
```
UserParameter=ram.load.percentage,free -m | awk 'NR==2{printf "%.2f", ($2-$NF)/$2*100}'
```
![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/3327ddd3-e2b0-4aa9-93dd-04b503cc1476)
![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/f970f9c8-537a-4c45-95a6-1b1ba2fc314a)
![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/885e8197-d50f-48d7-aeea-cfa0e028e2ef)
![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/77b0133e-03be-4473-9790-7aa17c150d5d)

 ---

### Задание 2
Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
5. Прикрепите за каждым хостом шаблон Linux by Zabbix Agent
6. Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

#### Требования к результату
- Результат данного задания сдавайте вместе с заданием 3 
### Решение Задание 2

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/bd85f93a-084e-411d-9614-f7e3a4d77bf0)

 ---

### Задание 3
Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Зайдите в настройки каждого хоста и в разделе Templates прикрепите к этому хосту ваш шаблон
3. Так же к каждому хосту привяжите шаблон Linux by Zabbix Agent
4. Проверьте что в раздел Latest Data начали поступать необходимые данные из вашего шаблона

#### Требования к результату
- [ ] Прикрепите в файл README.md скриншот страницы хостов, где будут видны привязки шаблонов с названиями «Задание 2-3». Хосты должны иметь зелёный статус подключения

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/7e6a4799-5468-4d95-afb9-f65d811aa6a5)

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/e419573f-c70c-4aae-9893-2de30d00de12)


### Задание 4
Создайте свой кастомный дашборд.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. В разделе Dashboards создайте новый дашборд
3. Разместите на нём несколько графиков на ваше усмотрение.

#### Требования к результату
- [ ] Прикрепите в файл README.md скриншот дашборда с названием «Задание 4»

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/da271135-2047-4fd2-a28b-420007fc3588)

 ---

### Задание 5* со звёздочкой
Создайте карту и расположите на ней два своих хоста.

#### Процесс выполнения
1. Настройте между хостами линк.
2. Привяжите к линку триггер, связанный с agent.ping одного из хостов, и установите индикатором сработавшего триггера красную пунктирную линию.
3. Выключите хост, чей триггер добавлен в линк. Дождитесь срабатывания триггера.

#### Требования к результату
- [ ] Прикрепите в файл README.md скриншот карты, где видно, что триггер сработал, с названием «Задание 5» 


### Решение Задание 5* со звёздочкой

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/7820c880-9269-4416-b533-221cabb236f5)


![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/2d4cba69-7ed5-4e2a-a384-4b34f466aae2)

Тест отключение хоста tenda-2

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/267edb60-9238-4c26-9e90-d2bf0c88b054)



 ---

### Задание 6* со звёздочкой
Создайте UserParameter на bash и прикрепите его к созданному вами ранее шаблону. Он должен вызывать скрипт, который:
- при получении 1 будет возвращать ваши ФИО,
- при получении 2 будет возвращать текущую дату.

#### Требования к результату
- [ ] Прикрепите в файл README.md код скрипта, а также скриншот Latest data с результатом работы скрипта на bash, чтобы был виден результат работы скрипта при отправке в него 1 и 2

```
vim /etc/zabbix_agentd.conf.d/userparameter_script.sh  
#!/bin/bash
   if [ "$1" = "1" ]; then
       echo "Denis Ten"
   elif [ "$1" = "2" ]; then
       date +"%Y-%m-%d"
   fi
```
Настройка zabbix-agent
```
vim /etc/zabbix_agentd.conf
Include=/etc/zabbix_agentd.conf.d/*.conf
UnsafeUserParameters=1
UserParameter=my_script[*],/etc/zabbix_agentd.conf.d/userparameter_script.sh $1
```

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/c8a9dc33-19d7-427a-bd73-99ad86ffa444)

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/ec6d4671-5851-4a59-83e6-92142877e6a9)

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/e7b2c757-5270-4734-8a17-0ed100599f75)

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/49b29793-fafa-4761-aee3-e2a5376275b6)



 ---

### Задание 7* со звёздочкой
Доработайте Python-скрипт из лекции, создайте для него UserParameter и прикрепите его к созданному вами ранее шаблону. 
Скрипт должен:
- при получении 1 возвращать ваши ФИО,
- при получении 2 возвращать текущую дату,
- делать всё, что делал скрипт из лекции.

- [ ] Прикрепите в файл README.md код скрипта в Git. Приложите в Git скриншот Latest data с результатом работы скрипта на Python, чтобы были видны результаты работы скрипта при отправке в него 1, 2, -ping, а также -simple_print.*


```
vim /etc/zabbix_agentd.conf.d/my_python_script.py
import sys
import os
import re
if (sys.argv[1] == '-ping'): # Если -ping
    result=os.popen("ping -c 1 " + sys.argv[2]).read() # Делаем пинг по заданному адресу
    result=re.findall(r"time=(.*) ms", result) # Выдёргиваем из результата время
    print(result[0]) # Выводим результат в консоль
elif (sys.argv[1] == '-simple_print'): # Если simple_print
    print(sys.argv[2]) # Выводим в консоль содержимое sys.arvg[2]
else: # Во всех остальных случаях
    print(f"unknown input: {sys.argv[1]}") # Выводим непонятый запрос в консоль
```

```
vim /etc/zabbix_agentd.conf
UserParameter=my_python_script[*], python3 /etc/zabbix_agentd.conf.d/my_python_script.py $1 $2
```

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/ea27b77e-00e4-4bfe-9ffb-0e3442aff0ff)


 ---

### Задание 8* со звёздочкой

Настройте автообнаружение и прикрепление к хостам созданного вами ранее шаблона.

#### Требования к результату
- [ ] Прикрепите в файл README.md скриншот правила обнаружения, а также скриншот страницы Discover, где видны оба хоста.*

### Решение Задание 8* со звёздочкой

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/23f1e7ff-f45c-42da-9dbc-4afa59324b21)

![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/3eae3963-d3d2-4317-9473-3268fd280b55)
![image](https://github.com/killakazzak/hw-02-zabbix-02/assets/32342205/4211fea8-e248-4cfb-91c3-423be7e7f39a)



 ---

### Задание 9* со звёздочкой

Доработайте скрипты Vagrant для 2-х агентов, чтобы они были готовы к автообнаружению сервером, а также имели на борту разработанные вами ранее параметры пользователей.

- [ ] Приложите в GitHub файлы Vagrantfile и zabbix-agent.sh.*

## Критерии оценки

1. Выполнено минимум 4 обязательных задания
2. Прикреплены требуемые скриншоты, код и файлы 
3. Задание оформлено в шаблоне с решением и опубликовано на GitHub
