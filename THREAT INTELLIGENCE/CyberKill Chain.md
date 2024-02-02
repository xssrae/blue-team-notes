# Introdução ao Cyber Kill Chain

## **O que é Cyber Kill Chain e Lockheed Martin?**

A **Lockheed Martin** foi fundada em 1995 e é uma empresa de segurança e aeroespacial que realiza pesquisas, desenvolve, projeta e produz sistemas tecnológicos avançados.

**Cyber Kill Chain** é uma estrutura criada pela Lockheed Martin em 2011 e usada para modelar os ataques de atacantes. Dentro dessa estrutura, os comportamentos dos invasores e todo o processo de ataque cibernético consistem em 7 etapas que se seguem.

**Página oficial da [Cyber Kill Chain**](https://www.lockheedmartin.com/pt-us/cyber/cyber-kill-chain.html) 
## **Significado da Cyber Kill Chain**
Cyber Kill Chain é ==importante para o analista SOC ter uma melhor compreensão dos **estágios de um ataque cibernético** e para determinar com qual ação (s) o ataque cibernético começa e qual(is) ação(s) segue==. A Cyber Kill Chain permite que a organização determine onde e *quão severas* são as falhas de segurança. A Blueteams pode identificar áreas em que faltam medidas de segurança com base nessas falhas e tomar as medidas apropriadas.

---
# Passos da Cyber Kill Chain

Existem várias ==**ações** que um invasor pode tomar *antes*, *durante* e *depois* de um ataque cibernético bem-sucedido==. Essas ações são sequenciais e, se o atacante falhar em um estágio, não é possível executar a próxima etapa do ataque cibernético. O modelo Cyber Kill Chain divide esses estágios de atacantes em **7 passos**. Os passos dos ataques cibernéticos são representados no visual abaixo:

  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Cyber+Kill+Chain/2.Cyber+Kill+Chain+Steps/steps1.png)

  
1. **Reconstituição**
2. **Armação**
3. **A entrega**
4. **A exploração**
5. **A instalação**
6. **Comando e Controle (C2)**
7. **Acções sobre os objectivos**

---
## Reconstituição
==O atacante tenta **obter informações** sobre o sistema de destino nesta etapa==. Quanto mais *conhecimento* um atacante tem sobre o sistema de destino, mais a **superfície de ataque** lhe parece. Os vetores de ataque para o alvo são divulgados dessa maneira. As técnicas empregadas nesta fase podem ser divididas em duas subcategorias:

1. **Reconhecimento passivo**
2. **Reconhecimento ativo**

O termo **"Reconhecimento Passivo"** refere-se à coleta de informações de fontes sobre o sistema alvo sem se envolver fisicamente com o sistema de destino.

**"Reconhecimento Ativo"** refere-se ao método de adquirir informações sobre um sistema alvo, envolvendo-o diretamente. 

### **O adversário**
O invasor pode ==coletar informações de várias fontes usando uma variedade de abordagens== durante o processo "Reconhecimento". Nesta fase, o atacante pode realizar as seguintes operações:
- Obtenção de informações de versão de servidores e software pertencentes ao alvo
- Obter informações de fontes abertas de informações sobre o alvo foi divulgado anteriormente
- Obtenção de endereços de e-mail dos funcionários da organização
- Obter informações internas ou pessoais sobre os funcionários da organização usando plataformas de redes sociais
- Detecção de dispositivos que estão conectados à Internet
- Detecção de vulnerabilidades de segurança em servidores abertos ao acesso na Internet
- Identificar o bloqueio de endereço IP pertencente à organização
- Identificação de fornecedores com os quais a organização coopera

