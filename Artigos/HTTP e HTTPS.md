# O protocolo HTTP
**Por Álvaro L., Lucas Albano e Thiago Felipe**

O Protocolo de Transferência de Hipertexto, abreviado como HTTP (do inglês, Hypertext Transfer Protocol), é a base da comunicação na World Wide Web (WWW). Desde sua criação por Tim Berners-Lee na década de 1990, o HTTP tem sido essencial para a troca de informações entre clientes, como navegadores web, e servidores. Neste artigo, vamos explorar detalhadamente o que é o protocolo HTTP, como ele funciona, suas etapas de comunicação, os tipos de requisições, métodos e os códigos de status.

## O que é o Protocolo HTTP?

O Protocolo HTTP é um protocolo da camada de aplicação utilizado para transferir documentos de hipermídia, como o HTML. Ele opera no modelo cliente-servidor, onde um cliente (geralmente um navegador web) faz requisições a um servidor para acessar recursos, como páginas da web, imagens ou vídeos, através de URLs (Uniform Resource Locators). É também um protocolo sem estado ou stateless protocol, que significa que o servidor não mantem nenhum dado entre duas requisições (state). Apesar de ser frequentemente baseado em uma camada TCP/IP, pode ser utilizado em qualquer camada de transporte confiável, ou seja, um protocolo que não perde mensagens silenciosamente como o UDP.

## Mas e o HTTPS?

O HTTPS (Hypertext Transfer Protocol Secure) é uma atualização do protocolo HTTP original que introduz camadas de segurança. Anteriormente, o modelo HTTP mantinha a conexão entre cliente e servidor como pacotes de bytes abertos, portanto qualquer um que conseguisse interceptar esse tráfego seria capaz de acessar informações sensíveis do usuário que poderiam estar nesse pacote. Pensando nisso, foi criado o modelo HTTPS, que emprega criptografia SSL/TLS para proteger a integridade e a privacidade das informações durante a comunicação entre o navegador do usuário e o servidor web.

O modelo SSL/TLS consiste na forma de criptografia utilizada junto com o HTTP atualmente, que foi primeiramente implementado com o SSL(Secure Sockets Layer), criado pela empresa Netscape. Nesse sentido, apesar de o modelo funcionar muito bem, ele possuía algumas falhas de segurança, além disso órgãos reguladores relacionados à internet, principalmente dos EUA, ficaram preocupados com a exclusividade que a Netscape tinha com relação a esse modelo de criptografia, uma vez que se eles cessassem seus serviços de alguma maneira, todo o tráfico HTTPS também pararia imediatamente. Nesse sentido, com a intenção de não se tornar refém de uma empresa privada, foi criado o protocolo TLS(Transport Layer Security), tendo como ponto de partida o SSL e resolvendo os problemas de segurança que seu antecessor possuía.

O protocolo TLS atual funciona com uma mistura de criptografia utilizando chaves simétricas e assimétricas. Primeiramente, quando o cliente tenta estabelecer o primeiro contato com o servidor, ele utiliza da chave de criptografia pública do servidor para criptografar uma mensagem contendo uma chave simétrica, o servidor utiliza sua chave privada para descriptografar essa mensagem e assim, receber a chave que estava contida nela. A partir desse momento, o servidor e o cliente começam a se comunicar utilizando essa chave simétrica, esse método evita que a chave seja interceptada por alguém mal-intencionado e permite a comunicação por criptografia simétrica, que é mais rápida e, portanto, melhora a performance da comunicação entre as duas partes.

## Funcionamento e Estrutura do HTTP

O HTTP opera em um modelo de solicitação-resposta (request-response), seguindo várias etapas de comunicação:

1. **Estabelecimento da Conexão:** O cliente inicia a comunicação estabelecendo uma conexão TCP/IP com o servidor na porta padrão 80 para HTTP ou na porta 443 para HTTPS.
2. **Solicitação (Request):** O cliente envia uma mensagem de requisição HTTP contendo informações como o método da requisição (GET, POST, etc.), a URL do recurso desejado, cabeçalhos de requisição e, opcionalmente, o corpo da requisição com dados adicionais.
3. **Processamento da Requisição:** O servidor recebe a requisição, interpreta os dados e determina o que deve ser feito.
4. **Resposta (Response):** O servidor envia uma mensagem de resposta HTTP de volta ao cliente contendo o código de status da resposta (200, 302, 404, etc.), os cabeçalhos de resposta e, opcionalmente, o corpo da resposta com os dados solicitados pelo cliente.
5. **Fechamento da Conexão:** Após completar a transmissão, a conexão TCP pode ser encerrada, a menos que seja mantida aberta para futuras solicitações (através do cabeçalho `Connection: keep-alive`).

