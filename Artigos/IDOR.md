# IDOR - Insecure direct object references
**Autor: Lucas Albano**

*Insecure direct object references* (IDOR - Referências diretas inseguras a objetos) são um tipo de vulnerabilidade de controle de acesso que ocorre quando um aplicativo permite que usuários acessem objetos diretamente, sem validar se possuem permissão para isso. O termo IDOR foi popularizado pelo OWASP Top Ten em 2007, mas representa apenas um exemplo de falhas comuns de controle de acesso.

## Causas
A vulnerabilidade IDOR ocorre quando um aplicativo confia nas entradas fornecidas pelo usuário para acessar objetos sem verificar se o usuário tem permissão para isso. Por exemplo, em um sistema de compras online, uma URL como `https://exemplo.com/pedido?id=123` pode permitir que um atacante modifique o ID do pedido na URL para acessar informações de outros usuários, caso o aplicativo não valide adequadamente as permissões de acesso.

## Mais Exemplos

Por exemplo, ao acessar um perfil de usuário a aplicação web pode gerar uma URL como `https://example.org/users/123`. O 123 na URL é uma referência direta ao registro do usuário no banco de dados, geralmente representado pela chave primária. Caso um atacante altere esse número para 124 e obtiver acesso às informações de outro usuário, o aplicativo está vulnerável à *Insecure Direct Object Reference*. Isso acontece porque o aplicativo não verificou corretamente se o usuário tinha permissão para visualizar os dados do usuário 124 antes de exibi-los. 

Em alguns casos, o identificador pode não estar na URL, mas sim no corpo do POST, conforme exemplo a seguir: 

```
<form action="/update_profile" método="post"> 
	<!-- Outros campos para atualização de nome, email, etc. --> 
	<input type="hidden" name="user_id" value="12345">
	<button type="submit">Atualizar perfil</button> 
</form>
``` 

Neste exemplo, o aplicativo permite que os usuários atualizem seus perfis enviando um formulário com o ID do usuário em um campo oculto. Se o aplicativo não realizar o controle de acesso adequado no lado do servidor, os atacantes podem manipular o campo “user_id” para modificar perfis de outros usuários sem autorização.

## Mitigação

Para mitigar um IDOR, é crucial implementar verificações de controle de acesso para cada objeto que os usuários tentem acessar. Os usuários devem ter acesso apenas aos recursos que precisam para realizar suas tarefas. Limitar o acesso aos recursos sensíveis ajuda a reduzir a superfície de ataque. Além disso, podem ser utilizados identificadores complexos como medida de defesa adicional, mas o controle de acesso é crucial mesmo com esses identificadores.

Se possível, evite expor identificadores em URLs e corpos POST. Em vez disso, determine o usuário atualmente autenticado a partir das informações da sessão. Ao utilizar várias etapas de fluxo, passe identificadores na sessão para evitar adulterações.

## Referências
- [OWASP Cheat Sheet Series: Insecure Direct Object Reference Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
- [PortSwigger: Insecure direct object references (IDOR)](https://portswigger.net/web-security/access-control/idor)
- [Varonis: O que é IDOR (Insecure Direct Object Reference)?](https://www.varonis.com/pt-br/blog/o-que-e-idor-insecure-direct-object-reference)