### **Defensor**
Blueteams podem tomar ==medidas em resposta às tentativas dos atacantes nesta fase==. Isso reduz a quantidade de informações que um invasor pode obter. Alguns métodos que os analistas SOC e blueteams podem implementar estão listados abaixo:
- Detecção de áreas de divulgação de informações com pentest externo
- Obtenção de informações sobre vazamentos sobre a organização de fontes de Inteligência de Ameaças
- Não manter os documentos fornecendo informações organizacionais disponíveis na internet
- Monitorar o tráfego instalando soluções de segurança, como firewalls em áreas da empresa acessíveis pela internet
- Atualização instantânea para evitar que novas vulnerabilidades de segurança sejam exploradas
---
# Armação
A “armação” é o segundo passo na Cyber Kill Chain. Nesta fase, ==o atacante usa as **informações obtidas** no estágio anterior para acessar as **ferramentas necessárias** para o ataque ou desenvolve a ferramenta/roteiro diretamente==. Nesta fase, a preparação para um ataque cibernético pode variar dependendo do tipo de ataque. Por exemplo, se um ataque cibernético do tipo phishing for realizado, um exploit pode ser construído em resposta a uma vulnerabilidade de segurança reconhecida ou conteúdo de e-mail malicioso pode ser gerado. Se as ferramentas para o ataque cibernético estiverem prontas, o invasor concluirá essa fase rapidamente e passará para a próxima fase do ataque cibernético. ==Neste ponto, o ataque ainda não começou, e a vítima geralmente desconhece o agressor==.

## **O adversário**
O invasor pode construir muitas técnicas alternativas de ataque ou preparar os componentes essenciais para um ataque cibernético durante o processo de "armação". A seguir estão alguns dos processos que o invasor pode empregar nesta fase:

- Criação de malware
- Desenvolvimento de explorações
- Criação de conteúdo malicioso para uso em uma tentativa de phishing (como um modelo de email e um documento malicioso).
- Identificar o melhor instrumento para o ciberataque

## **Defensor**
Não é possível que analistas de SOC e Blueteams evitem diretamente os preparativos de ataque dos atacantes nesta fase. No entanto, algumas medidas podem ser tomadas, embora limitadas. Algumas dessas medidas são as seguintes:

- Verificar os sistemas regularmente para ver se existem vulnerabilidades de segurança identificadas.
- Instalação de atualizações de segurança para os sistemas das instituições o mais rápido possível
- Analisar o impacto de ferramentas de ataque cibernético conhecidas ou recém-produzidas em sistemas, rastreando as ferramentas de ataque conhecidas ou recém-desenvolvidas e, portanto, sendo capaz de detectar quando a ferramenta é utilizada

---
#  A entrega

O terceiro passo da Cyber Kill Chain é o estágio "Delivery". Nesta fase, ==o atacante **executa o ataque cibernético** que ele preparou nas fases anteriores==. Este é o estágio em que a *primeira interação com a vítima* acontece. Por exemplo, o malware é carregado no ambiente adequado nesta etapa, e a vítima baixa o malware do ambiente carregado para seus sistemas. Os métodos usados para fornecer conteúdo malicioso podem diferir dependendo do tipo de ataque. Por exemplo, o uso de e-mail para um ataque de phishing pode ser preferido ou o conteúdo malicioso no e-mail pode ser carregado em um endereço da Web.

## **O adversário**
No estágio "Entrega", o atacante pode entregar uma variedade de armas cibernéticas à vítima através de uma variedade de métodos. Nesta fase, o atacante pode realizar as seguintes operações:
- Entregar um URL malicioso por e-mail
- Fornecer malware como um anexo de arquivo via e-mail
- Entregar malware através do site
- Entregar a URL maliciosa via mídia social
- Entrega de malware através de mídias sociais
- Carregar o malware diretamente para o servidor de destino (se o acesso direto ao servidor for possível)
- Instalação física ou habilitação da instalação de malware diretamente para o sistema de destino através de um dispositivo USB

## **Defensor**
Blueteams e usuários individuais podem tomar muitas medidas de precaução nesta fase. Embora não possam impedir totalmente o ataque cibernético de ocorrer, essas precauções podem minimizar drasticamente o risco de um ataque cibernético bem-sucedido. Algumas dessas medidas estão listadas abaixo:
- Adotar uma atitude cética em relação às URLs no conteúdo de e-mail e visualizá-las em um ambiente de sandbox
- Digitalização dos anexos do e-mail usando o software antivírus
- Usando produtos de solução de segurança de e-mail nas organizações
- Garantir que os usuários/funcionários institucionais recebam treinamento sobre segurança da informação
- Monitoramento constante do acesso ao servidor e gravação de logs
- Uso eficaz e gerenciamento de soluções de segurança como Firewall
- Realização de análise detalhada de atividades suspeitas quando necessário
- Detectar anomalias e determinar o motivo inicial
---
# A exploração

