# Atualizar o certificado wildcard Let's Encrypt

O certificado do Let's Encrypt é uma ótima forma de você utilizar HTTPS no seu site porque é totalmente gratuito, porém com 90 dias de validade, ou seja, a cada 90 dias você precisa renovar seu certificado.
Este tipo de certificado é bom para ser utilizado em produtos na fase de desenvolvimento ou teste. [^1]

## Meu certificado expirou, e agora?

1. Primeiro vamos executar o comando para ~~gerar~~ renovar um certificado ` certbot certonly --manual -d '[nome do domínio]'`

``` 
certbot certonly --manual -d '*.growuptecnologia.com.br'
```

2. Durante a execução, o *script* solicitará para criar um registro TXT no seu domínio para comprovar que você possui aquele domínio. Crie o script  Para mim foi este:

> _acme-challenge.growuptecnologia.com.br TXT "Hb4fP7HgYi5DBP7fK3xXUqtk9tz0jKGUW3pmeW-91nQ"

[^1]: Assim como todo certificado, ao renovar seu certificado você gera um novo arquivo .pem referente a aquele domínio.
