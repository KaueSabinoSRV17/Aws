# Cloud Formation

É uma ferramenta de Infra as Code da AWS. Com ela, podemos automatizar
e versionar o processo de criação de nossa infraestrutura. Ela trabalha
com 3 principais conceitos: 

- Templates.
- Stack.
- Change Sets.

## Templates

É uma base que define toda a sua infraestrutura, como os recursos a serem
criados. É possível também definir coisas como parâmetros, condições e 
outputs.

É interessante codar Templates para garantir que eles funcionem em diversas
regiões e contas.

São escritos em YAML.

## Stack

Sao usadas para gerir uma coleção de recursos relacionados. Para criar, deletar
ou atualizar nosso ambiente em produção, devemos o fazer com Stacks.

Uma Stack só pode ter um Template, porém, um Template pode criar diversas Stacks.

## Change Sets

É um resumo de suas mudanças que deverá aparecer antes de elas serem implementadas
em produção.
