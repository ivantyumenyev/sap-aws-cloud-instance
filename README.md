# Установка SAP инстанции на AWS Cloud

1) Заходим на https://cal.sap.com/
2) Для связки с Amazon, переходим в раздел Account и добавляем новый акк от Amazon и указываем Access и Secret Key

![image](https://user-images.githubusercontent.com/14922348/113564124-6106bb00-963b-11eb-998d-1d59c7fddd82.png)


3) Если у вас нет аккаунта IAM, то добавляем его тут https://aws.amazon.com/ru/iam/
  - Необходимо добавить новую группу с правами на
      - AmazonEC2FullAccess
      - AmazonVPCFullAccess
      - ReadOnlyAccess
      - AWSAccountUsageReportAccess
  - Создать пользователя в этой группе
  - Сгенерировать Access и Secret Key. После генерации вам предложат скачать csv-файл со всеми данными

  подронее тут: https://wiki.scn.sap.com/wiki/display/SAPCAL/FAQ+-+Specific+questions+for+Amazon+Web+Services
  
![image](https://user-images.githubusercontent.com/14922348/113563831-f9e90680-963a-11eb-8b19-b1c555e4fe3b.png)

![image](https://user-images.githubusercontent.com/14922348/113563968-28ff7800-963b-11eb-80c0-12670c40b19d.png)


4) Переходим в Solutions и выбираем инстанцию для установки. Например, openSAP: Writing testable ABAP Code

![image](https://user-images.githubusercontent.com/14922348/113564367-dbcfd600-963b-11eb-94a5-fd2ba87beb5a.png)


5) Указываем Account AWS и данные для инстанции

![image](https://user-images.githubusercontent.com/14922348/113564581-32d5ab00-963c-11eb-993b-85f1b142c47d.png)


6) После успешного создания инстанции мы можем подключиться к SAP системе, либо же скачать файл с настройками для подключения
  На странице созданной инстанции по кнопке Getting started доступен мануал по работе с системой https://caldocs.hana.ondemand.com/caldocs/help/Getting_Started_openSAPWritingTestableCode.pdf

![image](https://user-images.githubusercontent.com/14922348/113571885-bfd33100-9649-11eb-88fb-fb9e44362c5e.png)

![image](https://user-images.githubusercontent.com/14922348/113571928-d1b4d400-9649-11eb-93ee-ef0fe8211dfd.png)


7) Теперь мы можем подключиться к созданной инстанции и зайти в SAP. Для подключения к удаленному рабочему столу и входа в SAP используем пароль, который указали при создании инстанции. 

![image](https://user-images.githubusercontent.com/14922348/113577574-0c236e80-9654-11eb-844d-4f2d13c5cc4b.png)

![image](https://user-images.githubusercontent.com/14922348/113578899-1e061100-9656-11eb-96d4-4b1db0236897.png)


8) Регистрируем нашу установленную систему тут: https://go.support.sap.com/minisap/#/minisap

  - Выбираем нужную версию из списка доступных для активации и указываем регистрационные данные. В нашем случае это "NPL - SAP NetWeaver 7.x (Sybase ASE)".
  - Hardware Key берем из транзакции SLICENSE.

Более подробно тут https://wiki.scn.sap.com/wiki/pages/viewpage.action?pageId=526880970

![image](https://user-images.githubusercontent.com/14922348/113579267-9ec50d00-9656-11eb-9b5e-8213e5afb8ed.png)

![image](https://user-images.githubusercontent.com/14922348/113579534-05e2c180-9657-11eb-89b1-d081e475f694.png)


9) После генерации мы получаем текстовый файл NPL.txt. Устанавливаем его в систему с помощью кнопки Install New License.
10) Переходим в тр-цию SECSTORE и запускаем ее выполнение.
11) После использования системы, не забудьте остановить серверы. Иначе у вас быстро набежит счет на оплату.

Сделать это можно из Cloud Application Library в разделе Instances.
Либо в разделе урпавления инстанциями AWS EC2: https://console.aws.amazon.com/ec2/

# Для разработчиков
1) В системе есть пользователь - DEVELOPER. Он зарегистрирован в 001 манданте и доступен по дефолтному паролю. Сразу скажу - у меня не получилось зайти в систему со стандартным паролем.
Поэтому пришлось зайти в 001 под SAP* пользователем и скинуть пароль для DEVELOPER через тр-цию SU01.
2) Про генерацию тестовых данных можно прочитать тут: https://wiki.scn.sap.com/wiki/display/ABAP/Flight+Data+Application+-+Demo+Example+for+Integration+Technologies

Для генерации данных SFLIGHT и SBOOK необходимо запустить программу SAPBC_DATA_GENERATOR.
А для STICKET и SNVOICE - SFLIGHT_DATA_GEN.
