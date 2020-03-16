Настройка локали нужна, если вместо русского языка отображаются квадратики. Указаны команды, в комментариях после - примерный вывод. Все действия нужно выполнять от пользователя root или перед командой писать sudo.

Если система находится в режиме recovery (а файловая система в состоянии read only), нужно выполнить

```bash
mount -n -o remount,rw /
```

Генерация локали:

```bash
locale-gen ru_RU.UTF-8
# generating locales...
dpkg-reconfigure locales
# в окне enter, enter, пойдёт список en_... done
nano /etc/initramfs-tools/initramfs.conf
```

Добавить в /etc/initramfs-tools/initramfs.conf строку

FRAMEBUFFER=Y

Для выхода из текстового редактора **nano** нажать Ctrl+X, затем Y для принятия изменений.

```bash
update-initramfs -u
# generating /boot/initrd.img...

dpkg-reconfigure console-setup
```
Выбрать UTF-8, потом среди квадратиков 5 строку (где 5 слов на строке, третья после Latin), fixed, 8x16.

Если решение выше не помогло, то среди квадратиков на последнем шаге была выбрана неправильная строка. В /etc/default/console-setup нужно поставить значение CODESET="CyrSlav". Выполнить
```bash
/etc/init.d/console-setup restart
update-initramfs -u
```