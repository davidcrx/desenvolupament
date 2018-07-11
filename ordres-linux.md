<!-- TITLE: Ordres Linux -->
<!-- SUBTITLE: A quick summary of Ordres Linux -->

# Ordres Linux
## Fitxers

Borrar tots els fitxers .bak del directori actual

`find . -name "*.bak" | xargs -d "\n" rm`



## SSH

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

Obrir proxy mitjançant ssh.

`ssh -D 8080 user@domain.com`