### Pacotes HTTP
Um pacote HTTP possui dois tipos principais de cabeçalhos: o cabeçalho de solicitação (Request Header), enviado pelo cliente para o servidor, e o cabeçalho de resposta (Response Header), enviado pelo servidor de volta para o cliente. 
#### Cabeçalho de Solicitação (Request Header):
```
Método URI Versão_HTTP
Cabeçalho_1: Valor_1
Cabeçalho_2: Valor_2
...
Cabeçalho_N: Valor_N

Corpo_da_Solicitação (Opcional)
```

- **Método**: Indica a ação que o cliente deseja realizar no recurso identificado pelo URI. Exemplos comuns incluem GET, POST, PUT, DELETE, etc.
- **URI**: Uniform Resource Identifier que identifica o recurso solicitado.
- **Versão HTTP**: Versão do protocolo HTTP sendo usada, como HTTP/1.1.
- **Cabeçalhos**: São pares chave-valor que fornecem informações adicionais sobre a solicitação. Podem incluir informações sobre o cliente, preferências de conteúdo, formatos aceitos, cookies, entre outros.
- **Corpo da Solicitação**: Opcionalmente, a solicitação pode incluir um corpo, contendo os dados a serem enviados ao servidor, como no caso de solicitações POST.

> Nem todos os cabeçalhos exibidos em uma requisição são cabeçalhos de requisição. Por exemplo, o `Content-length` exibido em uma requisição POST é na realidade uma **entity header**, que referencia o tamanho do corpo da mensagem de requisição. Porém, esses cabeçalhos de entidade muitas vezes são chamados de cabeçalhos de requisição.

**Exemplo de Request Header:**

```
GET /home.html HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/testpage.html
Connection: keep-alive
Upgrade-Insecure-Requests: 1
If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT
If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a"
Cache-Control: max-age=0
```

##### Entity Headers Comuns:

1. **Content-Type**: Indica o tipo de mídia do corpo da entidade, como text/html, application/json, image/jpeg, etc.
2. **Content-Length**: Indica o tamanho do corpo da entidade em bytes.
3. **Content-Encoding**: Indica a codificação aplicada ao corpo da entidade, como gzip, deflate, br, etc.
4. **Content-Language**: Indica o idioma natural ou idiomas do conteúdo no corpo da entidade.
5. **Content-Disposition**: Especifica a forma como o conteúdo deve ser apresentado ao usuário, por exemplo, inline (dentro da página) ou attachment (como um download).
6. **ETag**: Uma etiqueta de entidade exclusiva, geralmente usada para verificação de condições de atualização usando cabeçalhos de solicitação If-Match ou If-None-Match.
7. **Last-Modified**: Indica a data e hora em que a entidade foi modificada pela última vez.
8. **Expires**: Indica a data e hora de expiração da entidade, após a qual ela é considerada obsoleta.
9. **Cache-Control**: Controla o comportamento de armazenamento em cache de entidades em caches intermediários.
10. **Pragma**: Usado para fornecer diretivas de controle de cache para compatibilidade com versões mais antigas do HTTP.
12. **Allow**: Especifica os métodos HTTP permitidos em uma entidade.
#### Cabeçalho de Resposta (Response Header):
```
Versão_HTTP Código_de_Status Razão
Cabeçalho_1: Valor_1
Cabeçalho_2: Valor_2
...
Cabeçalho_N: Valor_N

Corpo_da_Resposta (Opcional)
```

- **Versão HTTP**: Versão do protocolo HTTP sendo usada, como HTTP/1.1.
- **Código de Status**: Indica o resultado do processamento da solicitação pelo servidor, como 200 para sucesso, 404 para recurso não encontrado, 500 para erro interno do servidor, etc.
- **Razão**: Uma breve descrição textual do código de status.
- **Cabeçalhos**: Assim como no cabeçalho de solicitação, os cabeçalhos de resposta são pares chave-valor que fornecem informações adicionais sobre a resposta enviada pelo servidor.
- **Corpo da Resposta**: Opcionalmente, a resposta pode incluir um corpo, contendo os dados solicitados pelo cliente, como no caso de solicitações GET bem-sucedidas.

## Requisições HTTP:

Existem nove tipos de métodos HTTP que podem ser utilizados em uma requisição, são eles:

- **GET:** Solicita dados de um recurso específico
- **POST:** Submete dados para serem processados por um recurso identificado pela URL.
- **PUT:** Substitui todas as representações atuais do recurso de destino com o carregado no corpo da requisição.
- **DELETE:** Remove o recurso especificado.
- **PATCH:** Aplica modificações parciais a um recurso.
- **HEAD:** Solicita apenas os cabeçalhos de resposta, sem o corpo da resposta.
- **TRACE:** Ecoa o pedido, de maneira que o cliente possa saber o que os servidores intermediários estão mudando em seu pedido.
- **OPTIONS:** Recupera os métodos HTTP que o servidor aceita.
- **CONNECT:** Serve para uso com um proxy que possa se tornar um túnel SSL e TLS (um túnel pode ser usado, por exemplo, para criar uma conexão segura).