Durante a etapa de exploração, o ==processo de **execução do malware transmitido** para o dispositivo da vítima é realizado==. A operação inicial no sistema é realizada pelo atacante nesta fase. A operação de exploração realizada aqui é um precursor das atividades de ataque que serão realizadas nas fases subsequentes. As *próximas fases do ataque cibernético não podem ser realizadas se o exploit falhar aqui por um motivo*, ou se o malware entregue não puder ser executado.

## **O adversário**
O invasor tem algum conhecimento básico sobre o programa ou sistema destinado a ser explorado no alvo e preparou as ferramentas de ataque apropriadas de antemão no estágio "Exploração". Esta etapa pode ser falhada se a exploração ou ferramenta não for adequada para ser utilizada no sistema da vítima. Neste nível, o atacante pode executar as seguintes operações:
- Executar o exploit que explora a vulnerabilidade do hardware
- Executar o exploit que explora a vulnerabilidade do software ou sistema operacional
- Executando malware

## **Defensor**
Defender a exploração representa uma tarefa significativamente mais complexa e trabalhosa para as Blueteams em comparação com outras etapas. Para elucidar, o uso de exploits de dia zero pode complicar os procedimentos de detecção e prevenção durante esta fase. Os seguintes pontos podem ser considerados para detectar e prevenir atividades maliciosas:
- Treinar os funcionários da organização sobre quando é/não é necessário abrir um ficheiro carregado nos sistemas e quais os problemas que devem ser considerados
- Monitorar constantemente as operações de segurança do sistema nos ativos pertencentes à organização e detectar anomalias
- Rastrear as vulnerabilidades de segurança publicadas para os ativos pertencentes à organização, escrever a regra de monitoramento apropriada e detectá-las quando elas são exploradas
- Após as atualizações de segurança dos ativos pertencentes à organização e instalá-los imediatamente
- Atividades de monitoramento em endpoints utilizando produtos EDR
- Fornecer treinamento de codificação seguro para desenvolvedores de software para evitar vulnerabilidades de segurança em aplicativos desenvolvidos localmente
- Realizar pentests em ativos da organização regularmente
- Digitalização de vulnerabilidades automatizadas e monitoramento de relatórios
- Organizar as autorizações sobre os bens pertencentes à instituição e dar a cada conta a autoridade necessária

---
# A instalação

A quinta fase da Cyber Kill Chain é a fase de "Instalação". Nesta fase, o invasor tenta manter a persistência no sistema de destino que foi explorado. O invasor ==tenta obter um caminho de acesso que pode ser acessado a qualquer momento, instalando um backdoor no sistema==. Este é o estágio em que os preparativos de ataque são realizados para alcançar os objetivos finais, uma vez que o ataque cibernético tenha começado.

## **O adversário**
Na etapa "Instalação", um invasor pode executar uma ampla gama de operações. O atacante pode realizar com sucesso várias atividades tecnológicas, desde que seja restrito à sua autoridade no sistema que explora. Ao executar essas operações, o invasor tenta deixar o ==menor número possível de vestígios no sistema e garantir que os produtos de segurança não interfiram nas operações==. Desta forma, o atacante pode permanecer sem ser detectado no sistema por um período mais longo, ganhando o tempo necessário para realizar o ataque. Nesta fase, o atacante pode executar as seguintes ações:

- Instale malware no dispositivo da vítima.
- Colocar um backdoor no sistema da vítima
- Instalar web shell no servidor web (se é um servidor web).
- Adicionar um serviço, regra de firewall ou tarefa agendada para garantir a persistência do dispositivo da vítima

## **Defensor**
As operações que a Blueteams aplica contra os atacantes nesta fase consistem nas operações de caça a ameaças. ==O fato de que um invasor que chegou a esse estágio está realizando atividades maliciosas nos sistemas indica que o invasor não pode ser detectado==. Portanto, se o invasor está presente ou não, a equipe SOC deve gerenciar e executar operações de segurança sob a suposição de que há sempre um invasor presente no sistema. As operações de segurança que podem ser realizadas neste nível dependerão da estrutura atual. A seguir estão algumas atividades que podem ser tomadas em geral:

- Para realizar operações de monitoramento de segurança de rede em todos os ativos da organização
- Usando soluções de segurança EDR para estar ciente das mudanças de configuração aplicadas em cada ponto
- Restringir o acesso a arquivos críticos em sistemas e monitorar o acesso
- Restringir o acesso a caminhos críticos em sistemas e monitorar o acesso
- Permitir o uso de privilégios de administrador apenas para situações obrigatórias, fazendo arranjos de autorização para usuários nos sistemas
- Detectar atividades de processos maliciosos monitorando os processos em execução nos sistemas
- Permitindo apenas arquivos executáveis com uma assinatura válida a ser executado no sistema
- Detectar anomalias em todas as atividades do sistema monitorado e encontrar a causa raiz

---
# Comando e Controle (C2)

Neste ponto, o atacante completou várias tarefas cruciais do ataque e preparou o servidor de Comando e Controle para entregar comandos ao sistema. ==O atacante pode enviar comandos remotos para o sistema e executá-los nesta etapa.==
## **O adversário**
Nesse estágio, o que o atacante faz é estabelecer contato entre C2 e o sistema de destino. Esta fase não inclui a execução das ações visadas pelo atacante. Uma vez concluída a comunicação C2, o invasor procederá a realizar atividades maliciosas.

Resumidamente, o que o atacante faz nesta fase é o seguinte:
- Configurar o C2 Server para se comunicar com a vítima
- Implementar as ações necessárias no dispositivo da vítima para tornar possível o seu contato com o C2.
## **Defensor**
Embora não haja uma ação específica para as equipes azuis nesta fase, devem ser consideradas as técnicas e práticas gerais de monitoramento e detecção de segurança no contexto da comunicação C2. A Blueteams deve tomar as medidas adequadas para reconhecer e prevenir o fluxo de tráfego de rede C2. A seguir estão alguns passos a serem tomados:

- Para determinar se as ferramentas C2 conhecidas estão disponíveis em sistemas
- Bloqueio de endereços IP de servidor C2 de fontes de inteligência de ameaças cibernéticas por meio de produtos de segurança, como o Firewall
- Para detectar o tráfego de rede que pode ser comunicação C2 com o monitoramento de segurança de rede no sistema

---
# Ações sobre os objetivos
Neste ponto, o atacante toma as ações planejadas nos primeiros estágios do ataque cibernético. O atacante passa por inúmeras fases, cada uma das quais precisa ser realizada com sucesso antes de chegar a este passo. Portanto, o invasor pode realizar as operações desejadas no sistema.

## **O adversário**
Nesta etapa, as ações dos atacantes são determinadas por seu propósito e motivação. Se o objetivo principal do invasor é causar danos no sistema, eles podem excluir informações críticas, por exemplo. A seguir estão alguns dos passos que o atacante pode realizar nesta fase:
- Para criptografar arquivos no sistema com a ajuda de ransomware
- Exfiltrar informações/documentos críticos dentro do sistema
- Danificando o sistema excluindo informações críticas no sistema
- Para se tornar capaz de aplicar operações mais autorizadas com operações de escalada de privilégios e expandir o escopo do ataque cibernético, fornecendo acesso a outras máquinas na rede
- Coletar credenciais de usuário para obter acesso a outro dispositivo na rede
- Recolha de informação dentro do sistema
- Alterar ou manipular as informações no sistema
## **Defensor**
Neste estágio, as equipes azuis podem precisar tomar ações diferentes com base em cada processo específico para detectar e parar a atividade do invasor. Após a fase de detecção, a ação detectada deve ser seguida pela ação apropriada. Uma das medidas mais fundamentais que as equipes de SOC podem tomar é ==impedir que os invasores extraem dados da organização para fora==. Porque o vazamento de dados é um dos resultados de ataques cibernéticos mais comuns hoje. A seguir, algumas medidas a serem tomadas nesta fase:
- Detectando anomalias no tráfego de rede
- Restringir o acesso à rede externa e monitorá-lo continuamente
- Restringir o acesso a arquivos/pastas que contenham informações críticas e controle regular o acesso
- Restringir a autorização de acesso a bases de dados que contenham informações críticas e monitoramento contínuo do acesso
- Usando produtos DLP para evitar vazamento de dados
- Detectar acesso não autorizado pelos usuários