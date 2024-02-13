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

## Através dos logs de firewall, atividades suspeitas como:
- Atividades Port-Scan
- Detecção de comunicação com IoCs
- Acesso não autorizado (lân-la-l) ou vertical (lan-wan, wan-lan) pode ser detectado
---
### Análise de Log VPN
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


Por exemplo, quando o log do Portal de Segurança Web do Forcepoint abaixo é examinado;

```
Jun 17 10:47:00 10.10.18.11 CEF:0|Forcepoint|Security|8.5.4|194|Transaction bloqueado|7| appTMbloqueado appTMhtps dvc-10.10.18.11 dst-104.26.11.18 dhost-sentry-proxy.cargox.cc dpt?443 src?10.80.18.50-Mozilla/5.0 (Windows NT 10.0; Win64; x64) cs1Label-Policy cs1-Block_Risk_Category_Policy (Serversy) request-https://sentry-proxy.cargox.cc/api/3/envelope/?sentry_key

```
O usuário do Test_User enviou uma solicitação POST para o endereço “https[:]//sentry-proxy[.]cargox[.]cc” com o navegador Mozilla sobre seu servidor com um endereço IP de 10.80.18.50 (foi determinado pelo nome da política), e o endereço de destino foi determinado como “Block_Risk_Category_Policy” e bloqueio de ação.

---
# Análise de Log IDS/IPS

### IDS vs IPS

- IPS: Sistema de Prevenção de Intrusão - Detecta e previne as atividades suspeitas
- IDS: Sistema de Detecção de Intrusão - Apenas detecta as atividades suspeitas


==IDS e IPS têm base de dados de assinatura. Uma assinatura é um conjunto de regras projetadas para detectar ataques conhecidos. A estrutura que apresenta esse conjunto de regras centralmente é chamada de banco de dados de assinaturas==. Um link de banco de dados de assinatura de código aberto é compartilhado abaixo. Esses bancos de dados são constantemente atualizados contra vetores de ataque recém-formados. As atividades de rede que desencadeiam essas assinaturas podem ser bloqueadas ou detectadas apenas de acordo com a ação determinada da assinatura.

==Os sistemas IDS/IPS são uma das fontes que gerarão os alarmes mais frequentes entre todas as ferramentas de segurança para a detecção de ataques baseados em rede ou host. Como muitos ataques estão na rede ou no ponto final, os sistemas IDS/IPS podem detectar e bloquear muitas atividades suspeitas==. Muitas categorias de ataque diferentes, como ataque log4j, atividades pós-digitalização, explorações de vulnerabilidade, atividades de botnet podem ser detectadas e prevenidas com a ajuda de tecnologias IDS/IPS que são soluções de segurança vitais para as organizações.

Os analistas SOC geralmente ==podem acessar esses outputs produzidos por IDS / IPS via SIEM ou SOAR==. O SIEM apresenta os alarmes IDS/IPS coletados ao Analista SOC, transformando-os em alarmes com várias regras/correlações de acordo com seu nível, categoria e ocorrência em determinado número de vezes. Esses alertas podem ser investigados como um caso independente ou como um grupo, associando-os a diferentes alertas (Algumas SIEMs também podem estabelecer essa relação). Por exemplo, após a atividade de varredura portuária, a geração de eventos/alarmes na categoria de exploit em direção aos alvos que o país escanear a partir do mesmo endereço IP de origem será associada umas às outras e consideradas como um flagrodo vermelho do ponto de vista da segurança.


### Um log IPS de amostra
```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1650585615163261716 tz="+0300" logid="0419016384" type="utm" subtype="ips" eventtype="signature" level="alert" vd="root" severity="high" srcip=12.11.2.4 srccountry="Reserved" dstip=19.66.201.16 dstcountry="United States" srcintf="AOS_LAN" srcintfrole="lan" dstintf="Wan_RL" dstintfrole="lan" sessionid=254830141 action="detected" proto=17 service="DNS" policyid=2 poluuid="6b5c8674-a36a-51ec-bbfd-2250544a9125" policytype="policy" attack="DNS.Server.Label.Buffer.Overflow" srcport=57673 dstport=53 direction="incoming" attackid=37088 profile="default" ref="http://www.fortinet.com/ids/VID37088" incidentserialno=254762092 msg="misc: DNS.Server.Label.Buffer.Overflow" crscore=30 craction=8192 crlevel="high"
```


Após informações devem ser investigadas em detalhes ao analisar os logs IDS/IPS;

- A direção do ataque (inbound ou outbound) deve ser verificada.
- O nível de gravidade do evento deve ser verificado. Os níveis são geralmente definidos como baixo, médio, alto, crítico. Níveis altos e críticos indicam que a atividade é mais importante, é necessária uma ação rápida e um falso positivo é menos provável.

Um ==estado de gatilho de assinatura diferente deve ser verificado entre a mesma fonte e alvo==. Acionar diferentes assinaturas significa que o nível de gravidade do evento deve ser aumentado e uma ação mais rápida deve ser tomada. O evento é resolvido dentro do acordo de nível de serviço (SLA) dependendo do seu nível de gravidade em caso de seguintes situações como:

- Se uma única assinatura for acionada,
- Não há pedidos diferentes da fonte relevante,
- Não há aceitação diferente nos logs de firewall.
- A porta/serviço é especificado no detalhe de ataque em execução na porta de destino? Se estiver em execução, o nível do evento deve ser elevado ao nível crítico, e o sistema alvo deve ser verificado para infecção. Também deve ser verificado se uma resposta foi devolvida ao sistema relevante a partir da fonte. Se a resposta for não, bloquear o endereço IP de ataque como precaução seria uma ação apropriada.
- A ação é tomada apenas deteção ou também foi bloqueada? Se o ataque for bloqueado e não houver outras solicitações do mesmo endereço IP no firewall, podemos esperar um pouco mais para tomar a ação. No entanto, se a ação tomada para o ataque for apenas uma detecção, outras solicitações semelhantes devem ser revisadas e a ação de bloqueio deve ser aplicada se o conteúdo das solicitações provenientes do endereço IP não for falso positivo.


Por exemplo, no registro de exemplo dado acima, o ataque “DNS.Server.Label.Buffer.Overflow” foi detectado na solicitação feita a partir do endereço IP 12.11.2.4 para a porta 53 do endereço IP 19.66.201.16. Quando olhamos para os detalhes deste ataque que podem ser acessados através do ref. url no log, vemos que o Tftpd32 DNS Server foi afetado por este ataque. Se o serviço em execução na porta 53 da porta 19.66.201.16 não for o servidor DNS Tftpd32, podemos dizer que ele não foi afetado por este ataque. No entanto, o fato de que ele diz "detectado" na seção de ação significa que esse tráfego ocorre entre a origem e o destino e não está bloqueado. Em outras palavras, essa solicitação feita pelo endereço IP de origem chegou ao serviço em execução na porta 53 do endereço IP de destino.

Após atividades suspeitas pode ser detectado monitorando os registros IDS/IPS;
- Atividades de digitalização portuária
- Exames de vulnerabilidade
- Ataques de injeção de código
- Ataques de Bruto-Força
- Ataques Dos/Ddos
- Atividades de Trojan
- Atividades de botnet
---
