# Elastic Container Service (ECS)

Permite que você coloque apps containerizados no ar, colocando ou
não uma infraestrutura gerenciada pela AWS.

Podemos provisionar estes apps por 3 maneiras:

- EC2: pelo ECS é possível automatizar a criação de uma infra baseada em EC2 (auto-scaling, load balancer, etc).
- EKS: Kubernetes na AWS.
- Fargate: Gerência Serveless das suas apps conteinerizadas.

## Parando tarefas

Como o ECS provisiona automaticamente o auto-scaling, parar um tarefa
faz apenas com que outra se inicie, pois está settado um mínimo de 
tarefas rodando. Para realmente parar uma tarefa devemos settar este 
mínimo para 0.

## Tarefas

Podemos separar toda a orquestração de microserviço em tarefas, que 
rodam a partir da defininição dos containeres.

## Serviços

É a definição da infraestrutura que fica por trás das Tarefas, como um
Load Balancer e o Auto Scaling por exemplo.

## Cluster

São as máquinas, gerenciadas por você ou não, que vão rodar os Serviços
e Tarefas.
