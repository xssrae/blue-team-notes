---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
# Introdução ao SOC
Bem-vindo ao primeiro passo de sua carreira como analista SOC. Nesta primeira seção, falaremos sobre a estrutura das ferramentas SOC e SOC. Vamos discutir por que um analista SOC precisa dessas ferramentas SOC (Centro de Operações de Segurança) e como usá-las de forma eficaz.

**O que você aprenderá durante todo o treinamento?**  
- A estrutura de um SOC
- A operação de um SOC
- SOC Ferramentas / Produtos
- Como um analista SOC deve usar suas ferramentas
- Erros frequentes que os analistas SOC cometem
## Tipos e funções SOC
### Posições de SOC
- **Analista de SOC**: Pode ser dividido em grupos como Nível 1, 2 e 3 de acordo com a estrutura SOC. Um analista de segurança classifica o alerta, *procura a causa e aconselha sobre medidas corretivas*.
- **Respondente de Incidente**: O oficial de resposta a incidentes é a pessoa que *participará da detecção de ameaças*. Esta pessoa realiza a avaliação inicial das violações de segurança.
- **Caçador de ameaças**: Um caçador de ameaças é um profissional de segurança cibernética que *procura e investiga ameaças e vulnerabilidades potenciais* dentro da rede ou sistema de uma organização. Eles usam uma combinação de técnicas manuais e automatizadas para detectar, isolar e mitigar ameaças persistentes avançadas (APTs) e outros ataques sofisticados que podem evitar medidas de segurança tradicionais.
- **Engenheiro de segurança**: Engenheiros de segurança mantêm a infraestrutura de *segurança das soluções SIEM (Security Information and Event Management)* e produtos SOC. Por exemplo, essa pessoa prepara a conexão entre os produtos SIEM e SOAR (Orqueação de Segurança, Automação e Resposta).
- **Gerente de SOC**: Um gerente de SOC assume *responsabilidades de gerenciamento*, como orçamento, estratégia, gerenciamento de pessoal e coordenação de operações. Ele / ela lida com questões operacionais e não técnicas.

## Analista da SOC e suas responsabilidades
### Rotina geral
- **Os sistemas operacionais**: Para ser capaz de detectar o que é anormal em um sistema, é preciso saber principalmente o que é aceito como normal. Por esta razão, você deve saber a *lógica básica de como os sistemas operacionais Windows / Linux funcionam*. 
- **Rede**: Em primeiro lugar, estaremos lidando com muitos IPs maliciosos e endereços de URL. E teremos que verificar se há algum dispositivo na rede tentando se conectar a esses endereços. Se pudermos controlar isso, então ele definirá o tom de nossa análise. Como um passo mais complicado, podemos ter que detectar um potencial vazamento de dados na rede. Para poder realizar todas essas funções, *precisamos conhecer os fundamentos do networking.* 
- **Análise de malware**: Você vai se deparar com algum tipo de software malicioso ao lidar com a maioria das ameaças. Para ser capaz de entender qual é o propósito real desses malwares (eles às vezes exibem comportamentos diferentes para enganar os analistas), você precisa ter algumas habilidades em análise de malware. É importante, pelo menos, determinar qual é o *comando e o centro de controle do arquivo malicioso* e se existe ou não um dispositivo que se comunica com esse endereço. 

 
Geralmente discutimos o que é um analista SOC, o que ele / ela faz, e que tipo de habilidades ele/ela precisa ter. Enquanto continuamos com o programa, abordaremos as áreas técnicas. Vamos começar pelo SIEM.

---
# SIEM e relacionamento de analistas

Isso geralmente será sobre o que é o SIEM, por que ele é utilizado dentro de um SOC e a relação entre o SIEM e um analista SOC.  
### O que é o SIEM?
O **gerenciamento de informações e eventos de segurança (SIEM)** é uma *solução de segurança* que fornece registro em tempo real de eventos em um ambiente. O objetivo real do registro de eventos é detectar ameaças de segurança.  
  
Em geral, os produtos SIEM têm uma série de recursos. São mais os que mais nos interessam como analistas da SOC: filtram os dados que coletam e criam alertas para quaisquer eventos suspeitos.  
  
Exemplo de um alerta: se alguém em um sistema operacional Windows tentar inserir 20 senhas incorretas em 10 segundos, isso é atividade suspeita. Não é provável que alguém que esqueceu sua senha tente inserir novamente sua senha tantas vezes em um período tão curto. É por isso que criamos uma regra/filtro SIEM para determinar tais atividades que excedem os valores limite. Devido a esta regra SIEM, um alerta será criado se tal situação ocorrer.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/siem/siem+alert.png)

  
  
