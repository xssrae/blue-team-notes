# Netflow
O **Netflow** é um ==protocolo de rede que coleta informações de tráfego IP==. Embora tenha sido desenvolvido pela Cisco, ele suporta Netflow de diferentes fabricantes. 

O Netflow ==funciona em uma estrutura **stateful** e monitora e relata todo o tráfego IP que passa pela interface monitorada==. Toda comunicação IP aqui é definida como um fluxo. Fluxo é o conjunto de pacotes que compõem a comunicação entre a origem e o destino.

![](https://letsdefend.io/images/training/network-log-analysis/generic-1.png)

Para criar dados do NetFlow, as configurações do NetFlow são configuradas nos roteadores ou switches suportados na rede. Essas configurações podem ser feitas sobre a linha de comando ou interface web do host.

Através das saídas do NetFlow, podemos detectar:
- Aumento do volume de tráfego anormal
- Vazamentos de dados
- Acesso a sistemas privados
- Novos IPs na rede
- Sistemas acessados pela primeira vez, bem como analisar questões relacionadas

---
# Análise de Registro de Firewall
Os firewalls são dispositivos físicos ou virtuais que controlam os pacotes de entrada e saída na rede de acordo com as regras criadas dependendo das políticas cibernéticas da rede. 

Os registros de firewall mais essenciais são os ==**logs do tráfego** que passa pelo dispositivo==. Basicamente, este log nos fornece tempo de tráfego, informações de IP/Port de origem, informações de IP/Port de destino, informações de interface, informações de localização, etc.

### Um log de tráfego de firewall de amostra

```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1653131198230012501 tz="+0300" logid="0000000013" type="traffic" subtype="forward" level="notice" vd="root" srcip=172.14.14.26 srcname="CNL" srcport=50495 srcintf="ACC-LAN" srcintfrole="lan" dstip=142.250.186.142 dstport=443 dstintf="Wan" dstintfrole="wan" srccountry="Reserved" dstcountry="United States" sessionid=445180938 proto=6 action="accept" policyid=284 policytype="policy" poluuid="8ec32778-a70a-51ec-9265-8fdf896d07f1" service="HTTPS" trandisp="snat" transip=89.145.185.195 transport=50495 duration=72 sentbyte=2518 rcvdbyte=49503 sentpkt=13 rcvdpkt=42
```

## Olhando para os detalhes do log
 O registro de firewall nos fornecerá as informações sobre a origem e o destino do tráfego, bem como em que porta é realizada.

- **aceitar:** indica que o pacote passou com sucesso.
- **deny:** a transmissão de pacote é bloqueada, as informações são retornadas de volta ao endereço IP que está bloqueada.
- **drop:** a transmissão do pacote está bloqueada. Nenhuma informação é devolvida ao endereço IP que está bloqueada.
- **close:** indica que a comunicação é mutuamente encerrada.
- **client-rst:** indica que a comunicação foi encerrada pelo cliente.
- **server-rst:** indica que a comunicação foi terminada pelo servidor.

- Existe uma solicitação de aceitação em momentos diferentes do endereço IP que foi detectado como ataque e negado pelo IPS em logs de firewall?
- Verificando os logs de firewall, você poderá descobrir se há acesso a / dos IPs suspeitos / Domínios obtidos como resultado da análise do conteúdo malicioso nos logs do antivírus.
---
# Análise de Log VPN
Dados como ==informações de tempo, informações de IP de origem, informações do usuário nos registros de VPN== estão entre as informações mais úteis para os analistas ao investigar eventos / alardes.

As VPNs são geralmente usadas pelo Firewall existente da organização (firewall que suporta VPN). Além disso, é possível ver produtos que fornecem serviços dedicados apenas para VPNs em algumas redes. Em resumo, os logs de VPN podem ser obtidos a partir de dispositivos Firewall, bem como outros dispositivos que fornecem apenas serviços VPN.
### Um exemplo de log VPN
```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1653134913959078891 tz="+0300" logid="0101039424" type="event" subtype="vpn" level="information" vd="root" logdesc="SSL VPN tunnel up" action="tunnel-up" tunneltype="ssl-web" tunnelid=462105151 remip=13.29.5.4 user="letsdefend-user" reason="login successfully" msg="SSL tunnel established"
```

Quando revisamos o log de vpn de amostra acima, ==podemos detectar que um acesso VPN bem-sucedido foi estabelecido como o endereço IP que faz a solicitação VPN é 13.29.5.4, o nome do usuário é "lede-user-soludo" e a mensagem produzida pelo dispositivo pertencente à atividade VPN é "login com sucesso"==.

Atividades suspeitas pode ser detectado através dos logs da VPN:
- Acessos VPN bem-sucedidos / não bem-sucedidos
- Detecção de ataques de força bruta contra contas de VPN
- Detecção de acessos VPN fora dos países especificados
- Detecção de acessos VPN fora dos períodos de tempo especificados

---
# Análise de Log de Proxy
O Proxy basicamente atua como uma ponte entre o endpoint e a internet. As organizações geralmente usam a tecnologia proxy para fins como velocidade da Internet, controle centralizado e aumento do nível de segurança. Um simples desenho esquemático da estrutura do Proxy é compartilhado abaixo. As solicitações feitas pelo cliente chegam primeiro ao Servidor Proxy e depois à Internet. Proxies podem basicamente trabalhar em 2 tipos diferentes:

  
- **Proxy transparente:** ==Servidor alvo que acessamos pode ver o endereço IP de fonte real==.
- **Proxy Anônimo:** ==O servidor alvo que acessamos não pode ver o endereço IP de origem real==. Ele vê o endereço IP do proxy como o endereço IP de origem. Assim, não pode obter qualquer informação sobre o sistema que realmente fez a solicitação em segundo plano.



![](https://letsdefend.io/images/training/network-log-analysis/proxy.png) 
## Um log de proxy de amostra:
```
data-2022-05-21 hora 16:15:44 tipo "utm"utm" subtype"webfilter" eventtype?"urlfilter" level?"avivalning" srcip'192.168.209.142 srcport-34280 srcintfrole?"lan" dstip .-Guest" action -"blovado" url?"https://android.prod.cloud.netflix.com/") sentbyte 517 rcvdbyte'0 direction'outgoing" urlsource?"Local URL filter Block" msg."URL foi bloqueado porque está na lista de filtros de URL"
```

Quando analisamos o log, vemos que a solicitação foi bloqueada para acessar o endereço “https[:]/android[.]cloud[.]netflix.com/” do sistema com o endereço IP 192.168.209.19.142 no grupo “Wifi_Guest” devido à política aplicada ao perfil relevante. A razão pela qual esta solicitação foi bloqueada é porque o URL a ser acessado está na lista "Blocoblor de filtro de URL local" e o acesso aos URLs nessa lista está bloqueado.

Os ==logs de proxy são um dos tipos de log mais importantes quando um analista SOC precisa verificar qual domínio / URL um sistema (servidor, cliente, etc.) está fazendo uma solicitação aos nossos sistemas internos e se foi capaz de estabelecer uma conexão bem-sucedida==. Também é importante determinar se o domínio/URL é uma categoria arriscada e se foi possível estabelecer quaisquer conexões bem-sucedidas antes.

- Podemos detectar as seguintes atividades suspeitas através da revisão dos logs de proxy:
- Conexões de URLs suspeitas
- Detecção de sistema infectado
- Detecção de atividades de tunelamento

---
# Análise de Log IDS/IPS
### IDS vs IPS

- IPS: Sistema de Prevenção de Intrusão - Detecta e previne as atividades suspeitas
- IDS: Sistema de Detecção de Intrusão - Apenas detecta as atividades suspeitas

==IDS e IPS têm base de dados de assinatura. Uma assinatura é um conjunto de regras projetadas para detectar ataques conhecidos. A estrutura que apresenta esse conjunto de regras centralmente é chamada de banco de dados de assinaturas==. Um link de banco de dados de assinatura de código aberto é compartilhado abaixo. Esses bancos de dados são constantemente atualizados contra vetores de ataque recém-formados. As atividades de rede que desencadeiam essas assinaturas podem ser bloqueadas ou detectadas apenas de acordo com a ação determinada da assinatura.

==Os sistemas IDS/IPS são uma das fontes que gerarão os alarmes mais frequentes entre todas as ferramentas de segurança para a detecção de ataques baseados em rede ou host. Como muitos ataques estão na rede ou no ponto final, os sistemas IDS/IPS podem detectar e bloquear muitas atividades suspeitas==. Muitas categorias de ataque diferentes, como ataque log4j, atividades pós-digitalização, explorações de vulnerabilidade, atividades de botnet podem ser detectadas e prevenidas com a ajuda de tecnologias IDS/IPS que são soluções de segurança vitais para as organizações.

<<<<<<< HEAD
Os analistas SOC geralmente ==podem acessar esses outputs produzidos por IDS / IPS via SIEM ou SOAR==. 

=======
Os analistas SOC geralmente ==podem acessar esses outputs produzidos por IDS / IPS via SIEM ou SOAR==.
>>>>>>> c16d4f52492b19b1725cacc4fc001c49efe01458
### Um log IPS de amostra
```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1650585615163261716 tz="+0300" logid="0419016384" type="utm" subtype="ips" eventtype="signature" level="alert" vd="root" severity="high" srcip=12.11.2.4 srccountry="Reserved" dstip=19.66.201.16 dstcountry="United States" srcintf="AOS_LAN" srcintfrole="lan" dstintf="Wan_RL" dstintfrole="lan" sessionid=254830141 action="detected" proto=17 service="DNS" policyid=2 poluuid="6b5c8674-a36a-51ec-bbfd-2250544a9125" policytype="policy" attack="DNS.Server.Label.Buffer.Overflow" srcport=57673 dstport=53 direction="incoming" attackid=37088 profile="default" ref="http://www.fortinet.com/ids/VID37088" incidentserialno=254762092 msg="misc: DNS.Server.Label.Buffer.Overflow" crscore=30 craction=8192 crlevel="high"
```

<<<<<<< HEAD
Após informações devem ser investigadas em detalhes ao analisar os logs IDS/IPS;

- A direção do ataque (inbound ou outbound) deve ser verificada.
- O nível de gravidade do evento deve ser verificado. Os níveis são geralmente definidos como baixo, médio, alto, crítico. Níveis altos e críticos indicam que a atividade é mais importante, é necessária uma ação rápida e um falso positivo é menos provável.
---
# Análise de Log de WAF
WAF (Web Application Firewall) é a tecnologia usada para proteger aplicativos baseados na web. A análise de firewall ou logs IDS/IPS sozinhos geralmente não é suficiente para a detecção de ataques baseados na web. As principais razões para isso são o problema de descarregamento SSL e o controle dos dados na parte da carga (dados) da solicitação da web.

O SSL Offload é a descriptografia do tráfego criptografado pelo SSL. O principal objetivo do sistema é reduzir a carga e aumentar o desempenho, bem como descriptografar o tráfego / solicitação criptografado para tornar o conteúdo visível e controlável do ponto de vista de segurança. Desta forma, os vetores de ataque invisíveis no tráfego criptografado tornam-se detectáveis ou evitáveis.
  
Em redes equipadas com WAF, as solicitações dos usuários finais chegam ao WAF primeiro pela internet. Em seguida, o WAF inspeciona a solicitação e toma a decisão se ela será transferida para o Servidor Web ou não. Uma das maiores vantagens dos WAFs aqui é que ele pode executar SSL Off-load, o que ajuda a examinar o conteúdo do tráfego HTTPS. A WAF sem capacidade de descarregamento SSL não pode fornecer uma proteção completa e eficaz, pois não poderá inspecionar a parte de carga (dados) da comunicação HTTPS.

  

![](https://letsdefend.io/images/training/network-log-analysis/WAF.png)

  

Os produtos F5 Big-IP, Citrix, Imperva, Forti WAF são exemplos de soluções WAF que são bem conhecidas no mercado. Além disso, as soluções Cloudflare, Akamai, AWS WAF também são usadas como soluções WAF em nuvem.

  

Os sistemas WAF são geralmente os sistemas que lidam com as solicitações de acesso à web nos sistemas públicos enfrentados. Portanto, podemos dizer que os ==WAFs são os primeiros sistemas a detectar ataques da web== e os registros WAF são os que ajudam os analistas SOC a detectar atividades suspeitas. Os analistas precisam saber sua localização na rede claramente ao analisar os registros do WAF. Os registros WAF são a fonte dos logs para visualizar todas as solicitações da Web feitas e analisar ataques detectados na Web ou ataques bloqueados na web. Ao examinar os alertas gerados para ataques detectados ou bloqueados, a reputação do endereço IP de origem que criou o log / alerta deve ser analisada também outras atividades semelhantes que o IP de origem criado em outras fontes de log (como IDS / IDS, Firewall) deve ser investigada.


### Um log de amostra de WAF:

data-2022-01-26 hora'19:47:26 log_id-20000008 msg_id'000018341360 deviced_id-FVVM08 vd'"root" timezone"(GMT+3:00)Istambul" timezone_dayst'"GMTg-3" type-attack' main_type"Alert_Policy" src-19.6.150.138 src_port-56334 dst-172.16.10.10 dst_port-443 http_meth-od-get http_url??v?(SELETO (CHR(113)|CHR(120)|CHR(120)|CHR(120)|CHR(118)|CHR(118)|CHR(118)|CEND))::text" http_host"app.letsdefend.io" http_agent""Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.9b1) Gecko/2007110703 Firefox/3.0b1" msg"" Parameter (Passa-segue) acionado ID 030000136"Digite"SQL Injection" (em inglês)


Quando o registro de amostra WAF é analisado, as informações IP de origem e de destino devem ser verificadas, pois faz referência a um tipo de ataque de injeção de injeção de alto nível de gravidade por meio da detecção de assinaturas. A resposta do WAF a esta solicitação deve ser verificada se o ataque relatado for um ataque da web genérico (Intection, XSS, etc.) genérico como acima. Se o WAF não bloqueou esta solicitação, a resposta retornada pelo aplicativo deve ser verificada. O código de resposta da resposta da aplicação (IIS, Apache, Nginx, etc.) também é importante e deve ser investigado. Se o aplicativo respondeu 200 para um ataque que o WAF não poderia impedir, isso significa que o ataque chegou ao servidor web e retornou uma resposta bem-sucedida. Em alguns casos, o aplicativo retorna o código 200, enquanto ele deve realmente retornar o código 404 devido a algumas deficiências técnicas no aplicativo. Estes podem ser considerados como falsos positivos para os pedidos relevantes.

  

Exemplos de algumas das respostas da candidatura;
- 200 (OK): O pedido foi recebido com sucesso e a resposta foi devolvida.
- 301 (Redirecionamento Permanente): O pedido foi redirecionado para um local diferente.
- 403 (proibido): Não é permitido o acesso de dados solicitados.
- 404 (Não encontrado): O conteúdo solicitado não pôde ser encontrado.
- 503 (Serviço Indisponível): O servidor não pode responder. 

Categorias do código de resposta:
- Respostas informativas (100-199)
- Respostas bem sucedidas (200-299)
- Mensagens de Redirecionamento (300–399)
- Respostas de erro do cliente (400-499)
- Respostas de erro do servidor (500–599)

  

A solicitação de conexão no registro de amostra WAF compartilhada acima foi bloqueada devido às assinaturas que o WAF reconhece como maliciosa e gerou um alerta sobre ele por causa das expressões no URL dentro da solicitação provenientes do endereço IP 19.6.150.138 para a porta 443 do host 172.16.10.10 atrás do WAF. O nome da política aplicado para solicitações correspondentes a essa assinatura no WAF é "Alert_Policy" e a ação está definida como "alerta", que é o modo de monitoramento. Portanto, podemos dizer que o pedido chegou ao anfitrião de destino.

  

Se o ataque relatado pelo WAF para as solicitações for para detectar vulnerabilidades, é necessário analisar os detalhes da vulnerabilidade a ser detectada aqui. Por exemplo, se o seu aplicativo da Web está sendo executado no ASP e a detecção de vulnerabilidade é uma varredura específica do aplicativo PHP, então não se pode esperar que tal vulnerabilidade seja relatada. No entanto, ainda seria uma boa prática tomar quaisquer ações para o endereço IP que executam a atividade de digitalização. A melhor ação a ser tomada aqui é bloquear as solicitações de entrada no primeiro dispositivo de segurança no gateway onde as solicitações de entrada interagem pela primeira vez com a nossa rede.
 

Podemos ajudar a usar logs WAF ao analisar as seguintes detecções:
- Detecção de vulnerabilidades web conhecidas
- Detecção de variedade de ataques web como Injeção SQL, Ataque XSS, Injeção de Código, Diretório Traversal
- Detecção de uso de método suspeito, como PUT, DELETE
- Informações de endereço IP solicitantes
- Informações de URL mais solicitadas

**Método de solicitação:** Indica qual método a solicitação é feita dentro da linguagem web. Os principais métodos de solicitação são os seguintes.

- GET: É usado para recuperar dados do servidor
- POST: Ele é usado para enviar dados para o servidor (como imagem, vídeo)
- DELETE: É usado para excluir os dados no servidor
- PUT: Ele é usado para enviar dados para o servidor (os dados enviados criam ou atualizam arquivos)
- OPTIONS: Diga quais métodos o servidor aceita
=======
Um ==estado de gatilho de assinatura diferente deve ser verificado entre a mesma fonte e alvo==. Acionar diferentes assinaturas significa que o nível de gravidade do evento deve ser aumentado e uma ação mais rápida deve ser tomada. O evento é resolvido dentro do acordo de nível de serviço (SLA) dependendo do seu nível de gravidade em caso de seguintes situações como:

- Se uma única assinatura for acionada,
- Não há pedidos diferentes da fonte relevante,
- Não há aceitação diferente nos logs de firewall.
- A porta/serviço é especificado no detalhe de ataque em execução na porta de destino? Se estiver em execução, o nível do evento deve ser elevado ao nível crítico, e o sistema alvo deve ser verificado para infecção. Também deve ser verificado se uma resposta foi devolvida ao sistema relevante a partir da fonte. Se a resposta for não, bloquear o endereço IP de ataque como precaução seria uma ação apropriada.
- A ação é tomada apenas deteção ou também foi bloqueada? Se o ataque for bloqueado e não houver outras solicitações do mesmo endereço IP no firewall, podemos esperar um pouco mais para tomar a ação. No entanto, se a ação tomada para o ataque for apenas uma detecção, outras solicitações semelhantes devem ser revisadas e a ação de bloqueio deve ser aplicada se o conteúdo das solicitações provenientes do endereço IP não for falso positivo.


Após atividades suspeitas pode ser detectado monitorando os registros IDS/IPS;
- Atividades de digitalização portuária
- Exames de vulnerabilidade
- Ataques de injeção de código
- Ataques de Bruto-Força
- Ataques Dos/Ddos
- Atividades de Trojan
- Atividades de botnet
---
#  Análise do Web Log
Hoje, a maioria dos serviços é baseada na web e os serviços da web das organizações são os serviços mais comuns que estão abertos para o mundo exterior. Isso vem com muito interesse para os ataques da web do ponto de vista dos atacantes. Portanto, é muito importante que os Analistas de SOC sejam capazes de analisar os logs da web corretamente. Os servidores web mais comumente usados são o Microsoft IIS, Apache, Nginx. Embora os aplicativos sejam diferentes, os logs do servidor web têm conteúdo semelhante.

### Um log de servidor web de amostra

```
71.16.45.142 - - - [12/Dez/2021:09:24:42 +0200] "GET /?id-SELECT+-+FROMs HTTP/1.1" 200 486 "-" "curl/7.72.0"
```

**URL solicitado:** Indica o diretório/file no servidor que a solicitação foi feita. Ao mesmo tempo, se houver um ataque, ele pode ser detectado. Como no exemplo acima, as instruções “SELECT++FROM+users” representam-nos um padrão de ataque “Injeção SQL”. Examinar URLs é muito importante na análise de log da web.

### Tipos de ataque da Web e URLs de solicitação de amostra

![](https://letsdefend.io/images/training/network-log-analysis/WEB.png)


**Resposta do servidor:** O servidor responde às solicitações com algumas expressões numéricas. Esses códigos de resposta indicam se a solicitação é bem-sucedida ou não.

  

Digamos que você encontre que o URL contém informações sobre o vetor de ataque de injeção sql ao analisar os logs da web, então você deve prestar atenção à resposta do servidor da web;

- ==Se 200 é retornado:== A solicitação chegou com sucesso ao servidor e o servidor respondeu com sucesso, e o ataque foi bem sucedido. Por vezes, as falhas de aplicação fazem com que os servidores respondam com 200 enquanto deveriam retornar 404. Nesses casos, para esclarecer isso, é necessário consultar o URL e analisar a resposta dada à solicitação.

- ==Se 404 for retornado:== O servidor retornou "Não encontrado" porque a url solicitada não foi encontrada no servidor. Em outras palavras, consideramos que o ataque falhou.

- ==Se 500 é retornado: == O servidor não poderia interpretar esta solicitação e uma resposta "Erro de servidor" foi retornada. Em outras palavras, podemos interpretá-lo como o ataque falhou. No entanto, como essas solicitações no lado do servidor impedem que o serviço da Web funcione corretamente, ele é considerado um ataque DOS causando uma interrupção do serviço enquanto o invasor queria fazer um ataque na web.


Os significados desses códigos de status são os seguintes.
- 200 (OK): O pedido foi recebido com sucesso e a resposta foi devolvida.
- 301 (Redirecionamento Permanente): O pedido foi redirecionado para um local diferente.
- 403 (proibido): não foi permitido o acesso aos dados solicitados.
- 404 (Não encontrado): O conteúdo solicitado não pôde ser encontrado.
- 503 (Serviço indisponível): Ocorre quando o serviço do servidor não pode responder.

>**Informações do User-Agent:** Indica o aplicativo que foi utilizado para o pedido. As informações do User-Agent ajudarão a entender se as solicitações feitas são por um usuário real ou uma ferramenta de verificação automatizada durante a análise de log da web. Algumas das ferramentas automatizadas de digitalização da web são “nikto”, “nessus”, “nmap”. Se virmos "Mozilla, Chrome" ou informações semelhantes do navegador da Web na seção de informações do User-Agent, isso significa que a solicitação foi feita por um usuário real. 

### Análise de amostra web request, web log e saída
#### Pedido da Web

```
192.168.8.11/bwapp/sqli_1.php?title ?% 25iron%27+union+seleção+1%2C% 20%29%2C2C4%2C25%2C7--+-%25%27

```

## Pedido da Web Decodificado:
Você pode decodificá-los em [URL Decoder](http://meyerweb.com/eric/tools/dencoder)
```
192.168.8.11/bwapp/sqli_1.php?title-%iron' union select 1,user(),3,4,5,6,7-- - %'&action
```
#### Saída do navegador da solicitação da Web

![](https://letsdefend.io/blog/wp-content/uploads/2022/10/bwapp.png)

### Log da Web
```
192.168.8.54 - - [29/Jun/2022:07:42:42:48 +0300] "GET /bwapp/sqli_1.php?titleTM%25iron%27+union+select+1%2Cuser%29%2C3%2C2C 25%2C7----+%25%2C7-+25%227&action-Wig'"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/102.0.0.0 Safari/537.36"
```

A análise de log do ataque na web acima mostra que o ataque foi uma injeção de SQL, feita a partir de 192.168.8.54, e foi bem sucedida. Podemos ver que foi uma ==injeção SQL==, pois o URL da solicitação contém expressões como "union" e "selecionar", a resposta do servidor web foi de 200, e o analista foi capaz de confirmar que ele foi capaz de acessar as informações do banco de dados sobre o usuário "root-localhost".

---
# Análise de Log DNS

O DNS é um dos blocos de construção mais básicos da Internet. O DNS é basicamente uma tecnologia que é usada para o domínio - resolução IP. O tráfego de rede é basicamente realizado através de IPs e o DNS é o sistema que nos diz qual o endereço IP do servidor do google.com quando precisamos acessar "google.com".

  
==Os analistas do SOC geralmente usam logs DNS para verificar quais domínios e quando foram solicitados durante uma investigação de incidente de um sistema==. Devemos manter os seguintes itens ao verificar estes registros:

Por exemplo, a captura de tela abaixo mostra o evento sobre a exclusão do Event_ID: 516 deneme.c.local com os detalhes de quem o excluiu e em que servidor foi excluído dentro da zona Padrão.

  

![](https://letsdefend.io/images/training/network-log-analysis/dns1.png)

  

Os aplicativos que fornecem serviços de servidor DNS, como Microsoft DNS, Bind DNS, Dnsmasq, registram as consultas DNS que recebem mediante solicitação. Os logs de vinculação, que são serviços de servidor DNS geralmente usados em sistemas Linux, podem ser acessados através do arquivo de log "/var/log/querylog" na configuração padrão.

### Um log DNS de amostra
```
{ "timestampt": 1591367999.306059, "source_ip": "192.168.4.76", "source_port": 36844, "destination_ip": "192.168.4.1", "destination_port": 53, "protocol": "udp", "query": "testmyids.com", "qtype_name": "A", }
```

#### Os logs de consulta DNS geralmente contêm os seguintes dados
- Data-Hora
- Consultando IP, porta
- Tipo de consulta
- O domínio solicitado
  
Como o registro de exemplo acima é retirado de um produto (Bro/Zeek) que captura registros DNS na rede externa fora do servidor DNS, há também as informações do servidor onde a consulta foi feita junto com o IP que fez a consulta. Por esse motivo, os logs DNS podem ser obtidos diretamente do servidor, bem como nos sistemas que coletam essas consultas pela rede.

- Primeira vez visitado domínios
- Detecção de domínios de retorno NX
- Controles de IOC de domínio
- Detecção de DNS sobre TLS, DNS sobre acessos HTTPS

Quando os registros DNS abaixo são analisados, vemos que há solicitações de DNS feitas em relação a subdomínios que foram criados aleatoriamente a partir do endereço IP 192.168.10.12 no período de 1 minuto. Esta atividade de solicitações de DNS pode ser um sinal para uma ==potencial atividade de tunelamento de DNS. ==A investigação deve ser conduzida no ponto final determinando o processo de origem que cria essa atividade.

![](https://letsdefend.io/images/training/network-log-analysis/dns.png)

Nossas investigações no registro DNS abaixo mostram que os domínios solicitados parecem ser legítimos. Considerando que o servidor Oracle Database com um endereço IP de 192.168.10.3 está consultando esses domínios, o servidor Oracle perguntando aos domínios dos serviços da Microsoft usados para transferência de dados torna essa atividade suspeita.

```
Feb 5 09:12:11 ns1 named[80090]: client 192.168.10.3#3261: query: login.microsoftonline.com IN A

Feb 5 09:13:11 ns1 named[80090]: client 192.168.10.3#4536: query: onedrive.live.com IN A
```
>>>>>>> c16d4f52492b19b1725cacc4fc001c49efe01458
