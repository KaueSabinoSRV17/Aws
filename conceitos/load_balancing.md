# Elastic Load Balancing (ELB)

É um serviço que fica na frente de recursos como EC2, Containers,
Endereços IP e funções Lambda, e serve para balancear a carga
entre 2 ou mais destes recursos. Pode server para mais de uma 
Zona de Disponibilidade.

## Tipos

Pode ter 3 tipos:

- Application: HTTP e HTTPS
- Network: TCP, UDP e TLS
- Classic: Básico entre diversas EC2 e funciona tanto na conexão quanto em request.

## Atributos

Algumas apps precisam manter uma sessão para o cliente. Para configurar um mesmo 
servidor para responder após a primeira request, devemos procurar em "Atributos" por
"Stickness".
