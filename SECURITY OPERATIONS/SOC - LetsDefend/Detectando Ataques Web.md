---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
# Por que detectar ataques na Web é importante
Quando você olha para a vida diária do Joe Médio, você verá que ele usa muitos aplicativos da web ao longo do dia. Há quem visite o Spotify para ouvir música, quem visita o YouTube para assistir a vídeos ou quem usa as redes sociais.

Não é nenhuma surpresa que os invasores escolham aplicativos da Web como um gateway para seus ataques, porque todas as instituições têm aplicativos da Web que contêm principalmente dados críticos e porque os aplicativos modernos são altamente complicados e têm inúmeros vetores de ataque. Um estudo realizado pela Acunetix reembolsa essa ideia.

> “Pesquisa recente mostra que 75% dos ataques cibernéticos são feitos no nível da aplicação web.”

Se examinarmos a anatomia de um ataque, vemos que o melhor cenário é evitar o ataque em sua primeira fase. Por esta razão, existem várias precauções de segurança que visam prevenir e detectar aplicações web (WAF, IPS, regras SIEM...).

É crucial que um analista SOC detecte esses ataques baseados em aplicativos da Web que são a preferência de invasores e toma precauções contra eles.

**Referência**  
  
[1] [https://www.acunetix.com/websitesecurity/web-application-attack/](https://www.acunetix.com/websitesecurity/web-application-attack/)

---
# OWASP (IPO)
O Open Web Application Security Project (OWASP) é uma fundação sem fins lucrativos que trabalha para melhorar a segurança do software.[1]

É sem dúvida que o OWASP é um dos melhores recursos para obter informações sobre segurança de aplicativos web.
## **OWASP Top 10**

OWASP publica uma lista de 10 vulnerabilidades de aplicativos da Web que possuem os riscos de segurança mais críticos a cada dois anos. A partir da redação deste artigo, a última publicação foi em 2021.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/Owasp-Top-10.png)

A lista OWASP publicada em 2021 contém estes riscos críticos de segurança:

1. Controle de acesso quebrado
2. Falhas criptográficas
3. Injeção
4. Design inseguro
5. Configuração incorreta de segurança
6. Componentes vulneráveis e desatualizados
7. Falhas de identificação e autenticação
8. Falhas de integridade de software e dados
9. Registro de segurança e falhas de monitoramento
10. Fibra de solicitação do lado do servidor (SSRF)

Você pode ler a publicação OWASP que contém os riscos de segurança mais críticos [aqui](https://owasp.org/).

---
# Como funcionam as aplicações web
Para detectar uma anomalia, devemos primeiro entender como a tecnologia funciona. Os aplicativos utilizam determinados protocolos para se comunicar com precisão uns com os outros. Os aplicativos da Web se comunicam através do Hyper-Text Transfer Protocol (HTTP). Veja como funciona o protocolo HTTP.

Para começar, é importante saber que o protocolo HTTP está na 7a camada do modelo OSI. Isso significa que protocolos como Ethernet, IP, TCP e SSL são usados antes do protocolo HTTP.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/HTTP-Protocol-TCP-IP-Model-OSI-Model.png)

A comunicação HTTP ocorre entre o servidor e o cliente. Primeiro, o cliente solicita um recurso específico do servidor. O servidor recebe a solicitação HTTP e envia de volta uma (Tr.A.) para o cliente depois de passá-lo por certos controles e processos. O dispositivo do cliente recebe a resposta e exibe o recurso solicitado em um formato apropriado.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/HTTP-Request-and-HTTP-Response.png)

Vamos examinar solicitações HTTP e respostas HTTP com mais detalhes.

## Requisição HTTP
Uma solicitação HTTP é usada para recuperar um determinado recurso de um servidor web. Este recurso pode ser um arquivo HTML, vídeo ou dados json etc. O trabalho do servidor web é processar a resposta recebida e apresentá-la ao usuário.

Existe um formato HTTP padrão, e todas as solicitações devem estar em conformidade com esse formato para que os servidores da Web possam entender a solicitação. Se a solicitação for enviada em um formato diferente, o servidor da Web não a entenderá e enviará um erro ao usuário ou ao servidor da Web poderá não conseguir fornecer serviço (que é outro tipo de ataque).

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/HTTP-Request.png)

Um pedido HTTP consiste em uma linha de solicitação, cabeçalhos de solicitação e um corpo de mensagem de solicitação. Uma linha de solicitação consiste no método HTTP e no recurso solicitado no servidor web. O cabeçalho da solicitação contém certos cabeçalhos que o servidor processará. O corpo da mensagem de solicitação contém dados que se destinam a ser enviados para o servidor.

Na imagem acima você vê um exemplo de uma solicitação HTTP. Vamos examinar esta solicitação HTTP linha por linha.

1. O método GET afirma que o recurso “/” é solicitado ao servidor. Como não há nome, em vez disso, um símbolo como “/” significa que a página principal do servidor web é solicitada.
2. Hoje em dia, existem aplicativos da Web que pertencem a mais de um domínio encontrado em um único servidor da Web, de modo que os navegadores usam o cabeçalho “Host” para descrever a que domínio o recurso solicitado pertence.
3. Quando um aplicativo da Web quer armazenar informações no dispositivo do cliente, ele o armazena em um cabeçalho “Cookie”. Os cookies são geralmente utilizados para armazenar informações de sessão. Portanto, você não precisa digitar seu nome de usuário e senha quando visitar um aplicativo da Web que requer login.
4. Há informações sobre o navegador e o sistema operacional do cliente sob o cabeçalho “User-Agent”. Os servidores da Web usam essas informações para enviar respostas HTTP específicas ao cliente. Você pode encontrar alguns scanners de vulnerabilidade automatizados olhando sob este cabeçalho.
5. O tipo de dados solicitados é encontrado sob o cabeçalho “Aceitar”.
6. O tipo de codificação que o cliente entende é encontrado em cabeçalho “Aceitar codificação”. Normalmente, você pode encontrar nomes de algoritmos de compressão sob este cabeçalho.
7. Sob o cabeçalho “Aceitar-Idioma”, você pode encontrar as informações de idioma dos clientes. O servidor web usa essas informações para exibir o conteúdo preparado no idioma do cliente.
8. O cabeçalho “Connection” mostra como a conexão HTTP será feita. Se houver algum dado como “próximo” encontrado aqui, isso significa que a conexão TCP será fechada após a resposta HTTP ser recebida. Se você ver “Keep-alive”, isso significa que a conexão será continuada.
9. Uma linha vazia é colocada entre o cabeçalho de solicitação HTTP e o órgão de mensagens de solicitação HTTP para fazer uma partição.
10. Outros dados destinados a serem enviados para a aplicação web são encontrados no órgão de mensagens de solicitação. Se o método HTTP POST for usado, os parâmetros POST podem ser encontrados aqui.

