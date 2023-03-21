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

### Bucket Policies

Caso queiramos estabelecer Policies ao Bucket, a configuração é sempre feita no formato JSON.
A AWS disponibiliza oficialmente os templates para as principais configurações usadas.
