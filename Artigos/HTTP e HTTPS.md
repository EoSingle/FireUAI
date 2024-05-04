# Desvendando o protocolo HTTP: funcionamento, etapas de comunicação, requisições, métodos, status e vulnerabilidades.
**Por Álvaro L.**

O Protocolo de Transferência de Hipertexto, abreviado como HTTP (do inglês, Hypertext Transfer Protocol), é a base da comunicação na World Wide Web (WWW). Desde sua criação por Tim Berners-Lee na década de 1990, o HTTP tem sido essencial para a troca de informações entre clientes, como navegadores web, e servidores. Neste artigo, vamos explorar detalhadamente o que é o protocolo HTTP, como ele funciona, suas etapas de comunicação, os tipos de requisições, métodos e os códigos de status.

## O que é o Protocolo HTTP?

O Protocolo HTTP é um protocolo de comunicação utilizado para transferir dados na internet. Ele opera no modelo cliente-servidor, onde um cliente (geralmente um navegador web) faz requisições a um servidor para acessar recursos, como páginas da web, imagens ou vídeos, através de URLs (Uniform Resource Locators).

## Mas e o HTTPS?

O HTTPS (Hypertext Transfer Protocol Secure) é uma versão segura do protocolo HTTP. Ele emprega criptografia SSL/TLS para proteger a integridade e a privacidade das informações durante a comunicação entre o navegador do usuário e o servidor web. 

## Funcionamento do HTTP:

O HTTP opera em um modelo de solicitação-resposta, seguindo várias etapas de comunicação:

1. **Estabelecimento da Conexão:** O cliente inicia a comunicação estabelecendo uma conexão TCP/IP com o servidor na porta padrão 80 para HTTP e na porta 443 para HTTPS (HTTP Secure).
2. **Envio da Requisição:** O cliente envia uma mensagem de requisição HTTP contendo informações como o método da requisição, a URL do recurso desejado, cabeçalhos de requisição e, opcionalmente, o corpo da requisição com dados adicionais.
3. **Processamento da Requisição:** O servidor recebe a requisição, interpreta os dados e determina como responder. Ele executa a ação solicitada pelo cliente e prepara uma resposta apropriada.
4. **Envio da Resposta:** O servidor envia uma mensagem de resposta HTTP de volta ao cliente contendo o código de status da resposta, cabeçalhos de resposta e, opcionalmente, o corpo da resposta com os dados solicitados pelo cliente.
5. **Fechamento da Conexão:** Após completar a transação, a conexão TCP pode ser fechada, dependendo das configurações do servidor e do cliente.

## Requisições HTTP:

Existem vários tipos de métodos HTTP que podem ser utilizados em uma requisição. Alguns dos métodos mais comuns incluem:

- **GET:** Solicita dados de um recurso específico
- **POST:** Submete dados para serem processados por um recurso identificado pela URL.
- **PUT:** Substitui todas as representações atuais do recurso de destino com o carregado no corpo da requisição.
- **DELETE:** Remove o recurso especificado.
- **PATCH:** Aplica modificações parciais a um recurso.
- **HEAD:** Solicita apenas os cabeçalhos de resposta, sem o corpo da resposta.

## Status HTTP:

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

4. **304 Not Modified**: Usado para cache de navegador. Indica que a versão em cache do recurso ainda é válida e pode ser usada.

5. **400 Bad Request**: O servidor não consegue entender ou processar a solicitação devido a um erro do cliente, como dados ausentes ou formatação inválida.

6. **401 Unauthorized**: A autenticação é necessária para acessar o recurso, mas falhou ou não foi fornecida.

7. **403 Forbidden**: O servidor se recusa a aceitar a solicitação, mesmo que seja válida. Geralmente por falta de permissão.

8. **404 Not Found**: Indica que o recurso solicitado não foi encontrado no servidor.

9. **409 Conflict**: A solicitação entra em conflito com o estado atual do recurso, geralmente devido a atualizações simultâneas.

10. **410 Gone**: O recurso solicitado não está mais disponível e não estará novamente.

11. **500 Internal Server Error**: Indica um problema inesperado no servidor que impede o atendimento da solicitação. Geralmente requer investigação por parte dos desenvolvedores para identificar a causa.

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

O Protocolo HTTP é uma tecnologia fundamental que possibilita a comunicação eficaz na Web. Ao entender seu funcionamento, suas etapas de comunicação, os tipos de requisições, métodos, códigos de status e as vulnerabilidades, os desenvolvedores, ou outros profissionais da área, são capacitados a criar aplicações web robustas e eficientes e compreender o papel deste protocolo no funcionamento da internet. Pois com o crescimento contínuo da internet e das tecnologias web, o HTTP continua a desempenhar um papel vital na troca de informações online.

**Para saber mais sobre o protocolo HTTP, acesse os materias complementares:**

- https://www.alura.com.br/artigos/http

- https://youtu.be/CXzbUwK6lc8?si=y49BSdsCY4uwidrZ
