# RDS

É um serviço que provê bancos de dados de diversos motores diferentes, 
com sua infraestrutura totalmente gerenciada pela AWS.

O banco de dados pode ser distribuido entre muitas regiões (Multi A-Z)
e pode ter a função de Auto Scalling: Uma capacidade elástica, menor em
caso de desuso, maior em caso de sobrecarga.

## Backups

É também possível determinar por quanto tempo podemos reter os backups,
e em que janela de tempo eles serão executados. Se não escolhermos um
intervalo de tempo, devemos consultar a documentação para saber qual o 
intervalo de tempo default referente a Regiâo do recurso.

A AWS provê múltiplas instâncias, mas o propósito é garantir a 
disponibilidade, e não a performance. Ou seja, não será usado mais de 
uma instânica de cada vez, uma secundária irá entrar apenas se a primária
estiver indisponível.

Vale lembrar que ao fazer um backup, a performance pode ser muito 
prejudicada, e que a AWS não cobra pelo armazenamento do backup,
dado que o mesmo tenha até 100% do tamanho do banco de dados em si.

## Permissionamento

Para permissionar corretamente um recurso ao RDS, devemos adicionar a
ele um Security Group descrevendo a porta e tipo de conexão 
`Mysql/Aurora` e depois editar o mesmo Security Group para permitir o 
acesso a quem estiver dentro dele mesmo.
