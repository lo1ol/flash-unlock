# flash-unlock
Скрипты для настройки загрузки с защищенного носителя Rutoken ЭЦП Flash 2.0. Настройка првоерена на ОС Astra Linux и Ubuntu.

# Описание настройки
Установите зависимые пакеты:
```bash
sudo apt-get install opensc libpcsclite1 pcscd
```

Cкопируйте содержимое репозитория в дирректорию _/usr/share/initramfs-tools_ и пересоберите initrd:
```bash
sudo cp -r * /usr/share/initramfs-tools
sudo update-initramfs -u
```

## Настройка для загрузки с raed-only корня
Для загрузки с read-only корня вам дополнительно необходимо настроить overlay. 
* В Astra Linux для сборки initrd с включенным overlay над корнем используется команда:
```bash
astra-overlay enable
```
* В Ubuntu для сборки initrd с поддержкой overlay необзходимо поставить пакет **overlayroot**, настроить его и затем вручную пересобрать initrd. Подробности по настройке можно найти [здесь](https://spin.atomicobject.com/2015/03/10/protecting-ubuntu-root-filesystem/).

---
**Примечания**
* Активировать overlay рекомендуется после того, как система окончательно настроена.
* Если в */etc/fstab* присутсвуют разделы, которые после загрузки будут read-only, вероятно к ним нужно добавить опции *nofail*, *noload*(для ext4) и *errors=remount-ro* при монтировании.
* Для графического запроса ПИН-кода убедитесь, что при загрузке ядру передается аргумент splash, а plymouth сконфигурирован на использовании GUI темы.
* grub не использует файлы с закрытых разделов, например, картинку для фона
--



