# AWS CLI

É possível fazer qualquer coisa da Console pelo Terminal, através da 
AWS CLI.

Para ter acesso, precisamos primeiro ter um usuário do IAM com acesso
programático. Após criar o usuário, instalar a CLI e rodar o seguinte
comando:

	aws configure

Isso vai pedir os dados copiados da criação do usuário do IAM. Estes
dados são a `Secret Key` e a `Acess Key`.

**OBS: É possível dar permissão para uma EC2 usar a CLI sem as Keys,
através das Roles do IAM**