## Respostas HTTP
Uma vez que o servidor web recebe uma solicitação HTTP, ele executa os controles e processos necessários e, em seguida, envia o recurso solicitado para o cliente. Não há um processo uniforme aqui porque existem inúmeras tecnologias e projetos envolvidos. O servidor pode extrair dados do banco de dados de acordo com o que é o recurso solicitado ou pode processar de acordo com os dados recebidos. Mas a mensagem de resposta HTTP deve chegar ao cliente após todo o processamento.

Uma mensagem de resposta HTTP contém uma linha de status, cabeçalhos de resposta e um órgão de resposta. A linha de status contém o código de status (como 200: OK) e informações de protocolo HTTP. Existem cabeçalhos usados para vários fins dentro do cabeçalho de resposta. Os dados relacionados ao recurso solicitado são encontrados no órgão de resposta.

Se uma página da Web foi solicitada, geralmente haverá códigos HTML no órgão de resposta. Quando o cliente recebe o código HTML, o navegador da Web processa o código HTML e exibe a página da Web.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/HTTP-Response.png)

Você pode ver uma solicitação de resposta HTTP na imagem acima. Vamos examinar uma solicitação de resposta HTTP com base nessa imagem.
### Linha de status
Há informações sobre a versão HTTP e o código de status de resposta HTTP na Linha de Status. O código de status de resposta HTTP é usado para descrever o status da requisição. Existem muitos códigos de status de resposta HTTP, mas eles podem ser resumidos assim:

**100-199** : Respostas informativas

$ **200-299** : Respostas bem sucedidas

$ **300-399** : Mensagens de Redirecionamento

$ **400-499** : Respostas de erro do cliente

**500-599** : Respostas de erro de servidor
### Cabeçalhos de resposta
Aqui estão alguns cabeçalhos de resposta HTTP que você pode encontrar com frequência:

**Data** : A hora exata em que o servidor enviou a resposta HTTP ao cliente.

**Conexão:** Ele afirma como a conexão será tratada, assim como no cabeçalho de solicitação HTTP.

**Servidor:** Informações sobre o sistema operacional do servidor e a versão do servidor web.

**Last-Modified** : Informações sobre quando o recurso solicitado foi alterado. Este cabeçalho é usado para o mecanismo de cache.

**Content-Type** : O tipo de dados que é enviado.

**Content-Length** : O tamanho dos dados enviados.

### Corpo de resposta
O órgão de resposta HTTP contém o recurso que foi enviado pelo servidor e solicitado pelo cliente.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/HTML-example.png)

---
# Detecção de ataques de SQL Injection
## O que é SQL Injection (SQLi)?
Injeções SQL são métodos de ataque críticos em que um aplicativo da Web inclui diretamente dados não padronizados fornecidos pelo usuário em consultas SQL.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/sql-injection.png)

Os frameworks que usamos hoje em dia para desenvolver aplicativos da Web têm mecanismos preventivos para proteger contra ataques de injeção SQL. Mas ainda nos deparamos com vulnerabilidades SQL Injection porque às vezes as consultas SQL brutas são usadas, às vezes o framework tem uma vulnerabilidade inata de injeção SQL ou o framework não é usado corretamente.
### Tipos de injeção de SQL
Existem três tipos de injeções SQL. Estes são os seguintes:

1. **SQLi em banda (SQLi Clássico**): Se uma consulta SQL for enviada e respondida pelo mesmo canal, chamamos esses SQLi de banda. É mais fácil para os invasores explorarem estes em comparação com outras categorias SQLi.
2. **SQLi Inferencial (Blind SQLi):** consultas SQL que recebem uma resposta que não pode ser vista são chamadas de SQLi Inferencial. Eles são chamados de Blind SQLi porque a resposta não pode ser vista.
3. **SQLi de banda:** gf Se a resposta a uma consulta SQL for comunicada através de um canal diferente, esse tipo de SQLi é chamado de SQLi Out-of-band. Por exemplo, se o invasor está recebendo respostas para suas consultas SQL sobre o DNS, isso é chamado de SQLi de banda.
## Como funciona a injeção de SQL?
Hoje, os aplicativos da Web padrão geralmente recebem dados de um usuário e usam esses dados para exibir conteúdo específico. A página de login é onde a maioria dos ataques de injeção SQL acontece. Vamos examinar como as injeções SQL funcionam através de um exemplo.

Um usuário é geralmente esperado para digitar seu nome de usuário e senha na página de login. Por outro lado, o aplicativo web usará essas informações de nome de usuário e senha para criar uma consulta SQL como a abaixo:

> SELECT ? FROM users ONDE username ? **'USERNAME** ’ E senha ? ' **USER_PASSWORD** '

O significado desta consulta SQL é “traga-me todas as informações sobre o usuário da tabela de usuários cujo nome é **USERNAME** e cuja senha é **USER_PASSWORD** ”. Se o aplicativo da Web encontrar um usuário correspondente, ele autenticar o usuário, se não conseguir encontrar um usuário após a realização da consulta, o login não terá sucesso.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/Login-page.png)

Digamos que seu nome de usuário é **john**“Johnhn”, e sua senha é **“super secretapassword”.** Quando você insere essas informações e clicar no botão de login, a consulta SQL que você vê abaixo será consultada e você poderá entrar porque houve uma correspondência encontrada após a consulta SQL.

> SELECT ? FROM users WHERE username ? ‘ **john’** E senha ? **‘supersecretpassword** ‘

