# Amazon S3 - Simple Storage Service

Este serviço serve para guardar arquivos na Nuvem da AWS. Podemos usar ele para guardar e ler os 
arquivos de todo lugar da internet. 

## Elementos

- Bucket: um Bucket é aonde ficam armazenados os arquivos que guardamos no S3.
- Object: é como é chamado todo arquivo no S3.
- Keys: é como os Objetos são únicamente identificados, seguindo o padrão <nome do bucket><nome do objeto>.
- Regions: um bucket deve ter um nome completamente único em toda Nuvem da AWS, pois seu nome é usado em seu domíno. Porém, ele ainda está em uma Região

## Funções

### Classes de Storage

Uma classe de Storage define o preço de armazenamento de cada Objeto. Quanto mais barato, mais
tempo podemos levar para realizar a leitura do Objeto.

Portanto, devemos pagar mais para arquivos altamente lidos, e economizar com arquivos raramente lidos.

## Acesso

Por padrão, todo o acesso aos Objetos de um Bucket são restritos, ou seja, apenas quem tem acesso a Console é capaz
de ler e gravar os arquivos de um Bucket.

Podemos definir o nível de acesso ao nível de Objeto ou ao nível de Bucket (Regras definidas no Bucket estão 
acima de regras definidas por Objeto).

Objetos Públicos inplicam em uma URL de acesso livre ao arquivo em questão.

É possível adicionar um MFA ao deletar arquivos, muito útil para garantir que 
apenas os usuários certos podem fazer esta exclusão.

### Bucket Policies

Caso queiramos estabelecer Policies ao Bucket, a configuração é sempre feita no formato JSON.
A AWS disponibiliza oficialmente os templates para as principais configurações usadas.

## Segurança

Por padrão, toda a comunicação com o storage é feito através da criptografia SSL, através do 
HTTPS.

É possível gerenciar você mesmo a encriptação dos arquivos no Client Side, ou também feito 
Server Side

Ao encriptar no Server Side, podemos deixar a AWS gerenciar a criptografia (Também é possível
deixar a cargo da AWS, mas escolher com qual chave os arquivos devem ser encriptados).

### Responsabilidade

A responsabilidade da AWS é apenas gerenciar toda a infraestrutura da Nuvem. Os arquivos
guardados no S3 são estritamente de nossa responsabilidade!

## Versionamento

O Versionamento é uma função do S3 que permite guardarmos versões diferentes de um mesmo objeto.

Ao fazer o upload de um arquivo com um nome de outro já existente, a versão do arquivo é atualizada
e vamos ter ambos guardados no S3.

Há 3 estágios para o Versionamento de um Bucket. "não versionado", "versionamento ligado" e "versionamento suspenso".
Uma vez ligado, não é possível voltar para "não versionado", apenas é possível passar para "versionamento suspenso".

Vale ressaltar que o Acesso de um Objeto é ditado pelo ID de Versão, ou seja, após tornar a versão atual pública,
a próxima versão não irá herdar o Acesso público. Para cada versão, devemos configurar o acesso separadamente.

## Lifecycle

É possível estabelecer rotinas baseadas em eventos dentro do S3. Estas ações podem ser: 

- Transition actions: Quando um Objeto muda de para outra Classe Storage.
- Expiration actions: Quando Objetos expiram.

OBS: Podemos escolher se vamos aplicar para versões correntes e anteriores para ambas.

Pode ser que você receba um aviso de que as regras de Lifecycle estão conflitantes, apesar 
de estar ok. Revise bem antes de criar o Lifecycle.

## Replicação

É um serviço assíncrono (não instantâneo) que sincroniza os arquivos de dois Buckets.

Muitas vezes isso é necessário não por necesssidade, mas por Lei!

Vale destacar que para usar a Replicação, o Bucket obrigatoriamente deve estar versionado!
Ao rodar a replicação, podemos determinar se a Classe de Storage, Dono do Arquivo, entre outros,
vão mudar no destino do arquivo.

É importante salientar que o Bucket não será replicado até que haja um novo upload no Bucket.

## Acesso Entre Contas

É possível ter acesso entre serviços de S3 de diferentes contas. Para que isso seja possível, 
vamos precisar atender ao menos um dos seguintes requisitos:

- Policies baseados em Recursos e AWS Identity and Acess.
- Lista de Controle de Acesso baseada em Recursos e Policies do IAM.
- Roles do IAM Entre-Contas (o mais simples de ser implementado).

Ao seguir o método por Roles Entre-Contas do IAM, basta criar a Role com acesso ao S3 na conta dona do 
S3, entrar na conta que irá consumir o S3 e mudar a Role da conta para a criada.

## Transfer Acceleration

Este serviço acelera a transferência do Bucket, pois ele faz uso das Edge Locations do 
CloudFront mais próximas do Cliente.
