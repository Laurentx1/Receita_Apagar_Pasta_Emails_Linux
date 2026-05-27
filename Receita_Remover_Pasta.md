# Clean Exim4 Script (Linux)

Script simples para limpar filas e logs do **Exim4** automaticamente em servidores Linux.

---

# Objetivo

Este script:

- Para o serviço do Exim4
- Remove mensagens da fila
- Limpa logs de mensagens
- Reinicia o serviço

---

# 1. Criando o script

Abra o arquivo:

```bash
nano /usr/local/bin/clean_exim.sh
```

Cole o conteúdo abaixo:

```bash
#!/bin/bash

systemctl stop exim4

rm -rf /var/spool/exim4/input/*
rm -rf /var/spool/exim4/msglog/*

systemctl start exim4
```

---

# 2. Salvando e saindo do editor (nano)

- Salvar:
  ```text
  CTRL + O
  ```
  Depois pressione:
  ```text
  ENTER
  ```

- Sair:
  ```text
  CTRL + X
  ```

---

# 3. Permissão de execução

Dê permissão ao script:

```bash
chmod +x /usr/local/bin/clean_exim.sh
```

---

# 4. Teste manual

Execute o script para validar funcionamento:

```bash
/usr/local/bin/clean_exim.sh
```

Se não houver erro, está funcionando corretamente.

---

# 5. Automatização com Cron (a cada 5 dias)

Edite o cron:

```bash
crontab -e
```

Adicione a linha:

```bash
0 3 */5 * * /usr/local/bin/clean_exim.sh >/dev/null 2>&1
```

---

# Entendendo o agendamento

| Campo | Significado |
|--------|-------------|
| `0` | minuto 0 |
| `3` | 03:00 da manhã |
| `*/5` | a cada 5 dias |
| `* *` | todos os meses e dias da semana |

---

# Resultado

Execução automática a cada 5 dias às **03:00**.

---

# Observação importante

O `*/5` no cron **não significa um intervalo contínuo de 5 dias exatos**, mas sim:

```text
Dia 1, 6, 11, 16, 21, 26...
```

Ou seja, o cron executa nos dias divisíveis dentro do mês atual.