Então, e se não usávamos esse sistema da maneira como ele foi projetado e colocamos um apóstrofo (') na área de nome de usuário? A consulta SQL será como abaixo e o erro será excluído do banco de dados porque a consulta estava com defeito.

> SELECT ? FROM users WHERE username ? **‘Johnhn’’** E password ? **‘supersecretpassword** ‘

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/SQL-Injection-login-page.png)

Um invasor ficaria feliz em receber uma mensagem de erro. O atacante pode manipular as informações na mensagem de erro para sua própria vantagem e também mostra que ele está no caminho certo. E se o atacante entrar em uma carga útil como a abaixo na área de nome de usuário?

> ‘ OU 1o 1 --- -

Quando o invasor envia a carga útil, o aplicativo web executará a seguinte consulta SQL:

> SELECT ? FROM users WHERE username ? ?? OR 1? 1 -- -- - AND password ? **'supersecretpassword** '

No SQL, quaisquer que sejam os caracteres depois de “----” serão percebidos como uma linha de comentários. Então, se olharmos para a consulta acima, as consultas que vêm depois de “--” não significam nada. Então, vamos remover essa parte para simplificar as coisas antes de continuarmos a examinar a consulta SQL.

> SELECT ? DOS usuários WHERE username ? ? ? OR 1

Então, agora a consulta acima se parece com isso: **“se o nome de usuário está vazio ou 1 ? 1** ”. Não é realmente importante se a área de nome de usuário é deixada vazia ou não porque 1 é sempre igual a 1. É por isso que esta consulta será sempre verdadeira e provavelmente chamará a primeira entrada no banco de dados. O invasor poderá entrar com sucesso no aplicativo da Web porque há uma correspondência.

Este exemplo é um típico ataque de injeção SQL. É claro que os ataques de injeção SQL não se limitam a este exemplo, o invasor pode usar SQL para executar comandos no sistema com a ajuda de comandos SQL, como **xp_cmdshell.**

## Como os atacantes alavancam com ataques de injeção de SQL

Para entender por que os ataques de injeção de SQL são tão criticamente importantes, vamos dar uma olhada no que um ataque de injeção de SQL pode causar.

- bypass de autenticação
- Execução de comandos
- Exfiltrando dados sensíveis
- Entradas de criação/deletando/atualizando o banco de dados
## Como prevenir injeções SQL
- **Use uma estrutura:** é claro **que** apenas usar uma estrutura não será suficiente para impedir um ataque de injeção SQL. É de extrema importância utilizar o quadro de acordo com a documentação.
- **Mantenha sua estrutura atualizada:** mantenha seu aplicativo da Web seguro seguindo as atualizações de segurança relacionadas à estrutura que você usa.
- **Sempre higienize os dados recebidos de um usuário:** Nunca confie nos dados recebidos de um usuário. Além disso, não apenas higienizar os dados do formulário, mas também fazer o mesmo com outros dados (como cabeçalhos, URLs, etc.)
- **Evite usar consultas SQL raw:** Você pode ter o hábito de escrever consultas SQL cruas, mas você deve optar por fazer uso dos benefícios que uma estrutura fornece e você também deve fazer uso da segurança que ela oferece.
## Detecção de ataques de injeção de SQL
Nós discutimos o que os atacantes podem fazer com um ataque de injeção SQL na seção anterior. Cada um dos resultados de uma injeção SQL indicado acima pode causar grandes perdas para uma instituição, de modo que, como Analistas de SOC, devemos ser capazes de detectar esses ataques e ser capazes de tomar precauções contra eles.

Então, como podemos detectar ataques SQL Injection?

Há mais de uma resposta a esta pergunta. Estes são os seguintes:
- **Ao examinar uma solicitação da Web, verifique todas as áreas que vêm do usuário:** Como os ataques de injeção SQL não se limitam às áreas do formulário, você também deve verificar os cabeçalhos de solicitação HTTP como o User-Agent.
- **Procure por palavras-chave SQL:** procure palavras como INSERT, SELECT, ONDE dentro dos dados recebidos dos usuários.
- **Verifique se há caracteres especiais:** procure apóstrofos ('), traços (-) ou parênteses que são usados em SQL ou caracteres especiais que são frequentemente usados em ataques SQL dentro dos dados recebidos do usuário.
- **Familiarize-se com cargas úteis de injeção SQL usadas com frequência:** embora as cargas SQL sejam alteradas de acordo com o aplicativo da Web, os invasores ainda usam algumas cargas úteis comuns para verificar se há vulnerabilidades de injeção SQL. Se você estiver familiarizado com essas cargas úteis, você pode facilmente detectar cargas úteis SQL Injection. Você pode ver algumas cargas úteis de SQL Injection usadas com frequência [aqui](https://github.com/payloadbox/sql-injection-payload-list).

### Detectando ferramentas de injeção SQL automatizadas
Os atacantes usam muitos dispositivos automatizados para detectar vulnerabilidades de injeção SQL. Um dos mais conhecidos é o Sqlmap. Vamos olhar para a imagem mais ampla em vez de focar em uma ferramenta específica.

Você pode usar os métodos listados abaixo para detectar dispositivos SQL Injection:

1. **Olhe para o User-Agent:** Os dispositivos de navegador automatizados *geralmente têm seus nomes e versões gravadas*. Você pode olhar para o Agente do Usuário para detectar esses dispositivos automatizados.
2. **Verifique a frequência de solicitações:** Os dispositivos automatizados foram projetados para enviar uma *quantidade estimada de muitos pedidos por segundo para poder testar cargas o mais rápido possível*. Um usuário normal pode enviar 1 solicitação por segundo, então você pode dizer se as solicitações são feitas por um dispositivo automatizado ou não olhando para o número de solicitações por segundo.
3. **Olhe para o conteúdo da carga útil:** os dispositivos automatizados *geralmente gravam seus próprios nomes em suas cargas úteis*. Por exemplo, uma carga útil SQL Injection enviada por um dispositivo automatizado pode ser assim: **sqlmap’ OR 1 ? 1**
4. **É a carga útil complicada:** este método de detecção pode nem sempre funcionar, mas com base na minha experiência, eu poderia dizer que os dispositivos automatizados enviam *cargas úteis mais complicadas*.

### Exemplo de detecção
Temos logs de acesso de um aplicativo da Web que foi vítima de um ataque de injeção de SQL.

Você pode não ter ouvido o que é um log de acesso antes. Em suma, estes são os logs de acesso do servidor web. Esses logs geralmente contêm o endereço IP de origem, data, URL solicitado, método HTTP, agente de usuário e código de resposta HTTP. Estes logs são muito úteis em investigações.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/sql-injection-access-log.png)

(Registros de Acesso por Injeção SQL)

Temos um login de acesso em mãos. Agora, o que fazemos?

Em primeiro lugar, quando olhamos para as páginas que foram solicitadas, vemos que além de páginas como “info.php”, que é bastante legível, também há pedidos feitos para páginas que são complexas e têm símbolos como %. Não podemos dizer que os pedidos de páginas como essas são maliciosas, mas o fato de serem feitas repetidamente e muitas vezes é suspeito.

Primeiro de tudo, vamos falar sobre o que os símbolos % significam. Quando solicitamos uma página que contenha caracteres especiais, essas solicitações não são diretamente transferidas para o servidor web. Em vez disso, nossos navegadores executam uma codificação de URL (Encodificação de porcentagem) dos caracteres especiais e substitui cada caractere especial por uma cadeia de caracteres que começa com % e tem 2 caracteres hexadecimais nele. Portanto, as páginas que contêm o símbolo % acima são páginas que contêm caracteres especiais.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/URL-Encoding.png)