Algumas soluções populares do SIEM: IBM QRadar, ArcSight ESM, FortiSIEM, Splunk, etc. Para obter uma imagem melhor, você pode se referir à página “Monitoramento” em LetsDefend.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/siem/siem-monitoring.PNG)

  
### Relação entre um analista SOC e SIEM
Embora as soluções SIEM tenham muitos recursos, como analistas SOC geralmente seguimos apenas alertas. Existem outros grupos/pessoas que desenvolvem configurações e correlações de regras.  

Como mencionamos acima, os alertas são criados por dados que são passados através de filtros. Os alertas são analisados principalmente por um analista SOC. É exatamente aí que começa o dever de um analista SOC no centro de operações de segurança. Fundamentalmente, ele/ela deve decidir se este alerta criado é uma ameaça real ou um alarme falso.  
  
Para entender melhor, vamos voltar para a página “Monitoramento”, como você vê abaixo, há vários alertas na interface do SIEM. Como analista da SOC, devemos analisar os detalhes relacionados a esses alertas com a ajuda de outros produtos SOC (como EDR, Log Management, Threat Intelligence Feed, etc.) e, por último, devemos determinar se são ou não ameaças reais.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/siem/alert-details.PNG)

  
  
Podemos ver alertas recém-criados no “Canal Principal”, podemos pensar neste canal como um canal compartilhado. Seus colegas de equipe não podem ser vistos nesta simulação, mas em uma situação de trabalho real seus colegas de equipe serão capazes de ver este painel. Depois de escolher o alerta em que deseja trabalhar, clique no botão “Take Ownership” na área chamada “Ação” para se apropriar do alerta e direcioná-lo para o “Canal de Investigação”. Desta forma, seus colegas de equipe poderão ver em qual alerta você está trabalhando ativamente. Ao mesmo tempo, isso os ajudará a ver em qual alerta você já está trabalhando para que eles possam escolher outros alertas. Desta forma, sua equipe pode examinar rapidamente todos os alertas.  
  
Quando você clica no alerta, você pode ver os detalhes relacionados. Desta forma, você pode coletar as informações (nome de host, endereço IP, informações de hash de arquivo, etc.) necessárias para a investigação.  

---
# Gestão de Log

Você estará fazendo uma grande análise de log como um Analista SOC. Por esta razão, é importante estar familiarizado com os sistemas/soluções “Gerenciamento de Log”. O produto da marca que você usa não é importante, mas o que é importante é saber o que procurar e onde procurá-lo.  
### O que é o Log Management?
Em suma, permite o acesso a todos os logs em um ambiente (web logs, logs do sistema operacional, Firewall, Proxy, EDR, etc.) e permite o gerenciamento desses logs de um ponto. Assim, melhora a usabilidade e economiza tempo.  
  
Se você acessar a página “Gerenciamento de log” no LetsDefend, verá várias fontes de registro, como Proxy, Exchange e Firewall listadas como “Tipo”. Isso significa que todas essas fontes de registro foram coletadas em um só lugar e podemos ver a saída de log de fontes como Proxy, FW, etc. com apenas uma consulta. 

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/log-management/log-management.PNG)

Como analistas SOC geralmente usamos “Gerenciamento de Log” para verificar se há comunicação com um determinado endereço e para ver os detalhes desta comunicação. Digamos que você se deparou com um malware e depois de executá-lo, detectou que ele havia se comunicado com o endereço “letdefend.io” e executasse comandos a partir dele. Nesta situação, o centro de controle de comando é “letdefend.io”, você pode procurar por “letdefend.io” no Log Management da sua empresa para ver se houve algum dispositivo tentando se comunicar com o centro de controle de comando.  

---
# EDR - Detecção e Resposta de Endpoint
Um analista SOC precisa gastar uma grande quantidade de tempo usando o EDR enquanto realiza análises em um dispositivo de endpoint. Nas seções a seguir, discutiremos por que o EDR beneficia os Analistas de SOC e como usá-lo de forma eficaz.  
### O que é EDR?
A detecção e resposta de endpoints (EDR), também conhecida como detecção e resposta a ameaças de endpoint (ETDR), é uma solução integrada de segurança de endpoint que combina monitoramento contínuo em tempo real e coleta de dados de endpoint com recursos de resposta e análise automatizadas baseadas em regras. (Fonte de definição: mcafee.com)  
#### **Análise com o EDR**  
Algumas soluções populares de EDR usadas no local de trabalho: 
- CarbonBlack
- SentinelOne
- FireEye HX.  


