# Elastic Block Store (EBS)

É um serviço que provê volumes que podem ser livremente montados em uma EC2.
É necessário que ambos estejam na mesma Zona de Disponibilidade.

Ao criar um volume, ele não estará formatado. É como comprar um HD ou SSD novo
na loja.

Há diferentes tipos, com performances, tamanhos e preços diferentes.

## Montando Disco na EC2

Para montar um Disco EBS em uma EC2 será necessário acessa-la e montar o disco 
manualmente, como qualquer máquina Linux.

Primeiro, faça um update no `package manager`

Após isso, liste os discos conectados na máquina

	lsblk

É esperado que haja um disco com uma partiação e outro disco sem. Este sem
partição é o EBS que vamos configurar.

Agora devemos particionar o disco com o `fdisk`

	sudo fdisk /dev/<dispositivo sem partição>

Dentro do fdisk você pode usar os seguintes comandos: 

- p: printa as partições feitas.
- m: mostra todos os comandos.
- n: cria nova partição.

Após o comando `n`, rode:

- p: partição primária.
- 1: número de partição.
- 2048: início do disco.
- <final do disco>: fim do disco.
- n: Não remover a assinatura.

Após tudo isso, ao rodar `lsblk` de novo, você verá o disco e a sua partição.

	lsblk

Sendo isso validado, agora devemos criar um file system dentro desta partição.
Usa-se então o comando `mkfs`

	sudo mkfs.<tipo de file system> <partição> -f

Após isso devemos montar o disco em qualquer lugar desejado dentro da máquina.

	sudo mount <disco> <diretório de montagem>

Por fim, devemos garantir que isso tudo será persistido na EC2 após ela reiniciar.
Para isso, o UID do Disco deve estar no arquivo `/etc/fstab`

	sudo cat /etc/fstab

Caso ele não esteja lá, descubra qual o seu UID rodando:

	blkid

E o adicione com o editor de texto de usa escolha.
	
	UUID=<uuid do disco>	<caminho até o ponto de montagem>	<tipo de file system>	<flags> 0 2

Como errar na configuração deste arquivo implica na instância não subir, devemos garantir que nada está errado.
Faça isso desmontando o novo Disco

	sudo unmount <disco>

E depois rode:

	sudo mount -a

E:

	df -h

Se não houver nenhum erro, você pode reiniciar a instância para aplicar todas as alterações e depois entrar de novo:

	sudo reboot

## Encripitando Volume Root de uma EC2

Para fazer isso, devemos:

- parar a EC2 do Volume.
- Criar um snapshot do Volume.
- Copie o Snapshot, dessa vez encriptado.
- Criar Volume com o Snapshot, na mesma Zona.
- Faça o Detach do Volume que está sendo usado pela EC2.
- Faça o Atach do Volume, especificando a Instância e o EXATAMENTE o mesmo disco que estava o volume anterior.