Agora que entendemos o que os símbolos % significam, vamos revisitar os logs de acesso. Quando olhamos para as solicitações, podemos facilmente ver que, além dos símbolos %, há palavras legíveis como “UNION”, “SELECT”, “E”, “CHR”. Como estas são palavras específicas que pertencem ao SQL, podemos determinar que estamos cara a cara com um ataque de injeção SQL.

Para salvar nossos olhos, vamos tornar o exame um pouco mais fácil :) Você pode realizar uma pesquisa usando as palavras-chave “Decoder de URL Online” para encontrar aplicativos da web que farão automaticamente a decodificação de URL para você. Para ler esses registros de acesso mais fácil, obterei ajuda desses aplicativos da Web, não terei que forçar meus olhos ou os seus.

Deixe-me adicionar uma pequena nota. Não é aconselhável fazer upload de algo como um log de acesso que contém informações críticas em um aplicativo web de terceiros. Os registros de acesso que eu enviei foram preparados especificamente para este treinamento, então não há problema em fazê-lo. Mas você não deve cometer tais erros em sua vida profissional.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/Access-logs-with-URL-decoding.png)

Quando fazemos a decodificação de URL, podemos ver mais claramente que este é um ataque de injeção de SQL. Então, o que devemos fazer agora? Sim, nós confirmamos que é um ataque de injeção SQL, mas vamos deixá-lo lá?

- Claro que não. Agora vamos encontrar quaisquer outras informações que pudermos a partir desses registros de acesso.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/sql-injection-access-logs-date.png)

Primeiro, vamos ver as datas de solicitação. Todas as cargas de injeção SQL foram enviadas em “19/Fev/2022 11:09:24”. Podemos ver que mais de 50 pedidos foram feitos em 1 segundo. O fato de que tantos pedidos foram feitos em tão pouco tempo nos mostra que este é um ataque automatizado. Além disso, como mencionamos antes, quando os atacantes realizam testes manuais, eles optam por testar cargas úteis fáceis primeiro. Mas quando olhamos para os registros de acesso, vemos que as cargas são muito complicadas. Isso mostra que o ataque pode muito bem ser automatizado.

Confirmamos que um ataque de injeção SQL foi realizado e que foi realizado com um dispositivo automatizado. Então, podemos terminar a nossa análise, certo?

Mais um passo a fazer. Precisamos determinar se o ataque foi bem sucedido ou não. Você pode determinar se um ataque de injeção SQL foi bem sucedido olhando para a resposta, mas em sua carreira profissional você quase nunca terá acesso à resposta. Podemos presumir que todas as respostas serão aproximadamente do mesmo tamanho porque o ataque é realizado na mesma página e sobre a variável “id”. Podemos estimar o sucesso do ataque olhando para o tamanho da resposta.

Infelizmente, o servidor web básico que foi desenvolvido para servir como exemplo não pode fornecer um tamanho de resposta confiável. Portanto, não podemos estimar se o ataque foi bem sucedido olhando para este exemplo. Mas com servidores web que foram configurados corretamente, podemos encontrar o tamanho da resposta dentro dos logs de acesso. Você pode examinar essa área para determinar se há uma diferença notável nos tamanhos de resposta. Se houver uma diferença notável, você pode estimar que o ataque foi bem-sucedido. Mas nesta situação seria melhor escalar este alerta para um analista de nível superior.

O que nós sabemos:

1. Houve um ataque de injeção de SQL realizado no parâmetro “id” na página principal do aplicativo da web.
2. Os pedidos vieram do endereço IP: 192.168.31.174.
3. Como houve mais de 50 solicitações por segundo, esse ataque foi realizado por uma ferramenta de verificação de vulnerabilidades automatizada.
4. A natureza complexa das cargas úteis suporta a reclamação em 3 euros.
5. Não podemos determinar se a resposta foi bem-sucedida ou não porque não temos nenhuma informação sobre o tamanho da resposta.

### Arquivos de curso
[Injeção SQL - Web Attacks.rar](https://files-ld.s3.us-east-2.amazonaws.com/SQL+Injection+-+Web+Attacks.rar)

Senha: acesso

---
# Detectando ataques de scripts Cross Site (XSS)
## O que é o XSS?
O Cross Site Scripting (XSS) é um tipo de vulnerabilidade de segurança da Web baseada em injeção que é incluída em aplicativos da Web legítimos e permite que o código malicioso seja executado.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/xss.png)

