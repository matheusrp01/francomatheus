# Atualizar o certificado wildcard Let's Encrypt

O certificado do Let's Encrypt é uma ótima forma de você utilizar HTTPS no seu site porque é totalmente gratuito, porém com 90 dias de validade, ou seja, a cada 90 dias você precisa renovar seu certificado.
Este tipo de certificado é bom para ser utilizado em produtos na fase de desenvolvimento ou teste. [^1]

## Meu certificado expirou, e agora?

1. Primeiro vamos executar o comando para ~~gerar~~ renovar um certificado ` certbot certonly --manual -d '*.[nome do domínio]'`

``` 
certbot certonly --manual -d '*.growuptecnologia.com.br'
```

2. Durante a execução, o *script* solicitará para criar um registro TXT no seu DNS autoritativo para comprovar que você possui aquele domínio (sugestão: espere no mínimo 30 minutos para continuar o script após criar o registro no seu DNS). Será um modelo como este:

> _acme-challenge.growuptecnologia.com.br TXT "Hb4fP7HgYi5DBP7fK3xXUqtk9tz0jKGUW3pmeW-91nQ"

3. Após rodar com sucesso, o *script* irá criar os arquivos de certificado no caminho `/etc/letsencrypt/live/`. Neste caminho fica o arquivo `fullchain.pem`, `chain.pem` e o `key.pem`. Com estes 3 arquivos você conseguirá utilizar ou exportar o arquivo .crt do seu certificado wildcard.

Os certificados wildcards não são renovados automaticamente como os certificados para domínio, portanto atente-se na data de expiração.

[^1]: Assim como todo certificado, ao renovar seu certificado você gera um novo arquivo .pem referente a aquele domínio.
