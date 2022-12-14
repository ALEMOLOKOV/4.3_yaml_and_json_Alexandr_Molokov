# 4.3_yaml_and_json_Alexandr_Molokov
4.2 Языки разметки YAML и JSON

# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
#Исправленный вариант
    { "info" : "Sample JSON output from our service\\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : "71.75.22.42"
            },
            { "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"
            }
        ]
    }
```
  Нужно найти и исправить все ошибки, которые допускает наш сервис

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import socket
import time
import json
import yaml

hosts = {"drive.google.com": "0.0.0.0", "mail.google.com": ".0.0.0.0", "google.com": "0.0.0.0"}
while True:
    for url, ip in hosts.items():
        ip_addr = socket.gethostbyname(url)
        if ip == "":
            hosts[url] = ip_addr
            print("{} - {}".format(url, ip_addr))
        elif ip != ip_addr:
            print("[ВНИМАНИЕ] {} НЕСООТВЕТСИВЕ IP: СТАРЫЙ IP {} НОВЫЙ IP {}".format(url, ip, ip_addr))
            hosts[url] = ip_addr
        with open('hosts.json', 'w') as json_file:
            json_file.write(json.dumps(hosts, indent=2))
        with open('hosts.yaml', 'w') as yaml_file:
            yaml_file.write(yaml.dump(hosts, indent=2, explicit_start=True, explicit_end=True))
    time.sleep(2)
```

### Вывод скрипта при запуске при тестировании:
```
"C:\Netology\Python\Scripts\virtual interpretator\Scripts\python.exe" C:/Netology/Python/Scripts/2_task.py
[ВНИМАНИЕ] drive.google.com НЕСООТВЕТСИВЕ IP: СТАРЫЙ IP 0.0.0.0 НОВЫЙ IP 74.125.131.194
[ВНИМАНИЕ] mail.google.com НЕСООТВЕТСИВЕ IP: СТАРЫЙ IP .0.0.0.0 НОВЫЙ IP 216.58.209.165
[ВНИМАНИЕ] google.com НЕСООТВЕТСИВЕ IP: СТАРЫЙ IP 0.0.0.0 НОВЫЙ IP 216.58.210.142
[ВНИМАНИЕ] drive.google.com НЕСООТВЕТСИВЕ IP: СТАРЫЙ IP 74.125.131.194 НОВЫЙ IP 64.233.164.194
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
{
  "drive.google.com": "64.233.164.194",
  "mail.google.com": "216.58.209.165",
  "google.com": "216.58.210.142"
}
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
---
drive.google.com: 64.233.164.194
google.com: 216.58.210.142
mail.google.com: 216.58.209.165
...

```

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

Так как команды в нашей компании никак не могут прийти к единому мнению о том, какой формат разметки данных использовать: JSON или YAML, нам нужно реализовать парсер из одного формата в другой. Он должен уметь:
   * Принимать на вход имя файла
   * Проверять формат исходного файла. Если файл не json или yml - скрипт должен остановить свою работу
   * Распознавать какой формат данных в файле. Считается, что файлы *.json и *.yml могут быть перепутаны
   * Перекодировать данные из исходного формата во второй доступный (из JSON в YAML, из YAML в JSON)
   * При обнаружении ошибки в исходном файле - указать в стандартном выводе строку с ошибкой синтаксиса и её номер
   * Полученный файл должен иметь имя исходного файла, разница в наименовании обеспечивается разницей расширения файлов

### Ваш скрипт:
```python
???
```

### Пример работы скрипта:
???
