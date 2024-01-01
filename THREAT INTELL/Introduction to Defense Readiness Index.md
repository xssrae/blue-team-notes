---
tags:
  - THREAT-INTELLIGENCE
---
Imagine uma organização de segurança que esteja enfrentando uma ameaça cibernética. Surgem dois caminhos:

- A organização não está preparada e os invasores conseguem exfiltrar dados e bloquear sistemas. As equipes de segurança e de TI estão lutando contra incêndios durante dias para limpar tudo.

- Os invasores são rapidamente identificados e impedidos depois de se estabelecerem. As equipes de TI e de segurança redefinem prontamente as credenciais, protegem os sistemas e mantêm proativamente medidas de segurança contínuas.

Todos querem ser o último caso, mas o primeiro acontece diariamente nas organizações. Trata-se de um problema complexo que consiste em lacunas de conhecimento e controle, além de esforços concentrados nos lugares errados. O Defense Readiness Index (DRI) atende a essa necessidade fornecendo uma estrutura para priorizar habilidades e capacidades defensivas contra ameaças. 

O objetivo do modelo DRI é identificar rapidamente o nível que deve ser visado e, em seguida, avaliar sua prontidão para se defender contra ele. Em seguida, ele pode fornecer etapas acionáveis para solucionar quaisquer lacunas com novos recursos e/ou aprimoramento de habilidades. Esse modelo se aplica a organizações de todos os tamanhos, desde aquelas com um único profissional de segurança até aquelas com centenas de profissionais.

# Trabalho semelhante

A estrutura **[MITRE ATT&CK](https://attack.mitre.org/)** tornou-se o padrão de fato para descrever ataques e criar defesas; no entanto, ela não foi criada para priorizar nada. De fato, o próprio texto da MITRE afirma:

Existem muitas estruturas de controle, como o Center for Internet Security (CIS) e o National Institute of Standards and Technology (NIST), que são excelentes recursos para organizações maduras que buscam cobertura máxima; no entanto, elas são muito onerosas para organizações menores que provavelmente nunca verão agentes de ameaças de alto nível.

O modelo DRI busca oferecer um benchmark de várias camadas que se acumula até esses tipos de níveis de maturidade e, ao mesmo tempo, oferece pontos de partida úteis para todas as organizações.

## Nível de sofisticação da ameaça

- **Desenvolvimento**: Software ou conteúdo que deve ser desenvolvido para realizar as ações no alvo.
- **Direcionamento**: Trabalho que identifica oportunidades exploráveis. Elas se sobrepõem fortemente às variedades de dados comprometidas.
- **Distribuição**: Serviços usados para distribuir o conteúdo do agente, incluindo e-mail, servidores comprometidos e sites.
- **Serviços de não distribuição**: Serviços fornecidos e usados por agentes de ameaças que não sejam aqueles usados para a distribuição de conteúdo de agentes.
- **Cash-out**: Métodos para converter algo, por exemplo, o atributo comprometido, em moeda.

##  Recursos da ATT&CK

Para determinar quantitativamente quais técnicas são necessárias para cada DRI, primeiro você precisa identificar quais técnicas da ATT&CK se aplicam a cada nível de ameaça. 

- **Público**: Quantas horas seriam necessárias para atingir um recurso público em um único alvo? Medida de quão prontamente disponível/habilidade é a capacidade.
-  **Alterado**: Quantas horas são necessárias para alterar um recurso público para um único alvo? Medição de quanto tempo/habilidade adicional é necessário para alterar uma técnica pública, mas que ainda seja fundamentalmente a mesma.
-  **Sob medida**: Quantas horas são necessárias para desenvolver um recurso sob medida para um único alvo? Medida de quanto tempo seria necessário para criar uma subtécnica ou um método completamente novo.

- <**1 hora**: *Fire and forget scripting*, ataques automatizados usando ferramentas públicas.
- **1 hora**: *Kits de malware automatizados* e *kits de exploração*. Requer algumas habilidades de segurança de pré-requisito para usar e atingir.
- **10 horas**: As *técnicas interativas* (teclado prático) geralmente se enquadram aqui ao usar técnicas de código aberto, por exemplo, Metasploit.
- **100 horas**: Ferramentas *e técnicas personalizadas com escopo limitado*. Elas são usadas com frequência porque as públicas são insuficientes ou provavelmente serão capturadas com uma detecção simples - a maioria das empresas de pentest se enquadra aqui.
- **1.000 horas**: Recursos novos e personalizados que exigem recursos e conhecimento para fazer o que for necessário para atingir um objetivo.

## Esforço por alvo

O DRI normaliza o Nível de Sofisticação da Ameaça para organizações, calculando o esforço médio por alvo. Isso considera que a eficácia de uma técnica diminui à medida que sua prevalência aumenta, impactando a detectabilidade. Por exemplo, um agente de ameaças estabelecido, como um APT de estado-nação, pode assumir o controle de uma rede de uma pequena empresa operando na DRI2, mas é improvável a menos que haja algo de grande valor ou um passo para um objetivo maior. A avaliação interna de riscos da APT pode modificar seu DRI alvo com base nessas considerações, evitando riscos desnecessários.

|**Threat Sophistication Level**|**Targets**|**Hours of Effort per Target**|**TTPs Used**|
|---|---|---|---|
|Opportunistic Actors  <br>Example: Script Kiddie|Anyone susceptible to available attacks|<1|Publicly-available, requiring low skill to use and target|
|Prudent Actors  <br>Example: low-level e-crime|Industries or countries of interest|1|Paid or publicly-available, requiring medium skills, e.g., exploit toolkits|
|Emerging Actors  <br>Example: most e-crime|Industries or countries of interest|10|Some altered public tools and paid tools. May have interactive capabilities, e.g., Metasploit|
|Established Actors  <br>Example: most nation-states|Specific organizations to include collection and attacks|100|Mainly internally-developed tools and capabilities. Limited numbers of targets|
|Strategic Actors  <br>Example: high level nation-states|Specific organizations to include collection and attacks|1000+|Whatever gives the best OPSEC for the situation. Very limited use of the capabilities|

# DRI
 Depois de escolher uma DRI de destino com base nas ameaças, o modelo DRI usa as relações de detecção do ecossistema do MITRE para mapeá-las para os recursos apropriados do **[D3FEND](https://d3fend.mitre.org/)**  
 
![Example of D3FEND inferred relationships](https://cdn.rangeforce.com/modules/nn9KauyhRzxisYBUR/TdYZvCDHmMy4MfghP.png "Example of D3FEND inferred relationships")

1. **Capacidade Gerenciada:** Envolve sistemas ou funções gerenciados por terceiros, como fornecedores de segurança. O profissional de segurança precisa conhecer esses recursos para selecionar e entender suas funcionalidades, mas não necessariamente como operam internamente. Essa abordagem é eficaz contra ameaças públicas com assinaturas distintas.

2. **Capacidade Sob Medida:** Refere-se a sistemas ou funções adaptados a ambientes específicos. O profissional de segurança deve compreender e ajustar esses recursos para atender a um ambiente particular, como gerenciar listas de bloqueios ou ajustar alertas para comportamentos específicos.

3. **Capacidade Otimizada:** Envolve processos ou funções de segurança que exigem que o profissional aplique técnicas defensivas usando diversas ferramentas para ser eficaz. Isso inclui estabelecer uma linha de base, alertar desvios e criar políticas específicas para lidar com comportamentos maliciosos. Embora seja o esforço mais significativo, é crucial para enfrentar ameaças altamente evasivas.

