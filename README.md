# ALT Linux Lab Setup (ISP / SRV / CLI)

Шпаргалка по настройке лабораторного стенда на ALT Linux: **маршрутизатор (ISP)**, **сервер (SRV)** и **клиент (CLI)**.  
Внутри — пошаговые команды для сети, DHCP, NAT, RAID5, NFS, SSH и Samba AD DC.

> Основной гайд лежит в файле **[SETUP.md](SETUP.md)**. fileciteturn0file0L1-L4

---

## Что в гайде

- Топология и интерфейсы (ISP/SRV/CLI) fileciteturn0file0L5-L16  
- ISP: статический LAN + IPv4 forwarding fileciteturn0file0L20-L55  
- ISP: DHCP-сервер (включая фиксированный IP для SRV по MAC) fileciteturn0file0L59-L114  
- ISP: NAT через iptables fileciteturn0file0L118-L162  
- SRV: DHCP-интерфейс fileciteturn0file0L166-L177  
- SRV: RAID5 (mdadm) + ФС + fstab fileciteturn0file0L181-L229  
- SRV: NFS-сервер + экспорт fileciteturn0file0L233-L279  
- CLI: монтирование NFS fileciteturn0file0L283-L332  
- SSH: отдельные порты, ключи, алиасы, запрет паролей fileciteturn0file0L336-L450  
- Samba AD DC: домен `ilove.sa`, пользователи/группы, join клиента fileciteturn0file0L454-L614  
- Дополнительно: правила FORWARD (если нужно ограничивать трафик) fileciteturn0file0L618-L650  

---

## Быстрый старт

1) Открой **SETUP.md** и иди по шагам сверху вниз:  
   - сначала **ISP** (LAN → forwarding → DHCP → NAT) fileciteturn0file0L20-L162  
   - затем **SRV** (DHCP → RAID5 → NFS → SSH → Samba DC) fileciteturn0file0L166-L569  
   - потом **CLI** (NFS mount → SSH config → join в домен) fileciteturn0file0L283-L614  

2) Если делаешь SSH “как в шпоре”:
   - ISP: порт **2222**, SRV: порт **2223**, только ключи fileciteturn0file0L402-L449  
   - на CLI — алиасы `ISP` и `srv` в `~/.ssh/config` fileciteturn0file0L366-L400  

---

## Требования и допущения

- Используются роли машин: **ISP / SRV / CLI** fileciteturn0file0L1-L4  
- Подсеть: `10.0.128.0/24`, ISP LAN: `10.0.128.1/24`, SRV фиксируется как `10.0.128.2` fileciteturn0file0L8-L16  
- Имена интерфейсов в примере: `enp0s3`, `enp0s8` (смотри “Топология и интерфейсы”) fileciteturn0file0L5-L16  

---

## Файлы репозитория

- **SETUP.md** — основной гайд/шпаргалка (вся практика и команды). fileciteturn0file0L1-L4  
- **README.md** — этот файл (краткое описание и навигация).

---

## Лицензия

MIT — см. файл **LICENSE**.