Hoje, a maioria das estruturas que são usadas para desenvolver aplicativos da web tomaram medidas preventivas contra ataques de scripts entre sites. Mas ainda vemos frequentemente vulnerabilidades do XSS hoje porque as estruturas às vezes não são usadas, ou a estrutura em si tem uma vulnerabilidade XSS e os dados provenientes do usuário não são higienizados.
### Tipos de XSS
Existem três tipos diferentes de XSS. Estes são os seguintes:
1. **XSS refletido (não persistente**): é um tipo XSS não persistente que a carga útil XSS deve conter na solicitação. É o tipo mais comum de XSS.
2. **XSS (Persistente**): É um tipo de XSS onde o atacante pode carregar permanentemente a carga útil XSS para o aplicativo web. Em comparação com outros tipos, o tipo mais perigoso de XSS é o XSS armazenado.
3. **DOM Based XSS** : DOM Based XSS é um ataque XSS em que a carga útil do ataque é executada como resultado da modificação do “ambiente” DOM no navegador da vítima usado pelo script lateral do cliente original, de modo que o código do lado do cliente é executado de maneira “inesperada”. (OOWASP) (em inglês)

## Como funciona o XSS?
Assim como outros métodos de ataque na web, o XSS é uma vulnerabilidade de segurança que acontece devido à falta de higienização de dados. A vulnerabilidade XSS ocorre quando os dados recebidos do usuário são enviados na resposta sem higienização.

Vamos seguir um exemplo para entender melhor os ataques XSS.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/XSS-vulnerable-code.png)

Vejamos o pedaço de código acima. O que ele faz é realmente muito básico. Ele apenas exibe o que está inserido no parâmetro "usuário". Se entrarmos em “LetsDefend” como o parâmetro “usuário”, veremos as palavras “Olá Deixefenar”.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/XSS-image-1.png)

Até agora, não há problema. Se inserirmos os dados apropriados no parâmetro do usuário, seremos recebidos com uma saudação calorosa. Mas, como vimos acima, não há mecanismo de controle para o parâmetro do usuário. Isso significa que o que quer que insiramos no parâmetro “usuário” será incluído na Resposta HTTP que recebemos de volta.

Então, o que aconteceria se não inseríssemos um valor normal, mas inserimos uma carga útil que convocaria um pop-up?

Carga de pagamento: **?script?alert(1)/script?**

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/XSS-popup.png)

Porque o que quer que insiramos no parâmetro “user” está diretamente incluído na Resposta HTTP, o código javascript que escrevemos funcionou e uma janela pop-up apareceu na tela.

É exatamente assim que o XSS funciona. Como o valor inserido pelo usuário não é confirmado, o invasor pode inserir qualquer código javascript que ele gosta e obter o resultado que deseja. E se o atacante quiser redirecionar o usuário para um site malicioso?

Carga útil: **?script?window.location?’https://google.com’?/script?**

https://letsdefend.io/xss_example.php?user?% 3Cscript%3Ewindow.location?% 27https://google.com%27%3C/script%3E

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/XSS-google-redirect-1.png)

Claro que não vamos direcioná-lo para um aplicativo web. Dirija você para o Google será suficiente como exemplo. Quando o usuário clica no URL, ele será direcionado para o Google em vez do aplicativo web perfeito LetsDefend.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/XSS-google-redirect-2.png)

## Como os atacantes alavancam com os ataques XSS
Como o XSS é um método de ataque baseado no cliente, pode parecer menos importante do que outros métodos de ataque, mas os ataques XSS e seu impacto não devem ser tomados como garantidos.

Os atacantes podem fazer o seguinte com um ataque XSS:

- Roubar as informações de sessão de um usuário
- Iniciar processos que um usuário pode
- Capturar as credenciais

...e outras várias funções.

## Como evitar uma vulnerabilidade XSS
- **Sanitize dados provenientes de um usuário:** nunca confie em dados provenientes de um usuário. Se os dados do usuário precisam ser processados e salvos, ele deve ser codificado com codificação html usando caracteres especiais e só então deve ser salvo.
- **Use uma estrutura:** A maioria dos frameworks vem com medidas preventivas contra ataques XSS.
- **Use a estrutura corretamente:** Quase todas as estruturas usadas para desenvolver aplicativos da web vêm com um recurso de saneamento, mas se isso não for usado corretamente, ainda há uma chance de ocorrência de vulnerabilidades XSS.
- **Mantenha sua estrutura atualizada:** Frameworks são desenvolvidos por seres humanos para que eles também possam conter vulnerabilidades XSS. Mas esses tipos de vulnerabilidades são geralmente corrigidos por atualizações de segurança. Então, você deve certificar-se de que você concluiu as atualizações de segurança do seu framework.

  ## Detectando ataques XSS
Como mencionamos no artigo anterior, de acordo com um estudo feito pela Acunetix, 75% dos ataques cibernéticos são realizados em aplicações web. Como o XSS é uma das vulnerabilidades mais frequentemente testadas, você estará vendo muitas delas durante sua carreira como analista de SOC.
- **Procure por palavras-chave:** A maneira mais fácil de capturar ataques XSS é procurar palavras-chave como “alertar” e “roteiro” que são comumente usadas em cargas úteis XSS.
- **Familiarize-se com cargas úteis XSS usadas com frequência:** os atacantes usam principalmente as mesmas cargas úteis para procurar vulnerabilidades antes de explorar uma vulnerabilidade XSS. É por isso que se familiarizar com cargas úteis XSS usadas com frequência tornaria mais fácil para você detectar vulnerabilidades XSS. Você pode examinar algumas cargas úteis frequentemente usadas [aqui](https://github.com/payloadbox/xss-payload-list).
- **Verifique se algum caractere especial foi usado:** Verifique os dados provenientes de um usuário para ver se algum caractere especial que é usado com frequência em cargas úteis XSS como (-) ou menor do que (-) estão presentes.
### Exemplo de uma detecção
Neste exemplo, vemos logs de acesso de um servidor Apache com o Wordpress. Não se esqueça de revisitar nosso artigo sobre “Detecting SQL Injection Attacks” para obter mais informações sobre logs de acesso.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/XSS-apache-access-log.png)

Agora, vamos examinar os logs de acesso que foram fornecidos.

Em primeiro lugar, vamos dar uma olhada geral nos pedidos que foram feitos e tentar entendê-los. Vemos que todas as solicitações foram feitas para a página “/blog/” e que apenas os valores de parâmetro “s” foram alterados. Se você prestar atenção aos URLs das páginas da web que você visita, você teria notado que quando você realiza uma pesquisa no Wordpress, as palavras que você insere são enviadas usando o parâmetro “s?”. O exemplo que estamos olhando nos mostra que essas são pesquisas realizadas no Wordpress.

