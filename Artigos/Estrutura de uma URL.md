# Estrutura de uma URL
**Autor: Lucas Albano**

As URLs (Uniform Resource Locators) são fundamentais para a navegação na web. Uma compreensão básica de sua estrutura é crucial para qualquer pessoa utilize a internet e indispensável para profissionais de segurança da informação.

## Componentes de uma URL

Uma URL típica é composta por vários componentes:
### Esquema (Scheme)

O esquema é o protocolo que indica como o recurso deve ser acessado. Alguns dos esquemas mais comuns incluem:

- **HTTP**: para recursos web não seguros.
- **HTTPS**: para recursos web seguros que usam criptografia SSL/TLS.
- **FTP**: para acesso a servidores FTP.
- **File**: para arquivos locais no sistema de arquivos.

### Nome de Usuário e Senha (Username e Password)

Esses componentes são opcionais e geralmente são usados apenas para autenticação em determinados recursos protegidos por senha. Eles são separados do restante da URL por dois pontos (`:`).

### Host e Porta

O host é o endereço do servidor onde o recurso está localizado. Pode ser um domínio, como "www.exemplo.com", ou um endereço IP. Opcionalmente, uma URL pode especificar uma porta onde o recurso está disponível, separada do host por dois pontos (:). Se a porta não for especificada, será utilizada a porta padrão para o esquema fornecido.

### Caminho (Path)

O caminho indica o local específico do recurso no servidor. Ele começa após o nome do host e pode incluir vários diretórios e subdiretórios, além do próprio nome do arquivo.

### Consulta (Query)

A parte de consulta de uma URL é usada para enviar parâmetros adicionais para o servidor. Ela começa com um ponto de interrogação (`?`) e consiste em pares de chave-valor separados por e comercial (`&`). Por exemplo, em "`?id=123&nome=exemplo`", "`id`" e "`nome`" são os parâmetros da consulta, com os valores "`123`" e "`exemplo`", respectivamente.

### Fragmento (Fragment)

O fragmento identifica uma parte específica do recurso. Ele começa com uma cerquilha (`#`) e geralmente é usado em páginas da web para direcionar o navegador para uma seção específica da página.

## Exemplo de URL Completa

Segue um exemplo de uma URL completa com todos os componentes mencionados:

```
https://username:password@www.exemplo.com:8080/pasta/recurso.html?id=123&nome=exemplo#secao
```

Neste exemplo:

- **Esquema**: HTTPS
- **Nome de Usuário e Senha**: username e password
- **Host**: www.exemplo.com
- **Porta**: 8080
- **Caminho**: /pasta/recurso.html
- **Consulta**: id=123&nome=exemplo
- **Fragmento**: secao
