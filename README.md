# otus_lesson1

Занятие 1. Обновление ядра системы
Цель домашнего задания
Научиться обновлять ядро в ОС Linux.
Описание домашнего задания
1) Запустить ВМ c Ubuntu.
2) Обновить ядро ОС на новейшую стабильную версию из mainline-репозитория.
3) Оформить отчет в README-файле в GitHub-репозитории.

Дополнительное задание:
Собрать ядро самостоятельно из исходных кодов.

Ход выполнения:


Смотрим какая версия ядра установленная в ОС.
Для этого используем утилиту uname c ключем -r
<img width="598" height="100" alt="image" src="https://github.com/user-attachments/assets/19b148a3-0b69-4961-9873-a30b5a9e041c" />


А также можно использовать менеджер пакетов dpkg c ключем -l для просмотра установленных пакетов с помощью утилиты grep отфильтруем 
 <img width="958" height="155" alt="image" src="https://github.com/user-attachments/assets/67407c7b-b9c2-492e-9954-92ddd667ac89" />


Далее зайдём браузеров в репозиторий, где найдём свежую версию ядра для нашей архитектуры https://kernel.ubuntu.com/mainline .

Видим самую свежую версию ядра.
 <img width="974" height="650" alt="image" src="https://github.com/user-attachments/assets/6018b096-e42e-48a8-b458-dde4c9128516" />


Узнаем архитектуру процессора uname -p или hostnamectl
<img width="720" height="506" alt="image" src="https://github.com/user-attachments/assets/1dfd1354-4240-48cc-957f-f054a2780844" />

 
3.Находим актуальную ссылку и качаем пакеты на виртуальную машину  в заранее созданную директорию kernel

mkdir kernel && cd kernel

 <img width="603" height="156" alt="image" src="https://github.com/user-attachments/assets/854b5c76-325a-4450-92bb-995f10175145" />




Для того чтобы не качать пакеты несколько раз можно создать текстовый файл со списком ссылок например urlkernel.txt для этого я буду использовать текстовый редактор nano

 <img width="850" height="183" alt="image" src="https://github.com/user-attachments/assets/f9c6b4a7-8f63-4878-9a75-5998e8c45d83" />

<img width="974" height="169" alt="image" src="https://github.com/user-attachments/assets/74656d84-c270-4434-96ab-93a0119aca2d" />

 


Качаем пакеты wget -i urlkernel.txt

 <img width="974" height="655" alt="image" src="https://github.com/user-attachments/assets/9b6b4baf-f02d-49aa-8832-8eb1942d5100" />


Проверяем  ls
 <img width="974" height="160" alt="image" src="https://github.com/user-attachments/assets/f29bf683-daff-41a7-9e03-5a8cce15ab2f" />

Устанавливаем все пакеты сразу:

sudo dpkg -i *.deb
Проверяем установленные пакеты dpkg -l | grep linux-
<img width="974" height="419" alt="image" src="https://github.com/user-attachments/assets/d27caa19-2868-4bc8-9701-107b1e69c20d" />

 
Проверяем, что ядро появилось в /boot.
Ls -all /boot
 <img width="974" height="380" alt="image" src="https://github.com/user-attachments/assets/f28b1b6a-92f8-4706-85f7-08bf5568fc4c" />


Уже на этом этапе можно перезагрузить нашу виртуальную машину и выбрать новое ядро при загрузке ОС. 
Если требуется, можно назначить новое ядро по умолчанию вручную:
1) Обновить конфигурацию загрузчика:
[db@server ~]$ sudo update-grub
2) Выбрать загрузку нового ядра по-умолчанию:
   	[db@server ~]$ sudo grub-set-default 0

 <img width="974" height="307" alt="image" src="https://github.com/user-attachments/assets/b5ff1f8d-d5e9-45ff-9414-2a9615fea5e5" />

Перезагружаем
sudo reboot
Проверяем

 <img width="520" height="122" alt="image" src="https://github.com/user-attachments/assets/b2266406-d6d7-4518-90f5-869f04db4039" />