É difícil encontrar exemplos facilmente legíveis, como o exemplo no artigo “Detecting SQL Injection Attacks”. Em vez disso, encontramos caracteres que se transformaram em %XX como resultado da codificação de URL. Vamos realizar a decodificação de URL a seguir, mas primeiro vamos dar uma olhada nos URLs e tentar ver se podemos reconhecer quaisquer palavras.

Quando olhamos para os registros, notamos palavras relacionadas ao javascript como “script”, “prompt” e “console.log”. Quando vemos javascript, imediatamente traz XSS à mente. Se fizermos uma decodificação de URL, poderemos facilmente entender as solicitações feitas.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/xss-apache-access-log-with-url-decoding.png)

Quando olhamos para os logs de acesso depois de realizar uma decodificação de URL, vemos claramente as cargas úteis do XSS. Definitivamente, podemos dizer que o aplicativo Wordpress de onde temos esses registros de acesso tornou-se vítima de um ataque XSS.

Quando olhamos para os endereços IP solicitados, vemos que há mais de um. Mais de um atacante está tentando realizar um ataque XSS simultaneamente? Ou o invasor está constantemente mudando seu endereço IP para evitar ser bloqueado por produtos de segurança, como firewalls e IPS? Se você verificar o endereço IP, verá que ele pertence ao Cloudflare. Como o aplicativo Wordpress foi colocado atrás do Cloudflare, é normal que a Cloudflare esteja fazendo a solicitação.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/xss-apache-access-log-date.png)

Quando examinamos as datas dos pedidos, descobrimos que havia um pedido feito a cada 3-4 segundos. Não é realmente possível para um humano tentar entrar nessas muitas cargas XSS em tão pouco tempo, mas você pode não ser capaz de ter certeza de que o número de solicitações feitas por segundo é excessivo. Temos sorte porque temos as informações do User-Agent neste exemplo. Se examinarmos essas informações, vemos que ela pertence a uma biblioteca urllib. Isso nos mostra que essas solicitações foram feitas por meio de uma ferramenta de scanner de vulnerabilidade automatizada.

O ataque foi bem sucedido?

Não podemos dizer nada definitivo porque não temos acesso às respostas.

Como resultado de nossos exames:

1. É determinado que o ataque teve como alvo o aplicativo da Web de onde os registros de acesso vieram.
2. Depois de analisar a quantidade de solicitações e as informações do User-Agent, determinamos que o ataque foi realizado por um scanner de vulnerabilidade automatizado.
3. Como o aplicativo está por trás do Cloudflare, os endereços IP de origem não foram encontrados.
4. Não sabemos se o ataque foi bem sucedido ou não.

---
# Detectando Ataques de Injeção de Comando
## O que são ataques de injeção de comando?
Ataques de injeção de comando são ataques que acontecem quando os dados recebidos de um usuário não são higienizados e são transmitidos diretamente para o shell do sistema operacional.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/command-injection.png)

Os atacantes exploram vulnerabilidades de injeção de comandos para executar diretamente comandos no sistema operacional. O fato de que a prioridade do invasor é assumir o controle do sistema torna essas vulnerabilidades mais críticas do que outras vulnerabilidades.

Como o comando que o invasor envia usará os direitos do usuário do aplicativo da Web, um aplicativo da Web mal configurado concederia ao invasor acesso com direitos de administrador.
## Como funciona a injeção de comando?
Vulnerabilidades de injeção de comando acontecem quando os dados recebidos do usuário não são higienizados. Vamos examinar as vulnerabilidades de injeção de comando com um exemplo.

Digamos que tenhamos um aplicativo web básico que copia o arquivo do usuário na pasta “/tmp”. O código do aplicativo web está abaixo.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/web-application-code-example.png)

Em condições normais, a aplicação funcionará normalmente se usada com precisão. Por exemplo, se carregarmos um arquivo chamado `letsdefend.txt`, ele copiará com êxito o arquivo para a pasta `/tmp`.

Então, o que acontecerá se carregarmos um arquivo chamado “letdefend;ls;.txt”? O comando se tornaria:

Comando: `cp letsdefend;ls;.txt`

“;” significa que o comando terminou. Então, quando olhamos para a carga útil acima, existem três comandos diferentes que o sistema operacional executa. Estes são os seguintes:

1. `cp letsdefend`
2. `ls`
3. `.txt`

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/command-injection-example.png)

O primeiro comando é para o processo de cópia, mas se os parâmetros não forem inseridos corretamente, ele não funcionará corretamente.

Comando 2 é o comando de listagem de diretórios que o invasor deseja executar. O usuário não recebe a saída do comando para que o atacante não possa ver os arquivos no diretório, mas o sistema operacional executa com sucesso o comando.

Quando o sistema operacional quiser executar o comando número 3, haverá uma mensagem de erro porque não há comando ".txt".

Como você vê, o código foi executado no sistema operacional do servidor web. Então, e se o invasor enviar um arquivo chamado “letsdefend;shutdown;.txt”? O sistema operacional seria desligado e o aplicativo da Web não poderá funcionar.

O invasor pode criar um shell reverso no sistema operacional com a ajuda da carga precisa.
## Como os atacantes alavancam com ataques de injeção de comando

Os atacantes podem executar comandos em um sistema operacional explorando vulnerabilidades de injeção de comando. Isso significa que o aplicativo web e todos os outros componentes do servidor estão em risco.
## Como evitar a injeção de comando
- **Sempre higienizar os dados recebidos de um usuário:** Nunca confie nos dados recebidos de um usuário. Nem mesmo um nome de arquivo!
- **Limite os direitos de usuário:** Ajuste os direitos de usuário de aplicativos da Web a um nível mais baixo sempre que possível. Dificilmente qualquer aplicativo da Web exige que o usuário tenha direitos de administrador.
- **Faça uso de tecnologias de virtualização, como dockers**
## Detectando Ataques de Injeção de Comando
Acho que todos nós entendemos muito bem o nível de criticidade da vulnerabilidade de injeção de comando. Se tal vulnerabilidade crítica for explorada e não detectada, a empresa envolvida pode perder uma grande quantidade de dinheiro e reputação.

Então, como podemos detectar Ataques de Injeção de Comando?

Há mais do que uma maneira. Estes são os seguintes:

