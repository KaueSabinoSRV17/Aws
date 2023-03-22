# EC2

É o serviço que provisiona Instâncias Virtuais na AWS. 

Ela é sempre hospedada dentro de uma Zona de Disponibilidade dentro de uma Região.

## Preços

Elas podem ser precificadas seguindo as seguintes categorias:

- On-Demand: Pago pelo tempo que é usado.
- Spot Instances: Curto tempo que você sabe que será usado (muito mais barato do que On-Demand).
- Reserved Instances: Longo tempo (também mais barato do que On-Demand).
- Dedicated Host: Pensada para ser usada com licensas de software atreladas ao servidor.

## Tipos

Elas se encontram nos seguintes tipos:

- Uso Geral (T).
- Computação Otimizada.
- Memória Otimizada (R).
- Armazenamento Otimizado.
- Computação Acelerada (P).

## Volumes

É possíveis adicionar volumes tanto na criação quanto posteriormente.

## Segurança

É possível cuidar da segurança das EC2 com Security Groups. Nele, é possível determinar 
quais serão as portas expostas da EC2 e quais IPs podem ter acesso a ela. 
(Não basta ter a chave certa para o SSH. Você deverá também ter seu IP liberado para o 
acesso a EC2).

### Security Groups

Eles tem estado, e por padrão, permite todo o trafego para fora da EC2.
Suas regras são sempre permissivas, ou seja, sempre temos o mínimo de
permissões que precisamos. Você pode adicionar e remover regras
sempre que quiser e pode associar uma EC2 a múltiplos Security Groups.

## Conectividade

Para se conectar em uma EC2, devemos sempre guardar a chave gerada na criação da EC2.
Podemos guardar a chave em qualquer lugar de nossa preferência. O importante é garantir
que todos em apenas permissão de leitura ao arquivo. Isso é garantido como o seguinte comando:

	chmod 400 <nome da chave>.pem

Garantindo que a chave está permissionada corretamente, podemos agora nos conectar por ssh:

	ssh -i "<caminho até a chave>" <usuário da ec2>@<dns ou IP público da ec2>

**Observação: a AWS fornece estas duas linhas de comando**

## Boot Script

É possível estabelecer um Bash Script que vai ser rodado ao botar a EC2.

## Imagens

Para salvar tempo e replicar todo o ambiente criado em uma EC2 para outra,
podemos fazer uma Imagem AMI da mesma.

Um dos casos de uso mais interessantes é migrar todo uma EC2 de uma região
para outra. Para isso, é seguido os seguintes passos:

- Parar EC2.
- Fazer Imagem.
- Copiar Imagem para outra Região.
- Lançar Instância com Imagem.
- Adicionar Security Groups (Provavelmente não estarão na nova região).

## Meta Data

Informações que podem ser obtidas da EC2, acessando a URL http://<ip da EC2>/latest/meta-data/
(É necessário fazer a requisição estando dentro da VM, via `curl` por exemplo).

**OBS: Também existe a rota http://<ip da EC2>/latest/user-data/, para pegar informações de user como o boot script**

## Auto Scaling

É um serviço que permite aumentar ou diminuir o parque de EC2 conforme o uso. Caso haja 
sobrecarga, será aumentado até o limite estipulado por você.

É preciso definir um template para todas as máquinas do Grupo de Auto Scaling.
Depois de definir este grupo, caso queiramos coloca-lo em um Load Balancer
basta criar um Target Group, vincular o Target Group ao Grupo de Scaling e 
apontar o Load Balancer para o Target Group.
