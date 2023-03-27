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

Podemos ter até 9 seções em um Template, sendo a "Resources" a única obrigatória.
Ñão é necessário seguir uma ordem, mas é uma boa prática, pois uma seção pode 
depender de outra. Esta ordem é:

- Versão: Determina a versão do Formation a ser usada.
- Descrição.
- Metadata: Detalhes adicionais sobre o Template, como algumas configurações específicas.
- Parâmetros: Passa valores durante a execução de uma criação ou atualização de uma Stack. Promove reusabilidade em Recursos e Outputs.
- Mappings.
- Condições.
- Transform: Usado para configurar recursos Serveless
- Recursos: Define todos os recursos.
- Outputs: Estes Outputs vão para o Console ou o resultado do comando na CLI. Podem ser usados também como um recurso Inter-Stack.

### Update

Devemos nos atentar ao procedimento feito em um Update. Em alguns casos,
apesar de não parecer intuitivo, o Cloud Formation vai deletar recursos
ao invés de alterar existentes.

Por exemplo uma EC2: Caso não haja subnet definida no Template para ela,
toda alteração resultará em uma nova instância, não uma alteração da
existente.

### Parâmetros

Parâmetros são úteis para definir valores personalizados ao criar ou atualizar stacks.
Eles só podem ser usados nas seções de Recursos e Output, através da função Ref, que
vai receber o seu nome como argumento.

O seu tipo será obrigatório são:

- String.
- Number.
- List<Number>.
- CommaDelimitedList.
- AWS-Specific Parameter Types.
- Systems Manager Parameter Store.

É possível determinar constraints, como o tamanho máximo de uma String, e também
um valor padrão.

### Funções Intrínsicas

Funções Intrínsicas são funções padrões do Formation para gerenciar as Stacks.

São usadas para preencher valores durante o um Runtime como criar ou 
atualizar.

#### Função Ref

Retorna o valor de um Recurso ou Parâmetro ao receber o ID Lógico.

## Stack

Sao usadas para gerir uma coleção de recursos relacionados. Para criar, deletar
ou atualizar nosso ambiente em produção, devemos o fazer com Stacks.

Uma Stack só pode ter um Template, porém, um Template pode criar diversas Stacks.

## Change Sets

É um resumo de suas mudanças que deverá aparecer antes de elas serem implementadas
em produção.