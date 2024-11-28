# X-ui Auto Restart
ریستارت خودکار xui با استفاده از این آموزش

#### آموزش

1. ایجاد اسکریپت شل
ابتدا یک اسکریپت شل ایجاد کنید که دستور x-ui restart را اجرا کند.

```
sudo nano /usr/local/bin/x-ui-restart.sh
```
و محتوای زیر را در آن قرار دهید:

```
#!/bin/bash
x-ui restart
```
سپس فایل را ذخیره کرده و خارج شوید.

2. دادن مجوز اجرا به اسکریپت
دستور زیر را اجرا کنید تا اسکریپت قابل اجرا باشد:

```
sudo chmod +x /usr/local/bin/x-ui-restart.sh
```
3. ایجاد یک تایمر با Systemd
یک فایل سرویس Systemd ایجاد کنید:

```
sudo nano /etc/systemd/system/x-ui-restart.service
```
و محتوای زیر را در آن قرار دهید:

```
[Unit]
Description=Restart x-ui service

[Service]
ExecStart=/usr/local/bin/x-ui-restart.sh
```
فایل را ذخیره کرده و خارج شوید.

4. ایجاد تایمر برای اجرای هر ساعت
فایل تایمر را ایجاد کنید:

```
sudo nano /etc/systemd/system/x-ui-restart.timer
```
محتوای فایل تایمر زیر هر 1 ساعت خودکار اجرا میشود.
محتوای زیر را وارد کنید:

```
[Unit]
Description=Run x-ui restart every hour

[Timer]
OnBootSec=1min
OnUnitActiveSec=1h
Unit=x-ui-restart.service

[Install]
WantedBy=timers.target
```
⚠️ توجه کنید مثدار 1h به معنای یکساعت میباشد، میتوانید مطابق میل خود مقدار را تغییر دهید.

5. فعال‌سازی و اجرای تایمر
دستورات زیر را اجرا کنید:
```
sudo systemctl daemon-reload
```
```
sudo systemctl enable x-ui-restart.timer
```
```
sudo systemctl start x-ui-restart.timer
```
6. بررسی وضعیت تایمر
برای اطمینان از این که تایمر به درستی کار می‌کند، دستور زیر را اجرا کنید:

```
sudo systemctl list-timers --all
```
شما باید تایمر x-ui-restart.timer را ببینید که زمان اجرای بعدی را نشان می‌دهد.
