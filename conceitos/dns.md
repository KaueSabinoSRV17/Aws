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
