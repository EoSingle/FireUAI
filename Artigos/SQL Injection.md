# SQL Injection (SQLi)

Neste artigo, exploraremos os fundamentos do SQL, como funcionam as consultas SQL, e em seguida os detalhes de SQL Injection. Abordaremos como essa vulnerabilidade é identificada, os diferentes tipos de ataques possíveis, e algumas estratégias simples para mitigá-la e proteger aplicações web contra potenciais explorações.

## Primeiro, o que é SQL?

SQL (Structured Query Language) é uma linguagem padrão usada para gerenciar bancos de dados relacionais. Foi originalmente desenvolvida pela IBM nos anos 70 e desde então se tornou a linguagem de fato para interagir com sistemas de gerenciamento de banco de dados (SGBDs) como MySQL, PostgreSQL, SQL Server, Oracle, entre outros.

A principal função do SQL é permitir que os desenvolvedores e administradores de banco de dados possam realizar operações como consultas (queries), inserções, atualizações e exclusões de dados em um banco de dados. Além disso, o SQL também oferece recursos para criar e modificar estruturas de banco de dados, como tabelas, índices, procedimentos armazenados e funções.

A linguagem SQL é estruturada em diferentes partes, incluindo:

1. **DDL (Data Definition Language)**: Usada para definir a estrutura e esquema dos objetos no banco de dados, como CREATE (criação), ALTER (alteração) e DROP (exclusão).
    
2. **DML (Data Manipulation Language)**: Usada para manipular os dados dentro dos objetos do banco de dados, como INSERT (inserção), SELECT (seleção), UPDATE (atualização) e DELETE (exclusão).
    
3. **DCL (Data Control Language)**: Usada para gerenciar as permissões e acessos aos dados, como GRANT (concessão de permissões) e REVOKE (revogação de permissões).

### Estrutura de uma Query

Uma query SQL possui uma estrutura básica que varia dependendo da operação que você deseja realizar (consulta, inserção, atualização, exclusão) e das cláusulas específicas que você precisa aplicar para filtrar ou manipular os dados. Vamos detalhar a estrutura básica de uma consulta (SELECT), que é uma das operações mais comuns em SQL:

#### Estrutura básica de uma consulta SQL (SELECT):

1. **SELECT**: Indica quais colunas ou expressões serão retornadas pela consulta. Você pode selecionar todas as colunas usando `*` ou especificar colunas específicas separadas por vírgula.

   Exemplo:
   ```sql
   SELECT coluna1, coluna2, coluna3
   FROM tabela;
   ```

   Neste exemplo, `coluna1`, `coluna2` e `coluna3` são colunas específicas da tabela `tabela`.

2. **FROM**: Especifica a tabela ou tabelas das quais os dados serão recuperados. Pode-se consultar uma ou várias tabelas simultaneamente usando junções (JOINs).

   Exemplo:
   ```sql
   SELECT *
   FROM clientes;
   ```

   Aqui, `clientes` é o nome da tabela da qual estamos recuperando todas as colunas (`*`).

3. **WHERE** (opcional): Permite filtrar os resultados com base em uma condição específica. A condição pode ser qualquer expressão que avalie como verdadeira, como comparações, operadores lógicos, funções, etc.

   Exemplo:
   ```sql
   SELECT *
   FROM pedidos
   WHERE valor_total > 1000;
   ```

   Neste caso, estamos selecionando todos os pedidos da tabela `pedidos` onde o `valor_total` é maior que 1000.

4. **ORDER BY** (opcional): Define a ordem dos resultados com base em uma ou mais colunas. Por padrão, a ordenação é crescente (ASC), mas você pode especificar descendente (DESC) se necessário.

   Exemplo:
   ```sql
   SELECT *
   FROM produtos
   ORDER BY preco DESC;
   ```

   Aqui, estamos selecionando todos os produtos da tabela `produtos` ordenados pelo preço em ordem decrescente.

5. **GROUP BY** (opcional): Agrupa os resultados com base em uma ou mais colunas. É comumente usado com funções de agregação, como SUM, AVG, COUNT, etc.

   Exemplo:
   ```sql
   SELECT departamento, COUNT(*) as num_funcionarios
   FROM funcionarios
   GROUP BY departamento;
   ```

   Este exemplo conta o número de funcionários em cada departamento da tabela `funcionarios`.