- **Ao examinar uma solicitação da web, veja todas as áreas:** a vulnerabilidade de injeção de comando pode estar localizada em várias áreas, dependendo da operação do aplicativo da Web. É por isso que você deve verificar todas as áreas do pedido da web.
- **Procure palavras-chave relacionadas ao idioma do terminal:** Verifique os dados recebidos do usuário para palavras-chave relacionadas a comandos terminais, tais como: dir, ls, cp, cat, tipo, etc.
- **Familiarize-se com cargas úteis de injeção de comando usadas com frequência:** quando os invasores detectam uma vulnerabilidade de injeção de comando, eles geralmente criam um shell reverso para funcionar mais facilmente. É por isso que conhecer cargas úteis de injeção de comando usadas com frequência facilitará a detecção de um ataque de injeção de comando.
### Exemplo de detecção
Neste exemplo, não vamos olhar para os logs de acesso, em vez disso, estaremos examinando uma solicitação HTTP.

```shell
 GET / HTTP/1.1 (emo)

Anfitrião: yourcompany.com
 
Agente do Usuário: () :; ; eco "NS:" $(/etc/passwd)

Aceitar: texto/html, aplicativo/xhtml+xml+xml, aplicação/xml; q-0,9, imagem/avif, imagem/webp,image/apng,/ang,/?; q-0, s a 0.8, aplicação/signed-exchange;v-b3;q

Aceitar-Encoding: gzip, desinflar

Aceitar-Language: en-US,en; sq ? 0,9

Conexão: fechar
```

Se olharmos para a solicitação HTTP acima, vemos que a página principal do aplicativo web yourcompany [.]com foi solicitada.

Mas quando olhamos para os cabeçalhos de solicitação HTTP, vemos uma situação suspeita no cabeçalho User-Agent. Há um comando bash no cabeçalho User-Agent, enquanto deve haver informações de navegador / sistema operacional aqui.

Na verdade, este pedido foi capturado durante a exploração de uma vulnerabilidade chamada Shellshock. Shellshock é uma fraqueza de segurança que foi publicada em 2014 e teve grandes efeitos.

Shellshock é uma vulnerabilidade de segurança que se origina de bash de alguma forma involuntariamente executando variáveis de ambiente. Shellshock é um ótimo exemplo de um ataque de injeção de comando.

Quando o comando bash localizado dentro do User-Agent for executado, o conteúdo do arquivo `/etc/passwd` será retornado ao atacante no cabeçalho de Resposta HTTP como “NS”.

---
# Detectando Ataques Inseguros de Referência de Objetos Diretos (IDOR)

## O que é o IDOR?
**I** nsecure **D** irect **O**bject **R** eference (IDOR), é uma vulnerabilidade causada pela falta de um mecanismo de autorização ou porque não é usado corretamente. Permite que uma pessoa acesse um objeto que pertence a outro.

![](https://letsdefend.io/blog/wp-content/uploads/2022/03/idor.png)

Entre os maiores riscos de segurança de vulnerabilidades de aplicativos da Web publicados no OWASP 2021, o IDOR ou o “Controle de Acesso Arrotível” ocorre em primeiro lugar.

## Como funciona o IDOR
O IDOR não é uma vulnerabilidade onde o invasor manipula os parâmetros enviados para o aplicativo web, ganha acesso a um objeto que não pertence a si mesmo e é capaz de ler, alterar ou apagar o conteúdo.

Aqui está um exemplo para entender melhor como a vulnerabilidade do IDOR é explorada.

Imagine um aplicativo web básico. Ele recupera a variável **“id”** do usuário e exibe dados que pertencem ao usuário que fez a solicitação.

URL: **https://letsdefend.io/get_user_information?id**

Quando uma solicitação é feita em nosso aplicativo da Web, como a acima, ela exibe as informações do usuário com um valor de id de 1.

Se eu for o usuário que fez a solicitação e meu valor de id é 1 tudo funcionará normalmente. Quando fizer o pedido, verei as minhas informações pessoais.

Mas o que acontece se fizermos um pedido com 2 como o parâmetro “id”? Ou 3?

Se o aplicativo da Web não estiver controlando: “O valor “id” na solicitação pertence à pessoa que faz a solicitação?”, então qualquer pessoa pode fazer essa solicitação e ver minhas informações pessoais.Essa vulnerabilidade na web é chamada IDOR.

Os atacantes podem alcançar objetos que não pertencem a si mesmos, alterando parâmetros como o “id”. A que tipo de informação eles podem ter acesso pode mudar de acordo com o aplicativo da web, mas de qualquer maneira você não gostaria que ninguém acessasse suas informações pessoais, certo?
## Como os atacantes alavancam com ataques IDOR
O que um invasor pode fazer é limitado pela área de uma vulnerabilidade IDOR. Mas as áreas mais comuns que são vistas são geralmente páginas onde as informações de um usuário são recebidas. Se um invasor explorar uma vulnerabilidade IDOR, ele poderá:

- Roubar informações pessoais
- Acesse documentos não autorizados
- Conduzir processos não autorizados (por exemplo: eliminação, alteração)
# Como evitar o IDOR
Para estabelecer um ambiente seguro sem uma vulnerabilidade IDOR, você deve sempre verificar se a pessoa que fez a solicitação tem alguma autoridade.

Além disso, parâmetros desnecessários devem ser removidos e apenas a menor quantidade de parâmetros deve ser tirada do usuário. Se pensarmos no exemplo anterior, não precisamos obter o parâmetro “id”. Em vez de obter o parâmetro “id” do usuário, podemos identificar a pessoa que fez a solicitação usando as informações da sessão.

## Detectando ataques IDOR
Os ataques IDOR são mais difíceis de detectar do que outros ataques. Porque não tem determinadas cargas úteis, como SQL Injection e XSS.

Ter a resposta HTTP em questão ajudaria a identificar ataques IDOR. Mas as respostas HTTP não são registradas por várias razões e, portanto, é mais difícil identificar ataques IDOR.

Existem alguns métodos usados para identificar ataques IDOR. Estes são os seguintes:

- **Verifique todos os parâmetros:** uma vulnerabilidade IDOR pode ocorrer em qualquer parâmetro. É por isso que você não deve esquecer de verificar todos os parâmetros.
- **Olhe para a quantidade de solicitações feitas para a mesma página:** quando os invasores detectam uma vulnerabilidade IDOR, eles também desejam acessar as informações relacionadas a todos os outros usuários, portanto, geralmente realizam um ataque de força bruta. É por isso que você pode ver muitas solicitações feitas para a mesma página de uma fonte.
- **Tente encontrar um padrão:** Os atacantes planejarão um ataque de força bruta para alcançar todos os objetos. Porque eles vão realizar o ataque em valores sucessivos e previsíveis como valores inteiros, você pode tentar encontrar um padrão nessas solicitações. Por exemplo: se você vir solicitações como id'1, id'2, id'3, você pode suspeitar de algo.

### Exemplo de detecção
Abaixo você pode ver uma imagem de tela de logs encontrados em um servidor web executando o Wordpress.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/idor-apache-access-log.png)

