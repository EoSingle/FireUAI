# Segurança e Cibersegurança

A segurança em geral envolve a **proteção** de **ativos** contra diversas **ameaças** representadas por **vulnerabilidades** inerentes. Os processos de segurança geralmente tratam da implementação de mecanismos de segurança (também chamados de **contramedidas**) que ajudam a reduzir o **risco** representado por essas vulnerabilidades.

Cibersegurança é a proteção de todos os ativos que podem ser alcançados pelo **ciberespaço**. O que engloba sistemas de computadores, informações armazenadas ou em trânsito, dispositivos e os usuários destas tecnologias.

Para um ativo ser definido como protegido alguns atributos devem ser mantidos, são estes:

- Confidencialidade
	- Um ativo não pode ser acessado por uma entidade não autorizada.
- Integridade
	- Um ativo não pode ser alterado por uma entidade não autorizada.
- Disponibilidade
	- O acesso a um ativo não pode ser impossibilitado por terceiros.

Estes atributos são conhecidos como a tríade CIA (Confidentiality, Integrality, Availability) sendo um modelo designado a guiar as politicas de cibersegurança de uma organização.

<!-- ![CIAtriad](./Imagens/CIAtriad.png) -->
<div style="text-align: center">
    <img src="./Imagens/CIAtriad.png" alt="CIAtriad">
</div>


Definições mais recentes argumentam que a tríade precisa de novos atributos, dessa forma, adicionam outras características como:

- Autenticidade
	- Um ativo deve conseguir comprovar sua legitimidade e origem.
- Não repúdio
	- Uma entidade não pode negar a autoria de uma ação ou posse de um ativo.

## Padrões de Cibersegurança

Organizações internacionais, como a International Organization for Standardization (ISO) e o National Institute of Standards and Technology (NIST), desempenham um papel fundamental no desenvolvimento de padrões e diretrizes amplamente reconhecidos na comunidade de cibersegurança. Esses padrões frequentemente convergem em princípios fundamentais, processos e boas práticas, fornecendo um alicerce robusto para a segurança cibernética.

O NIST, uma agência federal dos Estados Unidos, é uma referência na produção de padrões e diretrizes para diversas áreas, com destaque para a cibersegurança. Seus documentos orientativos são vitais para organizações que buscam fortalecer sua postura de segurança.

Um exemplo notável é o NIST Cybersecurity Framework (CSF), uma estrutura aberta e baseada em princípios, desenvolvida em resposta à crescente necessidade de orientações comuns entre organizações para o gerenciamento de riscos cibernéticos. O CSF proporciona uma linguagem compartilhada para compreender e comunicar práticas de gestão de riscos cibernéticos.

O CSF é estruturado em cinco funções principais, cada uma centrada em uma área crítica de foco:

1. **Identify (Identificar):** Desenvolver uma compreensão das atividades, ativos e recursos críticos para a organização.
2. **Protect (Proteger):** Implementar salvaguardas para assegurar a entrega segura dos serviços essenciais.
3. **Detect (Detectar):** Desenvolver e implementar atividades de monitoramento e detecção para identificar incidentes de segurança.
4. **Respond (Responder):** Desenvolver e implementar planos de resposta a incidentes para lidar eficazmente com eventos de segurança.
5. **Recover (Recuperar):** Desenvolver e implementar planos de recuperação para restaurar as operações normais após um incidente.

<p style="text-align: center">
  <img src="./Imagens/NISTframework.png" alt="NISTframework">
</p>


A versão 2.0 do framework, lançada em agosto de 2023, introduziu a governança como uma nova função crítica que abrange todo o processo. O documento completo pode ser acessado em: https://doi.org/10.6028/NIST.CSWP.29.ipd

# Áreas da Cibersegurança

A cibersegurança, sem dúvida, engloba uma ampla gama de campos de estudo e áreas de atuação, muitas das quais apresentam enfoques distintos, embora frequentemente interdependentes. Abaixo, destacamos algumas dessas áreas fundamentais:
## Segurança da Informação
A Segurança da Informação abrange a proteção de dados sensíveis da organização, incluindo informações confidenciais, registros de clientes e propriedade intelectual. Essa área envolve a implementação de políticas, procedimentos, tecnologias avançadas e treinamento contínuo para assegurar a confidencialidade, integridade e disponibilidade dos dados.
## Segurança Ofensiva (Ethical Hacking / Penetration Testing)
A Segurança Ofensiva consiste na avaliação proativa da segurança de sistemas, redes e aplicativos, simulando potenciais ataques. Profissionais nessa área atuam como "hackers éticos" (odeio esse nome), identificando vulnerabilidades para corrigi-las antes que criminosos possam explorá-las.
## Segurança de Redes
A Segurança de Redes concentra-se na proteção da infraestrutura de rede, abrangendo dispositivos, protocolos e tráfego de dados. Profissionais dessa área implementam medidas como firewalls, VPNs e sistemas de detecção de intrusões (IDS) para garantir uma comunicação segura.
## Segurança de Sistemas:
A Segurança de Sistemas visa proteger servidores, sistemas operacionais e aplicativos contra ameaças cibernéticas. Isso inclui configuração segura, monitoramento de logs, aplicação de patches e gestão de contas de usuário.
## Segurança em Nuvem:
A Segurança em Nuvem é especializada na proteção de ambientes e dados armazenados em serviços de nuvem. Profissionais dessa área implementam controles específicos para garantir a segurança dos recursos hospedados na nuvem.
## Segurança de Aplicações (Application Security):
Essa área foca na proteção de software contra ameaças, utilizando testes de segurança de aplicativos, revisões de código e a implementação de práticas seguras de desenvolvimento.
## Forense Digital:
A Forense Digital é um campo especializado que aplica técnicas investigativas e analíticas para coletar, preservar, analisar e apresentar evidências digitais relacionadas a incidentes cibernéticos, crimes digitais ou disputas legais.
## Gestão de Identidade e Acesso (Identity and Access Management - IAM):
Concentrando-se na administração de identidades digitais e no controle de acesso a sistemas e dados, essa área inclui autenticação, autorização e gerenciamento de privilégios.
## Criptografia:
A Criptografia é uma disciplina especializada na prática de converter dados ou informações legíveis em um formato ilegível por meio de algoritmos e chaves. Seu principal objetivo é garantir que apenas partes autorizadas possam acessar e compreender a informação original. A criptografia é essencial para proteger dados confidenciais em transações financeiras, comunicações sensíveis e informações pessoais, evitando o acesso de terceiros não autorizados. Suas aplicações são vastas e estão integradas em muitos aspectos da cibersegurança e da privacidade digital.
## Gestão de Riscos e Conformidade:
A Gestão de Riscos e Conformidade preocupa-se em avaliar e mitigar os riscos de segurança cibernética, garantindo que as práticas da organização estejam em conformidade com regulamentações, como a GDPR e LGPD, bem como padrões de segurança reconhecidos. Essa área desempenha um papel crucial na construção de uma postura de segurança robusta e na adaptação contínua às exigências legais e normativas.

# **Hacker:**

Leia o artigo [Tipos de Hacker](./Tipos%20de%20Hacker.md) para entender melhor sobre o termo e os diferentes tipos de hackers existentes.
