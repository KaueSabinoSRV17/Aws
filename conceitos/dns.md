# Route 53

É um serviço usado para gerenciar endereços de DNS e a saúde 
dos IPs que são resolvidos por estes enderço.

Nele, podemos tanto registrar domínios completamente novos
e apontar domínios já existentes de sites terceiros para o
Route53 (esta configuração deve ser feita nestes sites
terceiros).

Por padrão, o Route53 disponibiliza até 50 endereços para a
sua conta da AWS.

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