Como em nossos outros exemplos, vamos começar com um exame geral, de base ampla. Como não há caracteres especiais incluídos nas solicitações que foram feitas, podemos ler facilmente os logs.

Se você tiver usado o aplicativo Wordpress antes de saber que a página “wp-admin/user-edit.php?user_id” contém informações sobre usuários registrados do Wordpress. Pode ser visto normalmente para poder acessar esta página, na verdade, se você tem mais de um usuário, você pode estar ganhando acesso com mais de um “user_id: parâmetro. Mas não é normal ter tantos parâmetros diferentes de “user_id”.

Parece que temos um ataque IDOR em nossas mãos.

---
# Detecção de ataques RFI e LFI
## O que é a inclusão de arquivos locais (LFI)?
A inclusão de arquivos locais (LFI) é a vulnerabilidade de segurança que ocorre quando um arquivo é incluído sem desinfetar os dados obtidos de um usuário. Ele difere do RFI porque o arquivo que se destina a ser incluído está no mesmo servidor web em que o aplicativo da Web está hospedado.

Os invasores podem ler arquivos sensíveis no servidor da Web, eles podem ver os arquivos que contêm senhas que lhes permitiriam chegar ao servidor remotamente.
## O que é a Inclusão Remota de Arquivos (RFI)?
A Inclusão Remota de Arquivo (RFI) é a vulnerabilidade de segurança que ocorre quando um arquivo é incluído sem higienizar os dados obtidos de um usuário. Ele difere de LFI em que o arquivo que se destina a ser incluído está hospedado em um servidor diferente.

Os invasores hospedam códigos maliciosos em seu servidor preparado e convidam o site da vítima pelo servidor remoto e tentam fazer com que ele seja executado.
## Como funciona a LFI & RFI?
Assim como a maioria das vulnerabilidades baseadas em aplicativos da Web, o LFI e o RFI também têm vulnerabilidades causadas por não higienizar dados recebidos de um usuário.

As vulnerabilidades RFI e LFI são causadas pelo uso de dados recebidos de um usuário diretamente no sistema ou para incluir um arquivo em um servidor remoto.

Por que os dados recebidos de um usuário seriam usados para incluir um arquivo? Os aplicativos da Web tornaram-se altamente complicados e, infelizmente, cada recurso que é desenvolvido é usado para fins maliciosos. A opção de idioma encontrada em aplicativos da Web é usada para incluir arquivos baseados em dados recebidos de um usuário.

![](https://letsdefend.io/blog/wp-content/uploads/2022/02/local-file-inclusion-code-example.png)

Se examinarmos o pedaço de código na imagem acima, veremos que o idioma desejado é selecionado usando o parâmetro “idioma” recebido do usuário.

Em uma situação normal, o aplicativo web funcionará conforme planejado. Por exemplo, se “en” for inserido como o parâmetro “linguagem”, receberemos o arquivo visto abaixo.

`website/ **en** /home.php`

Mas se um invasor inserir a carga útil vista abaixo no parâmetro “idioma”, infelizmente, o aplicativo da Web exibirá o arquivo “/etc/passwd” para o usuário.

Carga de pagamento: `/../../../../../../.../..../.../etc/passwd%00`

`site//../../../.../../../../../.../../../.etc/passwd%00/home.php`

“../” é usado para ir para o diretório pai. Como o invasor não sabe em qual diretório o aplicativo da Web está, ele se esforça para alcançar o diretório “root” usando “../”. Mais tarde, ele nomeia o arquivo “/etc/passwd” e permite a inclusão do arquivo dentro do aplicativo web. “%0” é usado para terminar a string. Desta forma, a string restante “/home.php” não é lida pelo aplicativo da Web.
## Como os atacantes alavancam com a RFI e LFI
- Execução de código
- Divulgação de informações sensíveis
- A negação do serviço
## Como prevenir o LFI & RFI
A maneira mais eficaz de prevenir ataques RFI e LFI é higienizar todos os dados recebidos de um usuário antes de usá-lo. Não se esqueça que os controles baseados no cliente são facilmente ignorados. É por isso que você deve sempre fazer seus controles no lado do cliente e no lado do servidor.
## Detecção de ataques LFI e RFI
Anteriormente, mencionamos o que os atacantes podem realizar com ataques RFI e LFI. Como uma empresa pode sofrer uma grande perda devido à exploração de tais vulnerabilidades, devemos ser capazes de detectar tais ataques e tomar precauções.

- **Ao examinar uma solicitação da web de um usuário, examine todos os campos.**
- **Verifique se há caracteres especiais:** Dentro dos dados recebidos dos usuários, especialmente procure por notações como ‘/’, ?. ., ?.
- **Familiarize-se com arquivos usados com frequência em ataques LFI:** Em um ataque LFI, o atacante lê os arquivos que estão no servidor. Se você se familiarizar com os nomes de arquivos críticos no servidor, você pode detectar ataques LFI com mais facilidade.
- **Pesquisar por acrônimos como HTTP e HTTPS:** Em ataques RFI, o invasor inclui o arquivo em seu próprio dispositivo e permite que o arquivo seja executado.
- Para incluir um arquivo, os invasores geralmente configuram um pequeno servidor web em seu próprio dispositivo e exibem o arquivo por um protocolo HTTP. É por isso que você deve procurar por notações como “http” e “https” para detectar ataques RFI com mais facilidade.