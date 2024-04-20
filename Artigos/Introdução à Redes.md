# O que é uma rede?

  

# Infraestrutura de rede
![[Pasted image 20240319094638.png]]

Redes podem ser organizadas de várias maneiras com base no escopo de cada empresa e seus objetivos específicos de conectividade. Nesse sentido, não existe nenhum modelo considerado "correto", existem prioridades diferentes de cada empresa e estruturas de rede com seus prós e contras, dentre essas, as principais são:
- Barramento:
	- Estrutura com o menor custo de instalação, consiste em uma linha principal (geralmente de fibra ótica) que se bifurca várias vezes para atender à cada computador da rede.
	- Seu maior problema envolve justamente essa centralização, caso algo ocorra com o cabo principal, todos os computadores que estejam conectados após essa falha vão perder toda a conectividade.
	 ![[Pasted image 20240420134747.png]]
  

# Camadas de rede e vulnerabilidades

  

## Camada de Aplicação

"Aplicações de rede são a razão de ser de uma rede de computadores. Se não fosse possível inventar aplicações úteis, não haveria necessidade de projetar protocolos de rede para suportá-las. Desde o surgimento da Internet, foram criadas numerosas aplicações úteis e divertidas. Elas têm sido a força motriz por trás do sucesso da Internet, motivando pessoas em lares, escolas, governos e empresas a tornarem a rede uma parte integral de suas atividades diárias."

  

A camada de aplicação é a sétima e última camada do modelo OSI, sendo responsável pela interação direta com os aplicativos e serviços de rede. Essa camada oferece serviços de rede específicos para as necessidades dos usuários e das aplicações. Algumas funções comuns da camada de aplicação incluem a comunicação de rede, transferência de arquivos, acesso a banco de dados e navegação na web.

  

Principais protocolos e serviços encontrados na camada de aplicação incluem:

  

1. **HTTP (Hypertext Transfer Protocol):** Utilizado para transferência de dados na World Wide Web, permitindo a visualização de páginas da web.

    - **Atributos:**

        - Stateless: O protocolo não mantém informações sobre o estado da comunicação entre as solicitações e respostas, tornando cada transação independente.

        - Baseado em texto: As mensagens HTTP são legíveis por humanos e consistem em cabeçalhos e corpos de mensagem.

    - **Estrutura do Pacote:**

        - Requisição: Linha de solicitação, cabeçalhos e corpo (opcional).

        - Resposta: Linha de status, cabeçalhos e corpo (opcional).

    - **Vulnerabilidades:**

        - **Injeção de SQL (SQL Injection):** Permite a inserção de comandos SQL maliciosos em campos de entrada, explorando falhas na validação de dados.

        - **Cross-Site Scripting (XSS):** Permite a execução de scripts maliciosos no navegador do usuário, muitas vezes inseridos em campos de entrada não validados.

2. **SMTP (Simple Mail Transfer Protocol):** Usado para envio de e-mails.

    -  **Atributos:**

        - Assíncrono: As mensagens são enviadas de forma assíncrona, sem esperar uma confirmação imediata.

        - Textual: A comunicação entre servidores SMTP é baseada em texto legível.

    - **Estrutura do Pacote:**

        - Composto por comandos (por exemplo, HELO, MAIL, RCPT) e respostas (códigos numéricos).

    - **Vulnerabilidades:**

        - **Relaying Não Autorizado:** Permite que um servidor de correio encaminhe e-mails sem autenticação, possibilitando o envio de spam ou phishing.

        - **Ataques de Força Bruta:** Tentativas repetidas e automáticas de adivinhar senhas, visando obter acesso não autorizado a contas de e-mail.

3. **FTP (File Transfer Protocol):** Utilizado para transferência de arquivos entre sistemas.

    - **Atributos:**

        - Bidirecional: Permite transferência de arquivos em ambas as direções (upload e download).

        - Modo Ativo/Passivo: Modos de conexão para transferência de dados.

    - **Estrutura do Pacote:**

        - Comandos (por exemplo, USER, PASS, RETR) e respostas (códigos numéricos).

        - Controle e dados separados (modo passivo) ou ambos através da mesma conexão (modo ativo).

    - **Vulnerabilidades:**

        - **Ataques de FTP Bounce:** Explora a capacidade do servidor FTP de enviar dados para outros hosts, possibilitando a realização de varreduras em redes internas.

        - **Captura de Credenciais (Sniffing):** Dados de login transmitidos em texto simples podem ser capturados por atacantes usando ferramentas de captura de pacotes.

4. **DNS (Domain Name System):** Responsável pela tradução de nomes de domínio em endereços IP.

    - **Atributos:**

        - Distribuído: Usa uma hierarquia de servidores para traduzir nomes de domínio em endereços IP.

        - Cache: Possui um sistema de cache para melhorar a eficiência das consultas.

    - **Estrutura do Pacote:**

        - Mensagens DNS contêm seção de cabeçalho, seção de pergunta, seção de resposta, seção de autoridade e seção de informações adicionais.

    - **Vulnerabilidades:**

        - **Envenenamento de Cache (Cache Poisoning):** Substituição de entradas legítimas do cache DNS por informações maliciosas, levando a redirecionamentos não autorizados.

        - **Ataques de Negação de Serviço (DoS):** Sobrecarregar servidores DNS com tráfego falso para torná-los inacessíveis.

5. **SNMP (Simple Network Management Protocol):** Facilita o monitoramento e gerenciamento de dispositivos de rede.

    - **Atributos:**

        - Gerenciamento de Rede: Utilizado para monitorar e gerenciar dispositivos de rede.

        - Extensível: Pode ser estendido com MIBs (Management Information Bases) para incluir informações específicas do dispositivo.

    - **Estrutura do Pacote:**

        - PDU (Protocol Data Unit) SNMP, que inclui tipos como GET, SET, e TRAP.

        - MIBs contêm a estrutura hierárquica de informações gerenciadas.

    - **Vulnerabilidades:**

        - **Comunidade SNMP Padrão:** Utilização de comunidades SNMP padrão (por exemplo, "public" ou "private"), que são facilmente adivinháveis, permitindo acesso não autorizado.

        - **SNMP Brute Force:** Tentativas repetidas de autenticação SNMP para obter acesso não autorizado.