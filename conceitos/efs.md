# Elastic File System (EFS)

Serviço que provê um File System NFS elástico, que escala para cima 
ou para baixo conforme apenas a sua necessidade, e é usado em EC2.

Ela é diferente de montar um disco pelo EBS.

É necessário que o EFS esteja na mesma Zona de Disponibilidade,
Subnet e Security Group da EC2, e também ter as ferramentas
CLI para realiar a montagem.

Sobre o Security Group, devemos criar um acesso do tipo NFS,
na porta padrão, e o range autorizado deverá ser inicalmente vazio.
Depois voltamos, e adicionamos o próprio Security Group como incluido
nos ranges autorizados

Para instalar:

	sudo apt install amazon-efs-utils

Crie a pasta que vai receber a montagem:

	mkdir <caminho desejado para a montagem>

Agora, realize a montagem:

	sudo mount -t efs <id do efs>:/ <caminho até a pasta destino>

**OBS: O código de exemplo da AWS não está ajustado com o próprio id do seu EFS!**