![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/edr-letsdefend.PNG)

  
Os dispositivos de endpoint acessíveis são listados à esquerda. Podemos procurar endpoints na barra de pesquisa ou se tivermos um COI (-Indicador do Compromisso - um endereço IP, hash de arquivo, nome do processo, etc.) podemos realizar uma pesquisa entre todos os hosts.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/list-endpoint.PNG)

  
  
No lado direito, podemos encontrar informações gerais sobre o dispositivo e seções exibidas, como “Histórico do navegador”, “Conexões de rede” e “Lista de processos”.  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/edr-letsdefend.PNG)

  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/process-list.PNG)

#### **Investigação ao vivo**  
Além disso, podemos clicar no botão “Conectar” e acessar a própria máquina para continuar nossa análise lá.  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/edr-connect.PNG)
#### **Contenção**  
Temos de isolar uma máquina hackeada da rede. Há razões importantes por trás disso: ser capaz de parar a conexão do atacante com a rede interna e impedir seu movimento em toda a rede interna.  
  
Portanto, o dispositivo deve ser cortado das redes internas e externas até que as lacunas de segurança sejam corrigidas e o dispositivo seja usado novamente. Podemos garantir que o isolamento aconteça usando o recurso “Contenção” das soluções EDR. Esse recurso permite que o dispositivo selecionado se comunique apenas com o centro EDR. Isso significa que, embora o dispositivo esteja isolado da rede, ainda podemos continuar nossa análise.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/edr/containment.PNG)
#### **Dica rápida**  
Se você tiver algum tipo de COI, como um hash de arquivo, nome do arquivo, etc., você pode realizar uma pesquisa no EDR entre todos os hosts e ver se há uma correspondência. Por exemplo, digamos que você tenha certeza de que um dispositivo foi invadido e obteve um arquivo com um hash MD5 de “ac596d2822e2f9b1501d66fce5a451f00”. Você pode procurar esse valor de hash no EDR e determinar se esse arquivo está presente ou executado em outros dispositivos. Portanto, você pode entender quem foi afetado por este ataque.  
### Conclusão
Cobrimos os fundamentos do EDR que você usará com a frequência do Log Management. Nós testemunhamos que os analistas não são capazes de usar efetivamente as soluções EDR, por isso, se você gastar algum tempo neste tópico, isso o colocará um passo na frente da multidão.  

---
# SOAR (Automação e Resposta de Orquestração de Segurança)
SOAR significa Automação e Resposta de Orquestração de Segurança. Ele permite que produtos e ferramentas de segurança em um ambiente trabalhem entre si, facilitando as responsabilidades dos membros da equipe SOC. Por exemplo, ele procurará automaticamente o VirusTotal para o IP de origem de um alerta SIEM, reduzindo a carga de trabalho do analista SOC.  
  
Alguns produtos SOAR frequentemente utilizados na indústria:  
  
- Jogos de Splunk Phantom
- IBM Resilient
- Sinal de Logsign
- Demisto
  
Você pode ver o que pode ser feito com uma solução SOAR na imagem abaixo.  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/SOAR/soar-capabilities.jpg)
  
Continuaremos a discutir os benefícios do SOAR e como podemos utilizar o SOAR efetivamente como analistas SOC na continuação deste artigo.  
  
**Salva o tempo** 
O SOAR economiza tempo através de fluxos de trabalho que automatizam processos. Alguns fluxos de trabalho usados com frequência são:  
  
- Controle de reputação do endereço IP
- Hash query 
- Digitalização de um arquivo adquirido em um ambiente de sandbox

**A centralização**  
Ele permite a operação de várias ferramentas de segurança em seu ambiente (sandbox, gerenciamento de logs, ferramentas de terceiros, etc.) de um ponto. Essas ferramentas são integradas à solução SOAR e podem ser usadas na mesma plataforma.  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/SOAR/soar-central.PNG)
  
**Livro de reprodução**  
Podemos facilmente investigar alertas SIEM usando playbooks criados para vários cenários dentro do SOAR. Podemos realizar uma análise usando esses manuais, pois podemos seguir os passos, mesmo que não saibamos ou lembremos todos os procedimentos.   

