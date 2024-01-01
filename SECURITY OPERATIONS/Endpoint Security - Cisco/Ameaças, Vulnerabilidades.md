---
tags:
  - SECURITY-OPERATIONS
---
# Ameaças comuns
### Ameaças Internas vs Externas

As ameaças podem se originar **dentro e fora de uma empresa**, com os invasores buscando acesso a informações confidenciais valiosas, como registros pessoais, propriedade intelectual e dados financeiros.

- **As Ameaças Internas** são geralmente realizadas por funcionários atuais ou antigos e outros parceiros de contrato que acidentalmente ou intencionalmente manipulam dados confidenciais ou ameaçam as operações de servidores ou dispositivos de infraestrutura de rede ao conectar a mídia infectada ou acessar e-mails ou sites mal-intencionados.

- **Ameaça externa** geralmente vem de invasores amadores ou qualificados que podem explorar vulnerabilidades em dispositivos de rede ou podem usar técnicas de engenharia social, como truques, para obter acesso aos recursos internos de uma organização.

![Ameaças externas e internas que se estendem dos criminosos digitais. As ameaças internas consistem em funcionários e ex-funcionários, funcionários contratados e parceiros confiáveis. As ameaças externas consistem em hackers organizados, como hackers, terroristas e hackers e amadores patrocinados pelo estado, de chapéu preto, cinza e branco.](https://skillsforall.com/content/noes/1.0/m1/course/pt-BR/assets/60ad062976d9601a3337b20d.png)

### Inteligência de Ameaças e Fontes de Pesquisa

O United States Computer Emergency Readiness Team (US-CERT) e o Departamento de Segurança Interna dos EUA patrocinam um **dicionário de vulnerabilidades e exposições comuns (CVE)**.

Cada entrada do CVE contém um número de identificador padrão, uma breve descrição da vulnerabilidade de segurança e todas as referências importantes aos relatórios de vulnerabilidade relacionados. A lista CVE é mantida por uma organização sem fins lucrativos, a MITRE Corporation, em seu site público.
- **Uma teia escura**: Isso se refere ao **conteúdo da Web criptografado** que *não é indexado pelos mecanismos de pesquisa convencionais e requer software*, autorização ou configurações específicas para acesso. Pesquisadores especialistas monitoram a Web obscura em busca de uma nova inteligência de ameaças.

- **Indicador de comprometimento (IOC)**: **IOCs, como assinaturas de malware ou nomes de domínio**, fornecem *evidências de violações* de segurança e detalhes sobre elas.

- **Compartilhamento Automatizado de Indicadores (AIS)**: O Automated Indicator Sharing (AIS), um recurso da Cybersecurity and Infrastructure Security Agency (CISA), permite a troca em tempo real de indicadores de ameaças à segurança cibernética usando uma linguagem padronizada e estruturada chamada Structured Threat Information Expression (STIX) e Trusted Automated Exchange of Intelligence Information ( TÁXI).

# Disfarce

## Engenharia Social

A engenharia social é uma estratégia não técnica que tenta manipular indivíduos para realizar determinadas ações ou divulgar informações confidenciais.

Em vez de vulnerabilidades de software ou hardware, a engenharia social explora a *natureza humana*, aproveitando a disposição das pessoas em ajudar ou se aproveitando de suas fraquezas, como ganância ou vaidade.

![[Pasted image 20231228140400.png]]

## Falsificação de Identidade e Fraudes

Os criminosos digitais têm muitas outras técnicas de dissimulação para ajudá-los a obter sucesso.

## Piggybacking e Tailgating

**Piggybacking** ou **Tailgating** ocorre quando um criminoso segue uma pessoa autorizada para obter entrada física em um local seguro ou em uma área restrita. Os criminosos podem conseguir isso:

- Dar a impressão de ser escoltado para a instalação por uma pessoa autorizada.
- Juntar-se e fingir ser parte de uma grande multidão que entra na instalação.
- Visar uma pessoa autorizada que não tem cuidado com as regras da instalação.

Uma maneira de evitar isso é usar dois conjuntos de portas. Isso às vezes é chamado de mantrap e significa que os indivíduos entram por uma porta externa, que deve fechar antes que eles possam ter acesso através de uma porta interna.

## Defesa Contra Engano

![Quatro cadeados abertos aparecem e linhas pontilhadas se formam ao redor deles em hexágonos, e os cadeados são fechados](https://skillsforall.com/content/noes/1.0/m1/course/pt-BR/assets/60a4caf80192ea628a19bfb1.png)

As organizações precisam promover a conscientização sobre as táticas de engenharia social e educar adequadamente os funcionários sobre as medidas de prevenção. Aqui estão algumas dicas importantes.

- Nunca divulgue informações confidenciais ou credenciais por e-mail, bate-papo, mensagens de texto, pessoalmente ou por telefone para pessoas desconhecidas.
- Resista ao desejo de clicar em e-mails atraentes e links da web.
- Desconfie de downloads não iniciados ou automáticos.
- Estabelecer e educar os funcionários sobre as principais políticas de segurança.
- Incentive os funcionários a assumirem responsabilidade pelos problemas de segurança.
- Não se submeter à pressão de pessoas desconhecidas.

# Ataques cibernéticos

## Bombas Lógicas

Uma bomba lógica é um programa malicioso que *espera por um gatilho*, como uma data especificada ou entrada de banco de dados, para detonar o código malicioso. Até que este evento de disparo aconteça, a bomba lógica permanecerá inativa.

## Ransomware

Malware projetado para manter um sistema de computador, ou os dados incluídos nele, presos até que o pagamento seja feito. Geralmente funciona criptografando os dados para que você não possa acessá-los.

## Ataques de Camada 2

A camada 2 refere-se à camada de link de dados no modelo de comunicação de dados Open Systems Interconnection (OSI).
#### Spoofing

Spoofing é um ataque de representação e tira proveito de uma relação de confiança entre os dois sistemas.
- A **falsificação de endereço MAC** ocorre quando um invasor *disfarça seu dispositivo como um dispositivo válido na rede* e, portanto, pode ignorar o processo de autenticação. 
- O **ARP spoofing** *envia mensagens ARP falsificadas através de uma LAN*. Isso vincula o endereço MAC de um invasor ao endereço IP de um dispositivo autorizado na rede.
- O **spoofing de IP** *envia pacotes IP com um endereço de origem falsificado* para se disfarçar.
#### Inundação de MAC

Os dispositivos em uma rede são conectados por um switch de rede usando o switching de pacote para receber e encaminhar dados para o dispositivo de destino. A inundação de MAC compromete os dados transmitidos para um dispositivo. Um invasor inunda a rede com endereços MAC falsos, comprometendo a segurança do switch de rede.

# Ataques a dispositivos móveis e sem fio

## Grayware e SMiShing

**Grayware** é qualquer aplicativo indesejado que se comporta de maneira irritante ou indesejável. E, embora o grayware não tenha nenhum malware reconhecível, ele ainda pode representar um risco para o usuário, por exemplo, acompanhando a sua localização ou disponibilizando publicidade indesejável.