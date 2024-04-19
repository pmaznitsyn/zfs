Репозиторий для создания с помощью vagrant образа виртуальной машины с развернутым zfs. Образ разворачивается на базе AlmaLinux8, к образу добавляется
 8 дисков по 100Мб, из них собирается 4 файловые системы в "зеркале" (mirror) и монтируются в каталоги /otus{1-4}. Для настройки виртуальной машины 
 используется скрипт setup_zfs.sh, в котором устанавливается пакет zfs, загружается модуль ядра, и создаются 4 зеркальных пула.
 В файле typescript вывод команд из консоли виртуальной машины по выполнению заданий.    