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

## Público X Privado

### Público Acessando Privado

Para que recursos de uma rede Privada sejam acessíveis por recursos de uma
Rede Pública, devemos configurar ambos os recursos no mesmo Security Group
