# Analise de Trafego e Rede

### RFC
RFC sao documentos que regulam o funcionamento da internet.

  - Algumas RFCs importantes para analise de trafego: 768,791,792, 793, 1122, 6890, 8200
  - Ferramentas para auxilio tshark, wireshark, mtr, ping, netcat, iptraf, packit e tcpdump.
  - [orgão responsavel pela homolocação da RFC](https://www.ietf.org)
  - Auxilio  para testes e estudo: simulador de redes CORE.

<br />

### Estrutura de um protocolo
![estrutura de um protocolo](img/estrutura_de_um_protocolo.png)

<br />

### Protocolo IP
![protocolo ip](img/protocolo_ip.png)

  - Protocolo IP e formado por 32Bits.
  - [**Version**]: os primeiros 4 bytes se referem a versao.
  - [**IHL**]: internet header length: tamanho do cabeçalho **internet**.
    - internet se refere a o nome do protocolo, "internet protocol ip".
  - [**Type of Service**]: e 1byte inteiro, "8bits" que utilizado para qualidade de serviço. Normalmente ele vem zerado.
  - [**Total Length**]: Tem 2bytes, e o tamanho em bytes de todo ip e todo payload ipv4 pode ter ate 65.535bytes de tamanho.
  - [**Fragment Offset**]: Utilizado na fragmentacao do ip. Se estiver marcada com 1, nao fragmente caso esta marcado com zero podera fragmentar.
  - [**Flags**] Sao 3Bytes, normalmente vem zerada
  - [**TTL ou Time to Live**] 8bytes e o tempo pela RFC medido em Hop "salto". Tempo de vida de um pacote.
    - Hop ou salto e numero de vezes que um pacote passa por um roteador.

Utilizando o comando "mtr" para exemplificar o Hop:

`root@terminal:~# mtr -n yahoo.co.jp`
![exemplo mtr](img/exemplo_mtr_yahoo.png)
 - Snt indica que o mtr faz envio continuo
 - **Loss** e a porcentagem de perda de pacote. No oitavo Hop pode ser visto que teve uma perda grande de pacote 96.6%
 - Do 1 ate 19 sao numero de roteadores que pacote passou ate seu destino que e o 20.

Funcionamento do **mtr**.
  - Para o mtr saber o caminho, por exemplo da qui ate Japao. Ele manda um pacote para yahoo do Japao com TTL=1, quando chega no primeiro roteador ele leva zero, manda um icmp dizendo, "Seu pacote foi destruido ttl expirado". Agora sabendo quem e o roteador que esta na frente, ele envia novamente pacote para o mesmo endereco, so que desta vez com TTL=2, fazendo esse percurso ate saber todos os Hops que pacote faz ate o destino.
 
 <br />
 
Utilizando o "ping"

`root@terminal:~# ping -c4 yahoo.co.jp`
![exemplo_pong](img/exemplo_pong.png)
  - Neste exemplo, e enviado um ping para o endereco indicado, ele       retorna o pong.
    - Pong e a resposta que a maquina do servidor enviou para o destinatario que fez a request.
  - [**rtt**] Round Triple Time. E o tempo de resposta de ida e vinda.
  - [**ttl=49**] E tempo de vida que um pacote pode ter. Ele e produzido pelo sistema operaciona e colocado dentro do pacote ip, e a cada roteador que ele passa "Hop" perde 1. Caso chegue a zero, esse roteador que tirou, tem que destruir esse pacote e informar para a origin que o ttl expirou.
  
Os sistemas operacionais possuem um ttl padrao.
   - Unix e derivados tem ttl 255
   - Windowns 128
   - Linux 64

Nesse caso e possivel saber que o servidor a qual foi enviado o pacote se trata de um linux. Analisando esse caso, vejamos:
  Por cada roteador que pacote passou, ate chegar aqui ele perdeu 1, ele teve em media 30 saltos "Hop", sabendo que nao se gasta mais de 30 saltos para atravesar o mundo, poderiamos dizer que teria 30 + 49 = 79.
  Se baziando nisso poderiamos chegar a 128 ou 64 de ttl. Nesse caso a opcao mais plausivel e ttl=64.

A casos em que o ttl pode ser alterado, dificultando assim a analise.
  
  Vejamos o exemplo:
  
`root@terminal:~# cat /proc/sys/net/ipv4/ip_default_ttl`
![ip_default_ttl](img/ip_default_ttl.png)
  - O diretorio **/proc** controla propriedades do kernel.
  - Caso altere o valor de 64 para 50 por exemplo o ttl dos pacotes sera setado para 50.
  
<br />
  
`root@terminal:~# traceroute -n yahoo.co.jp`

  - O traceroute tradicional mostra a rota.
  - Diferente do mtr o traceroute nao e ciclico, ele nao fica forcando uma resposta.
  
<br />

  - [**Header Checksum**] E calculado de dois em dois bytes, esse calculo e feito em cima do cabecalho. A cada pacote recebido o roteador tem que calcular o checksum pois, tem que diminuir um no TTL. No caso do ipv6, ele nao possui checksum no cabecalho, esse e um dos motivos que fazem do ipv6 ser mais rapido, pois diminui o tempo de processamento do roteador.
  
  - [**Source Adress**] E o endereco de ip de origem, que um dado obrigatorio.
  
  - [**Destination Adress**] O testino do pacote enviado.
  
  - [**Option**] Geralmente os pacotes nao usam. Sao quatro Options classicos no ip, sao eles:
    - **Time Stamp** para voce gravar dentro do campo option que vai ate 10 linhas a data e hora de passgem que um pacote faz por cada roteador.
    - **Record Root ou RR**. E a garavacao de todas sequencias de ips da ida ate a volta.
    - **Lose Root**. Exemplo do seu funcionamento e que se ele armazena tres ips, o seu pacote tem que passar por esses tres ips ate o seu destino. Nao importanto se ele passar por outro ip, mas ele tem que passar pelo tres ip la descritos, fazendo assim que seu pacote seja guiado.
    - **Struct Root**. Informando os ip nele faz com que o pacote so passe pela queles roteadores la descritos, fazendo um percurso restrito.

- [**Protocol**] O ip so conseugue carregar um tipo de dado dentro dele, um outro protocolo de rede, que sao chamados protocolos ip.
Segue o exemplo a baixo:

  `root@terminal:~# less /etc/protocols`
  ![exemplo_protocols](img/exemplo_protocols.png)
  - Aqui e exibido os protocolos que andam dentro do ip. Um dos conhecidos que e informado sao: tcp, icmp e tcp

<br />
  
- [**Padding**] E como se fosse a rolha do pacote, pois o cabecalho ip e multiplo, entao ele tem que fechar sentinho 32bits. Para isso e acrecentado zero nela ate fechar 32Bits.

<br />

Capturando o primeiro pacote. Representando em hexadecimal. Neste exemplo sera possivel ver todo cabecalho do pacote.

`root@terminal:~# tcpdump -n ip -c 1 -x`
![exemplo_tcpdump_hexadecimal](img/exemplo_tcpdump_hexadecimal.png)

<br />

Descricao do formato do ip: [**0.0.0.0./8**]


"Esta maquina/Esta rede"
  - Os primeiros 4 zeros, sao esta maquina, ou seja a maquina pessoal.
  - /8 e esta rede. A rede em que a maquina esta.

Para exemplo se fizer ping para propria maquina, o kelnel do sistema operacional ira responde.

Nesse caso ainda que a maquina nao tenha placa de rede, avera o retorno do pong. Pois e respota do kernel do sistema.

`root@terminal:~# ping -c2 0.0.0.0`
![ping_kernel_responde](img/ping_kernel_responde.png)

<br />

Como podemos observar **0.0.0.0** nao significa default, e sim esta rede.

`root@terminal:~# router -n`
![route_esta_rede](img/route_esta_rede.png)

  - Analisando a imagem, **0.0.0.0** e a representacao de todas as redes em que a maquina esta conectada na quele momento. Nesse caso **0.0.0.0** personifica:
    - 172.17.0.0
    - 192.168.0.0
  
  
  - E para ele chegar ate essa rede e atraves do Roteador, "192.168.0.2", que e o gateway.
    - **Roteador** e uma maquina que tem varias placas de rede, e cada placa de rede tem um ip e cada ip se chama gateway. Entao Gateway e um ip que me leva para outro segmento de rede.
  
  Entao 192.168.0.2 e o gateway deste roteador que me leva para as demais redes la descritas na imagem.
  
<br />

### Protocolo tcp

![protocolo_de_transporte](img/protocolo_de_transporte.png)

  - Protocolo tcp tem 32 bits de lagura, 16 bits inicias sao porta de origem, e os 16 bits finais sao a porta de destino.
  - [Source Port] 16 bits iniciais.
  - [Destination Port] 16 bits finais.
  - [Data Offset] tem 4 bits e onde começa o payload.
  - [Options] pode ter ate 10 linhas, e diferente do ip normalmente ele vem configurado.
  
### Flags TCP

  - [Syn] synchronize, Inicia conexao.
  - [Fin] finish, finaliza conexoes.
  - [Psh] push, envia dados.
  - [Ack] acknowledgment, confirmad de que e conhecido o numero de      sequencia do proximo seguimento a ser enviado pelo lado oposto.
  - [Rst] reset, nao entendi.

Para se iniciar uma conexao, utiliza se flag **Syn**. Sempre e o clinete que inicia uma conexao e numca o servidor.

Chegando a conexao no servidor ele devolve uma confirmacao da conexao, **Ack**. O tcp e um protocolo orientado a conexao.

Sao tres metodos de difucao de dados, sao eles:
  - **Syn-plex**
    - Eu falo e voce escuta, ex: tv e radio.
  - **Half-duplex**
    - Os dois podem falar, mas cada um no seu tempo, ex: radio de comunicao militar e nextel.
  - **Full-duplex**
    - Os dois podem falar a o mesmo tempo ex: telefone.

Primeira coisa que um servidor faz e testar a conexao. Servidor vai disser Syn, e o cliente responde Ack. Agora o cliente tenque testar a conexao dele ate o servidor, cliente diz Syn, servidor responde Ack. Veja exemplo:

   C/S     |   C/S    | Flags
-----------|----------|------
Cliente    | Servidor | [SYN]
Servidor   | Cliente  | [ACK]
Servidor   | Cliente  | [SYN]
Cliente    | Servidor | [ACK]

<br />

O protocolo http se encontra dentro do tcp, por isso ele entra pela porta 80, pois a porta 80 e porta do tcp. O protocolo http e o push do tcp. Processo de payload se se monta da seguinte forma.

Cliente responde [Psh], aqui ele pede o index para o servidor.

Servidor respode [Ack], em seguida o servidor respode com [Psh] que e o index da pagina.

Quando cliente recebe o [Psh] ele responde com um [Ack]. Caso a pagina seja muito grande o servidor ira enviar outro [Psh] , cliente responde [Ack], ate que pagina esteja completa.

Quando chega a o final tanto o cliente tanto servidor pode finalizar a conexao, sendo assim servidor responderia [Fin], cliente responde [Ack]. 
Aqui fechou o canol do servidor para cliente. 

Agora falta fechar do cliente para servidor. Entao cliente responde [Fin], servidor respode [Ack].

![http_dentro_do_tcp](img/http_dentro_do_tcp.png)


O ip nessa figura, que e o encapsulamento e igual uma encomenda dos correios. Voce nao ve o que esta dentro apenas fora, fora e o ip. Entao quando pacote chega, ele chega como ip. Voce abre ele, descarta o ip e surge um tcp de dentro do ip. O tcp nao enxerga o ip apenas as portas, nessa caso a porta 80.

<br />

### Utilizando telnet com tcpdump

Utilizando o telnet para fazer conexao tcp e usuando tcpdump para monitorar a conexao.

`root@terminal:~# tcpdump -ni lo port 80`
![tcpdump_port](img/tcpdump_port.png)
  - aqui tcpdump esta monitorando a porta 80

`root@terminal:~# telnet 127.0.0.5 80`

![telnet_conect](img/telnet_conect.png)
  - aqui telnet inicia uma conexao na porta 80. Apartir dai o tcpdump comeca sua captura de trafego de rede. Exemplo a baixo:
![tcpdump_captura](img/tcpdump_captura.png)

Analisabdo conteudo em ascii2

`root@terminal:~# tcpdum -nr arquivo.pcap -A | less`
![payload_ascii](img/payload_ascii.png)
  - aqui e pessivel ver detalhas do payload, ex:
    - navegador Mozila firefox apartir de um ambiente grafico x11.
    - sistema operacional linux

Obs: Exelente programa para fazer extracao de png e o **tcpxtract**.

<br />

### UDP

![udp_protocolo](img/udp_protocolo.png)

  - UDP nao e orientado a conexao e tem 32 bits de lagura.
  - checksum do UDP e opcional.
  - udp nao tem flags.
  - netcat e utilizado para conexao upd e tcp.
  
Ferramenta exelente para injecao de pacotes e o **packit**.

<br />

### ICMP

![cimp](img/icmp.png)
  - Ele e essencial para controle dos procolos ip com execao do tcp que se auto controla.
  - e utilizado para controlar as atividades de rede.
  - Nao se bloqueia ICMP em redes! Isso nao cria seguranca e sem descontrole. O correto e controlar o ICMP pelo sistema de firewall.
  - Sistemas de firewall sao compostos por diversos elementos  como filtros de pacotes, proxies, IDS, IPS, verificadores de rede integridades etc. Firewall nao controlam somente TCP e UDP.
  
<br />

### Modelo OSI

![modelo_osi](img/modelo_osi.png)

  - Ele possui 7 camadas.
  - Cada uma das camadas tem PDU
  - Fisica manipula bits.
  - Enlace manipula quadros ou frames.
  - Rede pacotes ou datagramas
  - Transporte manipula seguimentos.
  - Sessao onde e relazado sessao das aplicacoes.

<br />

![modelo_osi_simplificado](img/modelo_osi_simplificado.png)
  - Modelo OSI simplificado

<br />

![modelo_osi_encapsulado](img/modelo_osi_encapsulado.png)
  - O modelo OSI, na pratica, e uma referencia ao encapsulamento de dados e protocolos, com niveis de preparacao e controle.
  - Um exemplo, utilizando o protocolo HTTP como aplicacao.

<br />

### Core

  - Core (Common Open Reserch Emulator) pode ser instalado diretamente no seu computador. No entando, ele tambem pode ser ativado rapidamente via Docker.

instalando docker:

![instalando_docker](img/instalando_docker.png)

<br />

![simulador de rede](img/simulador_de_rede_core.png)

<br />

### Fluxo TCP

  - Demonstracao de situacao de bloqueio de porta.
  - Demonstracao de fluxo simples.
  - Demonstracao de fluxo em trafego anomalo.

Bloqueando a porta 81 com **iptables**.

`root@terminal:~# iptables -A INPUT -p tcp --dport 81 -j DROP`

  - Quando se conecta em uma porta bloqueada, ex com telnet, nao avera reset, ira ocorrer conenction time aut.

Existem dois tipos de retrasmicao no **tcp**.
  - Restransmicao rapida que se chama **fast for-ward**.
    - A restransmicao rapida e feita por tempo que leva 1 segundo. Com isso e mandando o seguimento, se em 1 seguindo nao tiver resposta e remando o seguimento, redobra o tempo ate dar time out. Normalmente o seguimento e reenviado de 5 a 6 vezes dependendo do kernel do sistema.
  - Retransmicao a pedido. quando vem um **Ack** do lado oposto pedindo que seja restransmitido o seguimento com numero de sequencia.

[Fluxo simples], e o fluxo que nao tem nada de errado acontecendo com ele.

Gravando fluxo

`root@terminal:~# tcpdump -ni lo -v -w fluxo.pcap`

Agora fazendo telnet na porta 80, para tcpdump capturar o fluxo.

`root@terminal:~# telnet 127.0.0.5 80`

em seguida fazer `GET /`.

`root@terminal:~# tcpdump -n -r fluxo.pcap -S`

  - A opcao "-S" e para ver o numero de sequencia absoluto, que sera importante para a analise.

![captura_trafego](img/captura_trafego.png)

  - Temos o nosso cliente 127.0.0.1 eo servidor 127.0.0.5, aqui como ja sabemos eo ip do cliente que vem primeiro pois foi ele quem iniciou a conexao. Entao cliente diz ao servidor um [S] e que o numero de sequencia e 267556**2909**.
  - Servidor responde para cliente [S.] seq 267556**2910**. Aqui ele encrementou o sumero de sequencia.
  - A proxima vez que o cliente enviar alguma coisa para o servidor o numero de sequencia tem que ser o 267556**2910**.
  - Na terceira linha, o cliente responde com um Ack [.], lebrando que Ack nao tem numero de sequencia.
  - Na quarta linha cliente envia um push Ack [P.] enviando um GET /. Push tem numero de sequencia, que aqui e 267556**2910**. O tamanho do payload e 7 "length 7" entao 7+2010 = **2917**, ficando 267556**2917**, esse calculo e uma deducao matematica. Entao proxima vez que o cliente for enviar algo sera com **2917**.
  - Na quinta linha o servidor responde [.], ack 267556**2910**
    - Aqui o servidor responde que espera que seu proximo sequimento seja com **2917**.
  - Na sexta linha o servidor envia o index.html pois o cliente avia o pedido antes.
  - Na setima linha cliente diz para servidor Ack[.], ack nao e flag enta onao tem numero de sequencia.
  - Na oitava linha o servidor diz [F.] e espera que a proxima coisa que o cliente enviar sera com numero de sequencia **2917** "ack 2675562917".
  - Na nona linha o cliente diz [F.] com numero de sequencia **2917**, aqui como e um [F] o payload e zerado "length 0".
  - Na decima linha o servidor responde com Ack [.] e espera que proximo numero seja **2918**. 
    - Nesse caso aqui nao avera o proximo numero de sequencia, porem e assim que o servidor confirma que o cliente recebeu o payload. Assim o lado do cliente sabe que o servidor recebeu.

[Fluxo em trafego anomala]

`root@terminal:~# tcpdump -n -r anomalo.dump -S | cat -n | sed 's/^\n/' | less`

![trafego_anomalo](img/trafego_anomalo.png)

  - Trafego anomalo e por que, ou ouve perda de pacotes ip no caminho, ou os pacotes chegaram fora de ordem.
  - Primeira linha, cliente para servidor [S] seq 116031**8600**.
  - Segunda linha, servidor para cliente [S.] seq 24283**69942**.
  - Terceira linha, o cliente diz numero de sequencia **69943**.
  - Quarta linha, o cliente diz ao servidor o que ele quer [P.] "Push".
  - Quinta linha, servidor para cliente diz [.].
  - Sexta linha, se espera que o servidor envie um [P], enviando o que o cliente pediu.
    - Porem nao e o que se esperava, o servidor enviou um [F.], e alem dele nao responder o que o cliente pediu, ele finalizou, e esta fora de ordem, pois o seq e **72010** e deveria ser **69943**. Sabendo disso ja se sabe que os pacotes estao fora de ordem.
    - O cliente nao joga fora esse pacote pois sera util mais a frente, ele quardar no buffer dele.
    - Na proxima linha o cliente deveria enviar o que ele estava esperando, porem como ele nao recebe o que estava esperando, ele vai pedir novamente o que ele nao recebeu, **"retransmissao a pedido"**. 
    - Setima linha, cliente diz para servidor [A] **69943**
    - Oitava linha, se espera agora que o servidor envia para o cliente um [P] seq **69943**.
    Porem nao e o que o servidor envia.
    - Nona linha, cliente ira novamente pedir o que ele estava esperando, enta ele envia ao servidor [A] **69943**.
    - Decima linha, o servidor envia um [P] seq **69943**, dessa vez correto.
    - Decima primeira linha, agora o cliente responde [.] **72011** da oitava linha.
    
  Olhando o numero de identificao do ip sera possivel saber o que aconeteceu. Se o numero de identificacao do ip faltar numero, e sinal que ouve perda, mas se os numeros estiverem em sequencia mas no entando estiverem fora de ordem, nao ouve perda, a chegada se deu fora de ordem. Vamos ver:
  
  `root@terminal:~# tcpdump -n -r anomalo.dump -S -v | less`
  
  O atributto "-v" e para ver detalhes.
  
  O que vai nos interesar e o lado do servidor.
  
  ![dump_detalhes](img/dump_detalhes.png)
  (1:28:00 refazer essa parte)
    
<br />

### Protocolo ARP

  - E um procolo de descoberta de tipo de endereco de hardware e tipo de endereco de protocolo.
    - Qual mac esta ligado a qual endereco ip.

Utilizando arp:

Toda vez que uma maquina fizer um ping na minha rede, o arp vai circular e perguntar quem e 10.0.0.1, ai maquina oposta vai responder 10.0.0.1 sou eu e meu mac e : xx:xx:xx:xx:xx:xx:xx.

`root@terminal:~# tcpdump -n arp`

![arp_perguntando](img/arp_perguntando.png)

  - 192.168.0.72 esta perguntando quem e o navegador de borda 192.168.0.2
  - Entao objetivo e saber quem e 192.168.0.72, que esta frequentimente pingando na rede.
    - Pode ser um celular com malware.

![arp_mac](img/arp_mac.png)

  - Minha maquina que e 192.168.0.180 esta perguntando com arp qual mac de 192.168.0.202
    - 192.168.0.202 esta em endereco mac dc:bf:e9:0f:7f:e3

  - Agora que sabemos isso, isso vai para uma tabela local que ficar armazena de 30 segundos a 30 minutos, variando de sistema operacional.

`root@terminal:~# arp -n`

![arp_tabela_local](img/arp_tabela_local.png)

Netdiscover

  - Ele pega tudo que esta sendo ouvido na rede, e vai montando uma tabela de arp map.

`root@terminal:~# netdiscover`

![netdiscover](img/netdiscover.png)
  - Aqui vemos que nao se trata de um celular, provavelmente uma tv.
  
  - Vemos o basico de arp, arp pode ser usado em varios ataques.
  - Ataques que sao de dificil deteccao, mas que tem recursos para voce previnir, swits que tem port security cisco, voce ativa o port security, isso quer dizer o seguinte, se mudar o mac que esta entrando na quela porta, a porta e bloqueada. Problema e que ele nao avisa, tem que ficar vasculhando para saber.
  - Outra poscibilidade e voce enplementar o procolo 802x
  

<br />

### Roteamento visto no modelo OSI

![limite_rede](img/limite_rede.png)

  - O sistema operacional quando recebe uma mascara de rede, imediatamente converte em endereco de rede e em endereco de broadcast.
  - Endereco de rede e endereco de broadcast sao o limite superior e inferior da sua rede. Se estiver fora do limite, que e o caso do 11.10.15.23, precisara de roteamento.
  
  - Roteamento visto entre dois segmentos de rede:
  ![roteamento_entre-dois](img/roteamento_entre-dois.png)
  
  - Segmento de rede eo que esta de um dos lados do roteador de rede. Cada um dos lados do roteador e um segmento de rede, cada segmento tem que ter um enderecamento proprio.
  - 10.0.0.1 quer falar com 10.0.0.2, primeira pergunta que 0.0.1 faz, 0.0.2 pertence ao meu segmento de rede ? Sim. Porque 10.0.0.2 esta no mesmo segmento, pois esta no meio. Entao 0.0.1 manda um arp no segmento, perguntando, quem e 0.0.2 ? 0.0.2 responde sou eu e meu mac e xx:xx:xx:xx:xx:xx.
  
  - Roteamento visto pelo modelo OSI.
  ![roteamneto_modelo_osi](img/roteamneto_modelo_osi.png)
  
<br />

### Bridges

  - As bridges sao nossas aliadas na analise de trafego e em sistemas de firewall. Poderia se dizer que a brige e similar a um switch, diferenca e que switch tem varias portas.
  
  [como criar uma bridge](http://bit.ly/bridge_debian)
  
  - Existem dois tipos de briges, volatil e permanente:
    - Volatil, apos reiniciar computador, perdese tudo.
    - Permanente, mesmo reiniciando ela continua.

Criando uma Bridge

Para criar a bridge tem que ter o pacote **bridg-utils** instalado.
  - Primeiro passo e remover todos os ips da maquina que sera a bridge.

  - `root@terminal:~# brctl adbr br0`
    - Adicionando a bridge.
  - `root@terminal:~# brctl addif br0 eth0`
    - Criando a interface 0.
  - `root@terminal:~# brctl addif br0 eth1`
    - Criando a interface 1.
  - `root@terminal:~# brctl show br0`
    - Visualizando a bridge e suas interfaces.
  - `root@terminal:~# ifconfig br0 up`
    - Subindo a bridge.
