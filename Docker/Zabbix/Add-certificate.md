# Adicionando um certificado no Zabbix frontend executado em docker compose

Muitas pessoas sabem da praticidade e agilidade de ter um ambiente Zabbix em cima de docker compose, mas acabam tendo muitas dúvidas de como gerenciar o frontend.
O certificado é uma das situações que pode levar a dúvida.

## Como adicionar o certificado no frontend?

Primeira coisa que temos que ter é um certificado gerador por uma certificadora. Temos muitas opções como CertSign, GoDaddy, Hostinger, Hostgator, entre outros.
[Neste post](https://github.com/matheusrp01/francomatheus/blob/main/Linux/Certificados/Renew-wildcard-letsencrypt.md) fiz um artigo explicando como criar um certificado totalmente gratuito pelo Let's Encrypt. Ele é válido apenas por 90 dias, mas pode ser renovado quantas vezes quiser (como falo no artigo, este é uma opção apenas para cenário de teste ou desenvolvimento).


1. Os [arquivos suportados](https://www.zabbix.com/documentation/current/pt/manual/installation/containers) pelo Zabbix é `.crt` e `.key`, portanto se você têm arquivos `.pem` iguais aos gerados pelo Let's Encrypt é só executar o comando abaixo.

Para gerar o `.crt`:

```
openssl
```

Para obter o `.key` basta copiar o arquivo `key.pem`:

```
cp
```

2. Com os arquivos em mãos, vamos confirmar se dentro do `docker-compose.yml` esta mapeado o volume do frontend para o caminho `/etc/ssl/apache2/` do nosso container.

```
frontend
```

3. Agora com o volume mapeado basta a gente copiar ou mover os arquivos para a pasta e reiniciar o container.
