✅ 1. Criar o script

Abra o arquivo:

nano /usr/local/bin/clean_exim.sh

Cole exatamente isso dentro:

#!/bin/bash

systemctl stop exim4

rm -rf /var/spool/exim4/input/*
rm -rf /var/spool/exim4/msglog/*

systemctl start exim4
💾 2. Salvar e sair do nano

Depois de colar:

Salvar: CTRL + O → depois ENTER
Sair: CTRL + X
🔐 3. Dar permissão de execução

Agora libera execução do script:

chmod +x /usr/local/bin/clean_exim.sh
🧪 4. Testar manualmente

Roda o script pra ver se está funcionando:

/usr/local/bin/clean_exim.sh

Se não der erro, está ok.

⏰ 5. Configurar cron (a cada 5 dias)

Abra o cron:

crontab -e

Agora adicione essa linha:

0 3 */5 * * /usr/local/bin/clean_exim.sh >/dev/null 2>&1
📌 O que isso significa
0 → minuto 0
3 → 03:00 da manhã
*/5 → a cada 5 dias
* * → todos os meses e dias da semana

👉 Ou seja: roda a cada 5 dias às 03:00 da manhã
