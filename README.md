# Aula1-de-sistema-distribuidos


# Ping, NSLookup e Tracert


1. Comando ping
O comando ping é utilizado para testar a comunicação entre o computador e outro dispositivo/servidor na rede.

Para executar no Windows:

Pressione Windows + R.

Digite cmd.

Pressione Enter.

Digite:

ping google.com

No exemplo da aula, o resultado foi:

Disparando google.com [172.217.172.46] com 32 bytes de dados:
Resposta de 172.217.172.46: bytes=32 tempo=13ms TTL=114
Resposta de 172.217.172.46: bytes=32 tempo=10ms TTL=114
Resposta de 172.217.172.46: bytes=32 tempo=9ms TTL=114
Resposta de 172.217.172.46: bytes=32 tempo=9ms TTL=114

Isso significa que o computador conseguiu enviar uma requisição para o endereço do Google e recebeu uma resposta.

O que significa cada informação?
bytes=32 → tamanho dos dados enviados no pacote.

tempo=13ms → tempo que o pacote levou para ir até o destino e voltar (RTT — Round Trip Time).

TTL=114 → Time To Live. É um valor usado para limitar por quantos roteadores um pacote pode passar antes de ser descartado.

No final:

Pacotes: Enviados = 4, Recebidos = 4, Perdidos = 0 (0% de perda)
Mínimo = 9ms, Máximo = 13ms, Média = 10ms

Nesse teste:

Foram enviados 4 pacotes.

Os 4 foram recebidos.

Houve 0% de perda de pacotes.

O menor tempo de resposta foi 9 ms.

O maior foi 13 ms.

A média foi 10 ms.

2. Por que usamos google.com em vez do IP?
Porque é muito mais prático utilizar um nome de domínio do que memorizar um endereço IP.

Por exemplo:

google.com

é mais fácil de lembrar do que:

172.217.172.46

O DNS (Domain Name System) é responsável por traduzir nomes de domínio em endereços IP.

3. Comando nslookup
O nslookup é utilizado para consultar informações do DNS.

Exemplo:

nslookup google.com

Resultado:

Servidor:  UnKnown
Address:  172.31.32.236

Não é resposta autoritativa:
Nome:    google.com
Addresses:  2800:3f0:4001:80e::200e
           172.217.172.46

Nesse caso, podemos observar que google.com possui endereços associados.

IPv4 e IPv6
O endereço:

172.217.172.46

é um endereço IPv4.

Já:

2800:3f0:4001:80e::200e

é um endereço IPv6.

Portanto, um domínio pode estar associado a mais de um endereço IP.

O que significa "Não é resposta autoritativa"?
Significa que a resposta não veio diretamente de um servidor DNS que seja o servidor autoritativo daquele domínio. Ela pode ter vindo, por exemplo, de um servidor DNS que possui a informação armazenada em cache ou que consultou outros servidores.

4. nslookup youtube.com
O mesmo teste pode ser feito com outros domínios:

nslookup youtube.com

No exemplo da aula:

Nome:    youtube.com
Addresses:  2800:3f0:4001:839::200e
           172.217.29.238

Novamente, temos um endereço IPv6 e um IPv4 associados ao domínio.

5. Comando tracert
O comando:

tracert google.com

é utilizado para rastrear o caminho que os pacotes percorrem entre o computador e o destino.

Ele mostra os saltos (hops) realizados pelos pacotes através dos equipamentos de rede, principalmente roteadores.

No exemplo:

Rastreando a rota para google.com [172.217.172.46]
com no máximo 30 saltos:

  1     5 ms     7 ms     8 ms  172.28.128.1
  2    25 ms     5 ms     4 ms  189.57.9.81
  3    90 ms     8 ms     7 ms  177.27.82.196
  4     *        *        *     Esgotado o tempo limite do pedido.
  5    14 ms    12 ms     9 ms  142.251.202.154
  6    27 ms    10 ms    11 ms  108.170.227.19
  7    19 ms     8 ms    12 ms  192.178.253.73
  8    21 ms     7 ms     8 ms  172.217.172.46

Quantos saltos foram realizados?
Foram identificados 8 saltos até chegar ao destino.

Cada número representa uma etapa do caminho:

Computador
   ↓
1º salto
   ↓
2º salto
   ↓
3º salto
   ↓
...
   ↓
8º salto
   ↓
Google

O que significa *?
No 4º salto apareceu:

4     *        *        *     Esgotado o tempo limite do pedido.

O * significa que não houve resposta dentro do tempo esperado para aquela tentativa.

Isso não significa necessariamente que existe um problema na conexão. Alguns roteadores são configurados para não responder a esse tipo de solicitação ou podem limitar/restringir essas respostas.

Por isso, o fato de o salto 4 não responder não impediu que o rastreamento continuasse até o Google.

6. O computador está conectado diretamente ao servidor do Google?
Não.

O computador não se conecta diretamente ao servidor final. Os dados passam por vários equipamentos de rede, principalmente roteadores, até chegar ao destino.

No exemplo, o caminho foi aproximadamente:

Seu computador
      ↓
  172.28.128.1
      ↓
  189.57.9.81
      ↓
  177.27.82.196
      ↓
  [salto sem resposta]
      ↓
  142.251.202.154
      ↓
  108.170.227.19
      ↓
  192.178.253.73
      ↓
  172.217.172.46
      ↓
    Google

Resumo da aula
Comando	Para que serve
ping google.com	Testar a comunicação e medir o tempo de resposta
nslookup google.com	Consultar o DNS e descobrir os IPs associados ao domínio
tracert google.com	Ver o caminho/saltos percorridos até o destino