---
# Feed de Inteligência de Ameaças
Uma equipe SOC deve saber das ameaças mais recentes imediatamente e tomar as precauções apropriadas. Feeds de inteligência de ameaças são formados para atender a essa necessidade. Podemos utilizar essas fontes como analistas SOC quando estamos realizando uma investigação.  
  
Um Feed de Inteligência de Ameaças são dados (como **hashes** de malware, C2 (**Command&Control**) **domain/endereços IP**, etc.) fornecidos por uma empresa terceirizada.  


![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/SOAR/TI.PNG)


Os dados aqui são feitos de artefatos de atividades maliciosas anteriores. Pode ser o hash do malware ou do endereço IP de um centro de comando e controle. Como analista de SOC, podemos pesquisar feeds de inteligência de ameaças para determinar se um arquivo de hash que temos em mãos *já foi usado em um cenário malicioso no passado*.  

**Aqui estão algumas fontes gratuitas e populares que você pode usar:**  
  
- [VirusTotal](https://www.virustotal.com/)
- [Talos Intelligence](https://talosintelligence.com/)
  
  
Pontos que devemos prestar atenção para:  
#### **Dados que executamos feeds que não aparecem**  
Digamos que executamos um hash que pertencia a um .exe no VirusTotal e não conseguiu encontrar nada suspeito sobre isso no passado. Não devemos supor que o arquivo é limpo, isso seria um erro. Ainda assim, devemos ser diligentes em realizar as análises de arquivos necessárias (estática/dinâmica).  
#### **Não devemos esquecer que os endereços IP podem mudar de mãos.**  
Por exemplo, digamos que um invasor criou um servidor pela AWS (Amazon Web Services) e o usou como um centro de comando e controle. Em seguida, vários feeds de inteligência de ameaças registraram esse endereço IP em suas listas como um endereço malicioso.  
  
Depois de 2 meses tinha passado o atacante fechou o servidor e alguém mudou seu blog pessoal para este servidor. Isso não significa que as pessoas que visitaram o blog foram expostas a conteúdo malicioso. O fato de que este endereço IP foi usado por razões maliciosas no passado não significa que ele contenha conteúdo malicioso.


# Erros comuns para os analistas SOC
Como qualquer pessoa, os analistas da SOC também cometem erros. Nesta seção, mencionaremos erros que são frequentemente cometidos por analistas SOC e discutiremos como podemos evitar cometer esses erros nós mesmos.  
#### **Sobre o Conserto dos Resultados VirusTotal**  
Por vezes, podemos confiar no resultado exibido na tela verde do VirusTotal depois de analisar a URL de um arquivo e ver que o endereço é inofensivo. Mas há um novo software malicioso desenvolvido usando uma técnica de desvio AV (AntiVirus) que pode não ser detectada pelo VT (VirusTotal). Por esta razão, devemos aceitar o VirusTotal como uma ferramenta de apoio e conduzir nossas análises com isso em mente.  
  
Aqui está um post detalhado relacionado ao assunto para leitura posterior: https://medium.com/maverislabs/virustotal-is-não-an-incident-responder-80a6bb687eb9  
#### **Análise apressada de malware em uma sandbox**  
Uma análise de 3 a 4 minutos em um ambiente de sandbox nem sempre produz resultados precisos. Aqui estão as razões:  
  
- Malware que detecta um ambiente de sandbox e não se ativa  
- Malware que não é ativado até 10-15 minutos após a operação

Por esta razão, a duração da análise deve ser mantida o maior tempo possível e deve ocorrer num ambiente real, se possível.  
#### **Análise de Log Insuficiente**  
De tempos em tempos, vemos que as análises de log não são realizadas corretamente. Por exemplo, digamos que um malware detectou um dispositivo com o nome do host “LetsDefend” e esse malware está secretamente enviando dados para o endereço “letdefend.io”. Como analista de SOC, devemos utilizar soluções de “Gerenciamento de Log” para determinar se qualquer outro dispositivo está tentando se conectar a esse endereço.  
#### **Datas de vista do VírusTotal**  
Se a pesquisa que você realizou no VirusTotal já tiver sido consultada antes, um resultado do cache será exibido. Por exemplo: pesquisamos o endereço “letdefend.io” no VirusTotal e o resultado está abaixo.  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/SOC+Fundamentals/mistakes/vt-old.PNG)

Se eu fosse um invasor, eu poderia procurar um endereço URL limpo no VirusTotal e, em seguida, substituir o conteúdo por conteúdo malicioso. É por isso que não devemos apenas olhar para o cache de pesquisa, devemos começar uma nova pesquisa.