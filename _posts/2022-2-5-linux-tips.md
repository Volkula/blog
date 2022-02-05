---
layout: post
title: Полезное в linux
---

![image](https://user-images.githubusercontent.com/2937856/152644246-1d4ebd30-269a-4f51-a04c-3fabebfa071f.png)

Интересные, важные и полезные моменты моей линуксовой жизни.

___
## Удалить строки С № и ПО №

```bash
for line in $(seq 1800 1815) ; do history -d 1800; done
```

___
## Установка ~oh-my-zsh

```bash
yum install zsh -y
chsh -s /bin/zsh root
echo $SHELL
yum install wget git -y
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh

/bin/cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
source ~/.zshrc

vi ~/.zshrc
```

> Моя любимая тема - candy. Превью всех стандартных тем - [тут](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

___
## Релоад отдельного компонента gitlab

```bash
gitlab-cli reload <component>
gitlab-cli reconfigure
```

___
## Посчитать колличество процессов

```bash
watch -n 1 "echo -n 'Apache Processes: ' && ps -C apache2 --no-headers | wc -l && free -m"
```

___
## Отправить сообщение боту в канал

```bash
#!/bin/sh
TOKEN="---"
CHAT_ID="----"
curl    -X POST \
        -H 'Content-Type: application/json' \
        -d '{"chat_id": "----", "text": "*ololo* ", "disable_notification": true}' \
        -d "parse_mode='Markdown'"\
        https://api.telegram.org/bot$TOKEN/sendMessage
```

___
## Почти 100% способ определить, ОС на виртуалке или на железе:

```vi
Команда dmidecode
там есть блок:
System Information
        Manufacturer: Dell Inc.
        Product Name: PowerEdge R610
        Version: Not Specified
        Serial Number: BGB2W4J
        UUID: 4c4c4544-0047-4210-8032-c2c04f57344a
        Wake-up Type: Power Switch
        SKU Number: Not Specified
        Family: Not Specified

System Information
        Manufacturer: Red Hat
        Product Name: KVM
        Version: RHEL 7.5.0 PC (i440FX + PIIX, 1996)
        Serial Number: Not Specified
        UUID: 6a4ab549-9332-4741-8397-34c2eea7dd82
        Wake-up Type: Power Switch
        SKU Number: Not Specified
        Family: Red Hat Enterprise Linux
```

___
## Сменить пароль пользователю в MySQl

```sql
ALTER USER 'exporter'@'localhost' IDENTIFIED BY '123456';
```

___
## Установка расширения vscode для подключения по ssh к удаленному хосту

1) Установить [Remote-SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) плагин
2) [Save-as-root](https://marketplace.visualstudio.com/items?itemName=yy0931.save-as-root) дополнение ДЛЯ КАЖОГО ХОСТА. И настроить хоткей.

___
## Как качать курлом из гуглодиска:

```bash
curl gdrive.sh | bash -s 1BIZY9OzLnQRuLoseGiB1uobxxTJLn4ix
```

> Где id берётся из публичной ссылки на файл
