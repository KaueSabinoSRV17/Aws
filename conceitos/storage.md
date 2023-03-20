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