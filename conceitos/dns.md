# Route 53

É um serviço usado para gerenciar endereços de DNS e a saúde 
dos IPs que são resolvidos por estes enderço.

Nele, podemos tanto registrar domínios completamente novos
e apontar domínios já existentes de sites terceiros para o
Route53 (esta configuração deve ser feita nestes sites
terceiros).

Por padrão, o Route53 disponibiliza até 50 endereços para a
sua conta da AWS.

Ao cadastrar um domínio de DNS no Route 53, vamos reeber da
AWS uma lista com os endereços que devem ser autoridades para
o domínio cadastrado. após isso devemos configurar estes endereços
cAmazon Cloud Front e Route53:omo no mesmo site que registramos o domínio.

**OBS: O Route53 não comporta domínios .com.br!**

## Testando a propagação

Depois de lançar o serviço do Route53, podemos testar se o
mesmo realmente está apontando para dentro da AWS.

	dig ns <endereço desejado>

## Policy Routing

Podemos estabelecer Políticas de Roteamento para os endereços
de DNS no Route53.

Entre outros, é possível estabelcer:

- Simples: Apenas resolve um endereço para um IP.
- Com Peso: Podemos atribuir pesos diferentes para os IPs, fazendo com que um atenda mais que o outro.
- Failover: É necessário ativar um Health Check. A partir de um Health Check, estabelecemos rotas primárias e de Back Up.
- Latência: Também é interessante usar com Health Check. Podemos direcionar para o servidor mais próximo à requisição.

## Certificado

Para que possamos realmente passara a usar o HTTPS em produção,
precisamos passar pela a etapa de emissão de um Certificado SSL.
Este também é um serviço da AWS, o Certificate Manager.
