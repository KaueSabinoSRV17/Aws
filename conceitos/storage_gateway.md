# Storage Gateway

Este é um serviço que procura mapear um Storage on-premise para o S3 da AWS.

Ele funciona da seguinte maneira: É necessário ter uma VM no ambiente on-premise
que vai ter o software do Storage Gateway instalado. Estas VMs podem ser as seguintes:

- VMware ESXi.
- Microsoft Hyper-v 2012R2/2016.
- Linux KVM.
- Amazon EC2.
- Hardware Físico.

Ele disponibiliza 3 tipos de storage:

- File Gateway
- Volume Gateway
- Tape Gateway

## File Gateway

Guarda arquivos como Objetos no S3, disponibilizando chace local para
baixa latência nos arquivos mais recentes.

## Volume Gateway

Block storage no S3, com backups point-in-time como snpashots do EBS
O Volume é montado como um sistema *Internet Small Computer System Inteface (ISCSI)*.

- Chaced volumes: acesso de baixa latência aos dados mais recentes.
- Stored volumes: dados on-premise com horários de backup (Anula a Disponibilidade de usar uma EC2).

## Tape Gateway

Faz um backup dos seus dados no S3 e arquiva no S3 Glacier, usando
seus processos de backup em fita existentes.
