# Virtual Private Network (VPC)

É um serviço que permite lançar recursos da AWS em uma rede virtual
definida por você, se parecendo com sua infraestrutura real, mas com
a vantagem da infra escalável da AWS.

Por padrão, quando acabamso de entrar em uma região é sempre criada
uma VPC default.

A VPC default sempre acompanha uma Subnet para cada Zona de Disponibilidade
da Região em que ela está.

## Padrão de ranges da Rede

Por padrão, quando criamos uma rede local, sempre temos 253 endereços, já
que o primeiro (endereço da rede em si) e o último (endereço broadcast)
são reservados.

Numa VPC, mais 3 endereços são reservados, portanto a quantidade disponível
ao criar uma VPC é 251.

## Internet Gateway

Para o acesso externo, devemos criar um Internet Gateway. Cada VPC pode ter
apenas um Internet Gateway.

É também necessário associar uma Tabela de Rotas, que é criada por default
quando criamos uma nova VPC. Dentro desta Tabela, precisamos settar como
targeto o Internet Gateway criado.

## Security Groups

Security Groups são uma forma de configuração de firewalls na VPC.

Em um Security Group, não é possível colocar regras de bloqueio, 
apenas regras de permissionamento, e caso tenhamos bloqueado toda
a entrada, mas liberado a saída, a entreda, vinda de um comunicação
para a saída permitida, será permitida também (isso ocorre pois
Security Groups são Statefull).

## Público X Privado

### Público Acessando Privado

Para que recursos de uma rede Privada sejam acessíveis por recursos de uma
Rede Pública, devemos configurar ambos os recursos no mesmo Security Group
(isso é chamado de Bastion host).

### Privado acessando a Web

Por padrão, uma rede privada não é capaz de acessar a Web.

Para isso, precisamos implementar um NAT Gateway. Ele garante que o recurso
consiga acessar a Web, mas barra o caminho contrário.

Um detalhe importantíssimo é que o NAT Gateway deve ser criado na rede 
pública. Após a sua criação, precisamos editar a Tabela de Rotas da 
rede privada e adicionar uma rota de 0.0.0.0/0 (toda a Web) apontando
para o NAT Gateway criado.

## Network ACLs

Para granular o acesso a VPC, podemos usar as ACLs.

Com elas, podemos determinar regras de entrada e saida da rede, que tem total
precedência sobre os Security Groups.

Elas não são Stateful como Security Groups. Isso significa que caso seja
necessário garantir uma comunicação, precisamos configurar as regras de
entrada e também de saída.

As requisições feitas a uma VPC não passam por todas as regras de ACL, elas 
parão na regra que atende a elas. Portanto, podemos ter ao mesmo tempo uma
regra que proibe o acesso SSH de todos os IPs, e uma regra que permite IPs
específicos. Caso o IP bata em uma regra específica dele, a regra que proibe
todos não vale para ele.

## Vpc Flow Log

Em uma VPC é possível associar logs ao CloudWatch e também ao S3.

## Direct Connect

É um serviço que provê conexão direta a rede da AWS através de 
pontos de acesso específicos ao redor do planeta. É necessário
criar na Console e realmente implementar a conexão fisicamente.

## Endpoint

Um Endpoint para as VPCs garante que a comunicação entre recursos
da AWS não saiam da rede da AWS. 

Por padrão, sem usar os IPs internos, os recursos vão até a Internet
e ai sim chegam em outros recursos.

### Tipos

Ele pode ser implementado em 2 tipos:

- Interface.
- Gateway (Apenas S3 e DynamoDB).
