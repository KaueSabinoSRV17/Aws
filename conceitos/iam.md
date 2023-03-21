# IAM - Identity Acess Management

O IAM é um serviço que serve para gerenciar os acessos aos recursos da Nuvem da AWS.
Podemos estipular acessos tanto para usuários humanos quanto para um recurso que quer acessar outro recurso
(Uma EC2 acessando um S3, por exemplo. Isso é possível através de Roles, o que descarta a necessidade de ).

## Boas Práticas

- Não criar uma conta para cada usuário, e sim vários usuários em uma mesma conta.
- Dar permissões granulares para cada usuário.
- Implementar Autenticação Multi Fator.
- Guardar com muito sigílo a senha de usuário Root.
- Usar o usuário Root apenas se for absolutamente necessário.
- Use Grupos para estipular uma vez Permissões válidas para diversos usuários.
- Usar políticas gerenciadas por clientes.
- Use níveis de acesso para revisar permissões IAM.
- Usar Roles para delegar permissões.
- Não compartilhe chaves de acesso.
- Rotacione chaves com frequência.
- Use Policy Conditions para segurança extra.
- Monitore a sua atividade na conta da AWS.
