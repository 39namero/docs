# GCP で Docker

GCP で Docker

https://densan-hoshigumi.com/server/gcp-free-linux

SSH認証鍵の作成

ssh-keygen -t rsa -f ~/.ssh/gcp-ssh-key -C “ichito24”

Enter passphrase (empty for no passphrase): （ Enter ）
Enter same passphrase again: （ Enter ）

ls -l ~/.ssh/gcp-ssh-key*

-rw-------  1 ichito24  staff  2602  1 16 17:28 /Users/ichito24/.ssh/gcp-ssh-key
-rw-r--r--  1 ichito24  staff   568  1 16 17:28 /Users/ichito24/.ssh/gcp-ssh-key.pub

cat ~/.ssh/gcp-ssh-key.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCk2rP4BpD4/DS+wK34MxZGIm0HlHvItmGQwfJqfgbCzuffBmlXc2HGkErTKVxEfLFJKy0FI2pgrVqcMBZD1wPkZ7GyuxbXHR0sh4UT5MgEmwbGcZvs/gi4zbMw6WGE9g9Uw/uvAQnjbe9vW5fM6AVmdfBOqosD+eVm90drbH7BwrFqmS+3bgghXh71TJTg2zgcalQMDSGox3KG+DfFCJAe2MixYfKAq7lfGowBSVNF6tBmM/J/xkmY0DOyGaUU2ZuRc3CafFKybzfd7CKKvKjVOOoA1N8Mo4KBkZ2MZw7i9LgFze8tWZ+2NIYvTUsa9CamtJ62Pxo2aebfAP7dQ1mTITmVoCp5NAJ3tz2WEM8TgNNR5FsCAjIXqefzc0gvO/HUZHGXDR/2OpEbeNcMys5e1Do7v0UimavKM6j776pta0MxYxEM4RpdBEYuURAgKaT3Wg+A0DTopX/GC2Sf9QEMiS0DkOlLf6BlfOpHL1ngDGeJCe0ulL5fWB4ZbE4lFIk= “ichito24”