6. **HAVING** (opcional): É usado em conjunto com GROUP BY para filtrar os resultados de grupos específicos baseados em condições.

   Exemplo:
   ```sql
   SELECT departamento, AVG(salario) as media_salario
   FROM funcionarios
   GROUP BY departamento
   HAVING AVG(salario) > 5000;
   ```

   Aqui, estamos selecionando departamentos onde a média de salário dos funcionários é superior a 5000.

### Exemplo completo:

```sql
SELECT nome, idade, cidade
FROM usuarios
WHERE cidade = 'São Paulo'
ORDER BY idade DESC;
```

Neste exemplo:

- `SELECT nome, idade, cidade`: Seleciona as colunas `nome`, `idade` e `cidade`.
- `FROM usuarios`: Indica que os dados serão buscados na tabela `usuarios`.
- `WHERE cidade = 'São Paulo'`: Filtra os resultados para incluir apenas aqueles onde a coluna `cidade` é igual a `'São Paulo'`.
- `ORDER BY idade DESC`: Ordena os resultados com base na coluna `idade`, em ordem decrescente.

Essa estrutura básica pode ser expandida com outras cláusulas SQL dependendo das necessidades específicas da consulta, mas esses são os elementos essenciais para construir e entender uma query SQL simples de consulta.

## ORMs(Object Relational Mapping):
ORMs são frameworks de desenvolvimento que intermediam o processo de consulta no banco de dados transformando tabelas SQL em Objetos e vice-versa, dessa forma, os desenvolvedores não precisem trabalhar diretamente com SQL. Essa alternativa além de acarretar em mais produtividade, também evita vulnerabilidades SQL pois permite uma filtragem pela aplicação antes que ela crie a query.
Dentre os principais Frameworks estão:
- Prisma(Javascript e Typescript)
- PonyORM(Python)
- SQLAlchemy(Python)
- Entity Framework(.NET)

## SQL Injection

O SQL Injection (SQLi) é uma vulnerabilidade web que permite que um invasor interfira nas consultas que um aplicativo faz em seu banco de dados. Isso pode permitir que um invasor visualize dados que normalmente não deveria conseguir acessar. Isso pode incluir dados que pertencem a outros usuários ou quaisquer outros dados que o aplicativo possa acessar. Em muitos casos, um invasor pode modificar ou excluir esses dados, causando alterações persistentes no conteúdo ou no comportamento do aplicativo.

Em algumas situações, um invasor pode escalar um ataque de SQL Injection para comprometer o servidor subjacente ou outra infraestrutura de back-end. Também pode possibilitar a realização de ataques de negação de serviço (DoS).

### Como funciona o SQL Injection?

SQL Injection explora a maneira como os dados são manipulados em uma aplicação web que utiliza consultas SQL para interagir com seu banco de dados. Aqui estão os passos básicos de como um ataque de SQL Injection pode ser realizado:

1. **Identificação da Vulnerabilidade**: Um invasor identifica uma entrada de usuário que não é adequadamente validada ou sanitizada antes de ser incluída em uma consulta SQL.

2. **Inserção de código malicioso**: O invasor insere código SQL malicioso na entrada, aproveitando-se da falha de segurança. Isso geralmente é feito através de campos de formulário, parâmetros de URL, cookies ou cabeçalhos HTTP.

3. **Execução da Instrução Maliciosa**: Quando o aplicativo web executa a consulta SQL, o código malicioso também é executado, causando efeitos indesejados.

### Exemplo de SQL Injection:

Suponha que um aplicativo de login tenha uma consulta SQL para verificar as credenciais do usuário:

```sql
SELECT * FROM usuarios WHERE usuario = 'usuario_digitado' AND senha = 'senha_digitada';
```

Um invasor pode explorar uma vulnerabilidade de SQL Injection inserindo o seguinte no campo de usuário:

```
' OR '1'='1
```

Após a injeção, a consulta SQL poderia se tornar:

```sql
SELECT * FROM usuarios WHERE usuario = '' OR '1'='1' AND senha = 'senha_digitada';
```

Neste caso, `'1'='1'` é sempre verdadeiro, então a consulta retornará todos os registros da tabela `usuarios`, ignorando a necessidade de uma senha válida para o login.

### Impactos do SQL Injection:

- **Leitura Não Autorizada de Dados**: Um invasor pode ler dados sensíveis que não deveriam ser acessíveis como senhas, dados bancários e demais informações pessoais.
- **Modificação de Dados**: Dados existentes podem ser modificados ou excluídos, comprometendo a integridade dos dados.
- **Execução de Comandos Arbitrários**: Comandos SQL maliciosos podem ser executados, potencialmente permitindo o controle total sobre o banco de dados.

### Como identificar um possível SQL Injection

Muitas vezes não há sinais óbvios visíveis externamente para identificar um SQL Injection. No entanto, existem algumas técnicas e sinais que podem ajudar a identificar se um sistema está vulnerável a SQL Injection. Para detectar manualmente a vulnerabilidade podemos inserir nas consultas:

- O caractere de aspas simples ' e procurar por erros ou outras anomalias. 
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente e procura diferenças nas respostas do aplicativo. 
- Condições booleanas, como OR 1=1 e OR 1=2, e procurar diferenças nas respostas do aplicativo. 
- Payloads projetadas para adicionar atrasos quando executadas em uma consulta SQL e procurar diferenças no tempo necessário para responder.

Ferramentas de segurança especializadas também podem ser utilizadas, como scanners de vulnerabilidades, que podem identificar automaticamente potenciais vulnerabilidades de SQL Injection através da análise de código e interação com o aplicativo.

## Outros tipos de SQL Injection
### Blind SQL Injection

Muitas vezes, instâncias de SQL Injection são "vulnerabilidades cegas". Isso significa que o aplicativo não retorna os resultados da consulta SQL ou os detalhes de quaisquer erros de banco de dados em suas respostas. Vulnerabilidades cegas ainda podem ser exploradas para acessar dados não autorizados, mas as técnicas envolvidas geralmente são mais complicadas e difíceis de executar.

As seguintes técnicas podem ser usadas para explorar vulnerabilidades de Blind SQL Injection, dependendo da natureza da vulnerabilidade e do banco de dados envolvido:

- Você pode alterar a lógica da consulta para acionar uma diferença detectável na resposta do aplicativo, dependendo da verdade de uma única condição. Isso pode envolver a injeção de uma nova condição em alguma lógica booleana ou acionar condicionalmente um erro, como uma divisão por zero.
- Você pode acionar condicionalmente um atraso de tempo no processamento da consulta. Isso permite inferir a verdade da condição com base no tempo que o aplicativo leva para responder.

### Second-order SQL injection

O SQL Injection de primeira ordem ocorre quando o aplicativo processa a entrada do usuário de uma solicitação HTTP e a incorpora em uma consulta SQL de maneira insegura.

Já o SQL Injection de segunda ordem ocorre quando o aplicativo recebe a entrada do usuário de uma solicitação HTTP e a armazena para uso futuro. Isso geralmente é feito colocando a entrada em um banco de dados, mas nenhuma vulnerabilidade ocorre no ponto em que os dados são armazenados. Mais tarde, ao lidar com uma solicitação HTTP diferente, o aplicativo recupera os dados armazenados e os incorpora em uma consulta SQL de maneira insegura. Por esse motivo, o SQL Injection de segunda ordem também é conhecida como injeção SQL armazenada (Stored SQLi).

## Mitigação e Prevenção:

Para evitar ataques de SQL Injection, é crucial adotar práticas de segurança sólidas, como:

- **Uso de Parâmetros SQL e Prepared Statements**: Em vez de concatenar strings diretamente em consultas SQL, use parâmetros ou prepared statements fornecidos pelo seu framework ou linguagem de programação. Isso ajuda a separar os dados da lógica da consulta SQL e evita que o código malicioso seja executado.

- **Validação e Sanitização de Dados**: Sempre valide e sanitize os dados de entrada antes de incorporá-los em consultas SQL. Isso inclui usar funções como `mysql_real_escape_string()` (no MySQL antigo), ou preferencialmente, utilizar os métodos de escape fornecidos pelos ORM (Object-Relational Mapping) modernos.

- **Princípio do Menor Privilégio**: Limite as permissões de acesso ao banco de dados para que os aplicativos usem apenas as operações necessárias.

- **Auditoria e Monitoramento**: Implemente auditorias regulares de segurança e monitore o tráfego de dados em busca de atividades suspeitas.

# Referências
- https://portswigger.net/web-security/sql-injection