### Status HTTP:

Após receber uma requisição, o servidor responde com um código de status HTTP, que indica o resultado da operação. Grupos de status HTTP:

- **1xx:** Informacional - Indica que a requisição foi recebida e está sendo processada.
- **2xx:** Sucesso - Indica que a requisição foi bem-sucedida.
- **3xx:** Redirecionamento - Indica que é necessário tomar uma ação adicional para completar a requisição.
- **4xx:** Erro do Cliente - Indica que ocorreu um erro na requisição do cliente.
- **5xx:** Erro do Servidor - Indica que ocorreu um erro no servidor enquanto processava a requisição.

**Códigos de status mais comuns:**

1. **200 OK**: Indica uma solicitação HTTP bem-sucedida. A resposta inclui o conteúdo solicitado, dependendo do método de solicitação (GET, PUT, POST, etc.).

2. **201 Created**: Confirma que a solicitação foi bem-sucedida e resultou na criação de um novo recurso.

3. **204 No Content**: O servidor atendeu à solicitação, mas não há conteúdo para retornar. Geralmente usado para solicitações que não exigem resposta, como exclusões.

4. **205 Reset Content**: Diz ao agente do usuário para redefinir o documento que enviou esta solicitação.

5. **300 Multiple Choices**: A solicitação tem mais de uma resposta possível. O agente do usuário ou usuário deve escolher um deles. (Não há uma maneira padronizada de escolher uma das respostas, mas links HTML para as possibilidades são recomendados para que o usuário possa escolher).

6. **301 Moved Permanently**: A URL do recurso solicitado foi alterada permanentemente. A nova URL é fornecida na resposta.

7. **302 Found**: Este código de resposta significa que o URI do recurso solicitado foi alterado temporariamente. Outras alterações no URI podem ser feitas no futuro. Portanto, esta mesma URI deve ser utilizada pelo cliente em requisições futuras.

8. **304 Not Modified**: Usado para cache de navegador. Indica que a versão em cache do recurso ainda é válida e pode ser usada.

9. **400 Bad Request**: O servidor não consegue entender ou processar a solicitação devido a um erro do cliente, como dados ausentes ou formatação inválida.

10. **401 Unauthorized**: A autenticação é necessária para acessar o recurso, mas falhou ou não foi fornecida.

11. **403 Forbidden**: O servidor se recusa a aceitar a solicitação, mesmo que seja válida. Geralmente por falta de permissão.

12. **404 Not Found**: Indica que o recurso solicitado não foi encontrado no servidor.

13. **409 Conflict**: A solicitação entra em conflito com o estado atual do recurso, geralmente devido a atualizações simultâneas.

14. **410 Gone**: O recurso solicitado não está mais disponível e não estará novamente.

15. **500 Internal Server Error**: Indica um problema inesperado no servidor que impede o atendimento da solicitação. Geralmente requer investigação por parte dos desenvolvedores para identificar a causa.

16. **501 Not Implemented**: O método da requisição não é suportado pelo servidor e não pode ser manipulado.

### Cookies

HTTP Cookies são pequenos arquivos de texto armazenados no dispositivo do usuário pelo navegador da web. Eles são usados para armazenar informações específicas sobre a atividade do usuário em um determinado site. Os cookies desempenham um papel fundamental na personalização da experiência do usuário na web, permitindo que os sites se lembrem das preferências e do histórico de navegação dos usuários.

#### Funcionamento dos cookies

Quando um usuário visita um site, o navegador envia uma solicitação HTTP para o servidor web. Esta solicitação inclui informações sobre o navegador, o dispositivo e outras informações relevantes. O servidor responde à solicitação enviando não apenas o conteúdo da página solicitada, mas também instruções sobre como o navegador deve se comportar. Isso inclui a definição de cookies.

Quando o navegador recebe a resposta do servidor, ele armazena os cookies no dispositivo do usuário. Os cookies geralmente consistem em pares de chave-valor e podem conter informações como preferências de idioma, informações de login, itens no carrinho de compras, etc. Em solicitações subsequentes para o mesmo site, o navegador envia os cookies relevantes de volta para o servidor junto com a solicitação HTTP. Isso permite que o servidor acesse as informações armazenadas nos cookies e personalize a experiência do usuário de acordo. O servidor processa os cookies recebidos junto com a solicitação e utiliza as informações contidas neles para personalizar a resposta. Por exemplo, se um usuário está logado, o servidor pode fornecer acesso a áreas restritas do site.

