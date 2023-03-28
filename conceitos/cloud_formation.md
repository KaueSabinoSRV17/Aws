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
- Parâmetros
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
um valor padrão (vale lembrar que o valor padrão também será validado pelas
constraints definidas).

#### Parâmetros Específicos da AWS

A AWS fornece uma série de Tipos específicos de Parâmetros que referenciam os principais
recursos, como VPCs e subnets. Ao popular na criação da Stack, teremos um select box apenas
com os valores válidos dos recursos da nossa conta, o que tira a possibilidade de erros.

#### Pseudo Parâmetros

São Parâmetros padrões que podemos acessar, como ID da Conta, Região, etc.

### Metadata

Região onde podemos determinar informações adicionais sobre o nosso template.

Geralmante apps de terceiros, a própria interface do CloudFormation usam esta
seção e os nosso Parâmetros podem fazer uso do que está definido em Metadata.

### Condições

Podemos estipular uma seção para condições em nossos Templates.
Para avaliar as condições, podemos referenciar via `!Ref` um 
Parâmetro, Pseudo-Parâmetro, Mapping e outras Condições.
Nesta seção há algumas Funções Intrínsicas:

#### Equals

Recebe um valor e o compara com outro. Retorna `true` se forem iguais e `false´
se forem diferentes.

### Not

Inverte o valor de uma Condição.

### And

Recebe duas condições, e retorna `true` se ambas forem `true` e
`false` se ambas forem `false`.

### Or

Recebe duas condições e retorna `true` caso apenas uma seja `true`
e `false` caso apenas uma seja `false`.

### If

Recebe uma condição, um valor que será assumido caso a condição
recebida seja `true` e outro valor caso a condição recebida seja
`false`.

Esta é a única Função Condicional que pode ser usada fora da seção
Conditions do Template.

### Outputs

Nesta seção podemos definir a sáida da Stack criada com o Template.
Esta saída pode referênciar qualquer coisa criada dentro da Stack
e também pode ser usada em Templates Multi-Stack para proporcionar
uma Stack maior gerenciada entre Múltiplos Templates.

Temos um limite máximo de 60 Outputs.

#### Função GetAtt

Caso seja necessário ter um parâmetro específico, podemos usar a 
`GetAtt`, que recebe um recurso, e o nome do atributo a ser retornado.

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

É uma foram alternativa de atualizar suas Stacks. Usando este recurso, podemos ver
uma previsção do que exatamente vai acontecer antes de executar a alteração.
Isso garante que nada fora do planejado irá acontecer.

é possível criar mais de um Change Set, mas ao executar um deles, todos serão deletados.

Vale lembrar que um Change Set não prevê todas as falhas que podem acontecer ao executar,
e assim como um Update comum, todas as mudanças bem sucedidas serão desfeitas caso uma delas
dê erro.