Os cookies podem ser atualizados, modificados ou excluídos pelo servidor a qualquer momento. Eles também podem ter uma data de expiração, após a qual são automaticamente removidos pelo navegador.

Os cookies são amplamente utilizados na web para uma variedade de fins, incluindo rastreamento de sessões de usuários, personalização de conteúdo, armazenamento de preferências do usuário e muito mais. No entanto, é importante observar que os cookies também podem levantar preocupações com a privacidade do usuário, especialmente quando são usados para rastrear o comportamento do usuário sem seu consentimento explícito.

## Principais vulnerabilidades do protocolo HTTP:

- **Falta de Criptografia:**

O HTTP transmite dados em texto simples, o que significa que qualquer pessoa com acesso ao tráfego de rede pode interceptar e ler as informações transmitidas entre o cliente e o servidor. Isso torna o HTTP suscetível a ataques de interceptação de dados, como o sniffing de pacotes, onde os invasores podem capturar e analisar o tráfego de rede em busca de dados sensíveis, como credenciais de login e informações financeiras.

- **Ataques Man-in-the-Middle (MITM):**

Os ataques MITM são uma ameaça significativa ao protocolo HTTP, onde os invasores interceptam o tráfego de rede entre o cliente e o servidor para realizar atividades maliciosas, como a modificação de dados transmitidos, o roubo de informações confidenciais e a injeção de código malicioso em páginas da web. Como o HTTP não possui criptografia embutida, os ataques MITM podem ser facilmente realizados, comprometendo a segurança da informação online.

- **Ataques de Injeção de Conteúdo:**

Devido à falta de validação adequada de entrada de dados, o HTTP é vulnerável a ataques de injeção de conteúdo, como SQL Injection e Cross-Site Scripting (XSS). Os atacantes podem explorar essas vulnerabilidades para inserir código malicioso nos dados transmitidos via HTTP, comprometendo a segurança do aplicativo web e permitindo a execução de comandos não autorizados no servidor.

- **Replay Attacks:**

Sem controle de estado embutido, o HTTP está suscetível a ataques de repetição, onde os invasores capturam e retransmitem solicitações HTTP válidas para realizar ações não autorizadas no servidor ou comprometer a integridade dos dados transmitidos. Os replay attacks representam uma ameaça significativa à segurança do HTTP, especialmente em cenários onde a autenticação do usuário é realizada via tokens de sessão não criptografados.

- **Exposição de Dados Sensíveis:**

Devido à transmissão de dados sensíveis via URL no HTTP GET, há o risco de exposição de informações confidenciais nos logs do servidor, caches de proxy e histórico do navegador. Isso pode incluir senhas, tokens de autenticação, informações financeiras e outros dados privados, tornando os usuários vulneráveis a ataques de espionagem e roubo de identidade.

- **Cookies Inseguros:**

Os cookies são frequentemente usados para rastrear a sessão do usuário em sites. No entanto, quando transmitidos sem criptografia, os cookies podem ser interceptados e manipulados por atacantes para assumir a identidade de um usuário legítimo, realizar sessões hijacking (sequestro de navegador, que é a modificação não autorizada das configurações de um navegador) e acessar informações confidenciais.

## Mitigação das vulnerabilidades do HTTP:

Para mitigar as vulnerabilidades do HTTP, são recomendadas as seguintes medidas de segurança:

- Implementação do HTTPS para criptografar o tráfego de rede.
- Uso de firewalls de aplicativos da web (WAFs) para proteger contra ataques de injeção de conteúdo e outros ataques de aplicativos da web.
- Validação rigorosa de entrada de dados para prevenir ataques de injeção.
- Autenticação de dois fatores para proteger contra ataques de replay e roubo de credenciais.
- Criptografia de cookies para proteger informações sensíveis durante a transmissão.

## Conclusão:

O Protocolo HTTP é um dos principais protocolos da internet, sendo fundamental para seu funcionamento. Ao entender suas etapas de comunicação, os tipos de requisições e respostas, métodos, códigos de status, sua estrutura e as vulnerabilidades, os desenvolvedores são capacitados a criar aplicações web mais seguras. Além disso, entender o HTTP é indispensável para profissionais de segurança da informação, como pentesters, pois é o procolo que dita a interação com aplicações web.

#### Materiais complementares:

- https://www.alura.com.br/artigos/http
- https://youtu.be/CXzbUwK6lc8?si=y49BSdsCY4uwidrZ
- https://developer.mozilla.org/pt-BR/docs/Web/HTTP
- https://en.wikipedia.org/wiki/HTTP_cookie
