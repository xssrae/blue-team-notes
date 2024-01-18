---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
# Introdução ao phishing
Os ataques de phishing correspondem à fase de **"Entrega"** no modelo **Cyber Kill Chain** criado para analisar ataques cibernéticos. A fase de entrega é o passo em que o atacante transmite o conteúdo prejudicial previamente preparado para os sistemas / pessoas da vítima.

![](https://umuttosun.com/wp-content/uploads/2020/06/Intrusion_Kill_Chain_-_v2-1.png)

Os atacantes geralmente visam clicar no link prejudicial no e-mail, como “você ganhou um presente”, “não perca o grande desconto”, “se você não clicar no link no e-mail sua conta será suspensa” para direcionar os usuários para clicar nos links no e-mail.

![](https://letsdefend.io/blog/wp-content/uploads/2020/08/Screen-Shot-2020-08-22-at-10.43.37-1024x916.png)


# Busca por Informações
### Spoofing
Usando a técnica chamada **spoofing**, os atacantes podem enviar e-mails em nome de outra pessoa, pois os e-mails não têm necessariamente um mecanismo de autenticação. Vários protocolos foram criados para evitar a técnica de Spoofing por e-mail. Com a ajuda dos protocolos **SPF**, **DKIM** e **DMARC**, pode ser entendido se o endereço do remetente é falso ou real. Alguns aplicativos de e-mail fazem essas verificações automaticamente. No entanto, o uso desses protocolos não é obrigatório e, em alguns casos, pode causar problemas.

- Quadro de política do remetente (SPF)
- Mail identificado (DKIM)

Para descobrir manualmente se o e-mail é paródia ou não, o endereço SMTP do e-mail deve ser aprendido primeiro. Os registros SPF, DKIM, DMARC e MX do domínio podem ser aprendidos usando ferramentas como o [Mxtoolbox](https://mxtoolbox.com/). Ao comparar as informações aqui, pode-se aprender se o e-mail é paródia ou não.

![](https://umuttosun.com/wp-content/uploads/2020/05/Screen-Shot-2020-05-10-at-15.21.06-1-1024x291.png)

Uma vez que os endereços IP das grandes instituições que utilizam os seus próprios servidores de correio lhes pertencerão, pode-se examinar se o endereço SMTP pertence a essa instituição, olhando para os registos whois do endereço IP SMTP.

Um ponto importante aqui é que, se o endereço do remetente não for paródia, não podemos dizer que o correio é seguro. Os e-mails nocivos podem ser enviados em nome de pessoas confiáveis por hackear endereços de e-mail corporativos / pessoais. Esse tipo de ataque cibernético já aconteceu, então essa possibilidade deve ser sempre considerada.
### Análise de Tráfego de E-mail
Muitos parâmetros são necessários ao analisar um ataque de phishing. Podemos aprender o tamanho do ataque e o público-alvo nos resultados de pesquisa a serem feitos no gateway de e-mail de acordo com os seguintes parâmetros.

- Endereço do remetente(info-letsdefend.io)
- Endereço IP SMTP(127.0.0.1)
- ?letsdefend.io (base de domínio)
- letsdefend (Além da conta do Gmail, o invasor pode ter enviado a partir da conta do hotmail)
- Indivíduo (ender address e SMTP podem estar em constante mudança)

Nos resultados da pesquisa, é necessário aprender os endereços de destinatário e informações de tempo além dos números de e-mail. Se os e-mails prejudiciais forem constantemente encaminhados para os mesmos usuários, seus endereços de e-mail podem ter vazado de alguma forma e compartilhado em sites como o PasteBin.

Os atacantes podem encontrar endereços de e-mail com a ferramenta Harvester no Kali Linux. Recomenda-se que tais informações não sejam compartilhadas explicitamente, pois manter endereços de e-mail pessoais em sites seria um potencial vetor de ataque para invasores.

Se os e-mails forem enviados *fora do horário de trabalho*, o atacante pode estar **vivendo em uma linha de fuso horário diferente**. Ao coletar essas informações, podemos começar a entender o ataque.

# O que é um cabeçalho de e-mail e como lê-os?
Nesta seção, explicaremos quais são as informações do cabeçalho em um e-mail, o que pode ser feito com essas informações e como acessar essas informações. É importante seguir esta seção com cuidado, pois explicaremos como realizar a análise de cabeçalho na próxima seção.  
### O que é um Email Header?
"Header" é basicamente uma seção do e-mail que contém informações como remetente, destinatário e data. Além disso, existem campos como "Return-Path", "Reply-To" e "Recebido". Abaixo você pode ver os detalhes do cabeçalho de um e-mail de amostra.

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/email-header.PNG)  
  
  
### O que o cabeçalho de e-mail faz?
**Permite a identificação do remetente e do destinatário**  
Graças aos campos "De" e "Para" no cabeçalho, é determinado a quem um e-mail irá para quem. Se olharmos para o e-mail acima que você baixou no formato "eml", vemos que ele foi enviado a partir do endereço "ogunal-letsdefend.io" para "info-letsdefend.io"
  
![](https://letsdefend.io/blog/wp-content/uploads/2022/03/sample-subject.png)  
  
**Bloqueador de Spam**  
É possível detectar e-mails de spam usando a análise de cabeçalho e outros métodos diferentes. Isso protege as pessoas de receber e-mails de SPAM.

**Permite o rastreamento de uma rota de e-mail**  
É importante verificar a rota que segue para ver se um e-mail veio do endereço certo. Se olharmos para o e-mail de exemplo acima, vemos que ele veio do endereço "ogunal-letsdefend.io", mas realmente veio do domínio "letdefend.io" ou de um servidor falso diferente que imita o mesmo nome? Podemos usar as informações de cabeçalho para responder a essa pergunta.

### Campos importantes
**A partir de**  
O campo "De" no cabeçalho da Internet indica o nome e o endereço de e-mail do remetente.  
  
**Para a sua forma de**  
Este campo no cabeçalho do mail contém os detalhes do destinatário do e-mail.  

Inclui o seu nome e o endereço de e-mail. Campos como CC (cópia de carbono) e BCC (cópia cega de carbono) também se enquadram nesta categoria, pois todos incluem detalhes de seus destinatários.  
  
Se você quiser saber mais sobre cópia de carbono e cópia cega de carbono, confira como usar CC e BCC.  
  
**Data de lançamento**  
Este é o carimbo de data/hora que mostra quando o email foi enviado.  
  
No Gmail, geralmente segue o formato do "dia dd month yyyyy hh:mmss  
  
Então, se um e-mail tivesse sido enviado no dia 16 de novembro de 2021, às 16:57:23, ele apareceria como Qua, 16 Nov 2021 16:57:23.  
  
**Assunto**  
O assunto menciona o tema do e-mail. Ele resume o conteúdo de todo o corpo da mensagem.  
  
**Return-PathTradução**  
Este campo de cabeçalho de e-mail também é conhecido como Reply-To. Se você responder a um e-mail, ele irá para o endereço mencionado no campo Return-Path.  
  
**Chave de domínio e assinaturas DKIM**  
A Chave de Domínio e o Mail Identificado por Chave de Domínio (DKIM) são assinaturas de e-mail que ajudam os provedores de serviços de e-mail a identificar e autenticar seus e-mails, semelhantes às assinaturas SPF.  
  
**Message-IDTradução**  
O campo de cabeçalho de ID de mensagem é uma combinação única de letras e números que identifica cada e-mail. Não há dois e-mails que tenham o mesmo ID de mensagem.  
  
**Versão do MIME**  
Multipurpose Internet Mail Extensions (MIME) é um padrão de codificação da Internet. Ele converte conteúdo não textual como imagens, vídeos e outros anexos em texto para que possam ser anexados a um e-mail e enviados por SMTP (Simple Mail Transfer Protocol).  
  
**Recebido**  
O campo recebido lista cada servidor de e-mail que passou por um e-mail antes de chegar na caixa de entrada do destinatário. Ele está listado em ordem cronológica inversa - onde o servidor de e-mail na parte superior é o último servidor que a mensagem de e-mail passou, e a parte inferior é onde o e-mail se originou.  
  
**Status do X-Spam**  
O status X-Spam mostra a pontuação de spam de uma mensagem de e-mail.  
Primeiro, ele destacará se uma mensagem é classificada como spam.  
Em seguida, a pontuação de spam do e-mail é mostrada, bem como o limite para o spam para o e-mail.  
Um e-mail pode atender ao limite de spam de uma caixa de entrada ou excedê-lo. Se for muito spam e exceder o limite, será automaticamente classificado como spam e enviado para a pasta de spam.

_Definição de campo: gmass.co_

  
### Como acessar seu cabeçalho de e-mail?
**Gmail (em inglês)**  
  
**1- Abrir o e-mail relevante**  
**2- Clique nos 3 pontos no canto superior direito "..."**  
**3- Clique no botão "Download message".**  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/mail-header-gmail.PNG)

  
**Downloaded ".Abra o arquivo com a extensão "eml" com qualquer aplicativo notebook**  
  
**Perspectiva**  
  
**1- Abrir o e-mail relevante**  
**2- Arquivo - ? Info - ? Propriedades - ? Cabeçalhos da Internet**  
  

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/outlook-1.png)



![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/outlook2.png)

# Análise de cabeçalho de e-mail

Nas seções anteriores, falamos sobre o que é um e-mail de phishing, o que é informações de cabeçalho e o que ele faz. Agora, quando suspeitamos que um e-mail é phishing, saberemos o que devemos fazer e como deve ser o processo de análise.

Aqui estão as principais perguntas que precisamos responder ao verificar os títulos durante uma análise de phishing:

- O e-mail foi enviado do **servidor SMTP** correto?
- Os dados "De" e "Return-Path / Reply-To" são os mesmos?
### Servidor SMTP correto?
Podemos verificar o campo "Recebido" para ver o caminho seguido pelo e-mail. Como a imagem abaixo mostra, o e-mail é 101.29.994.116 do servidor de endereços IP.

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/received-header.PNG)

Se olharmos para quem está enviando o e-mail ("remetente"), vemos que ele veio do domínio Letsdefend.io

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/email-from.PNG)

Assim, em circunstâncias normais, "letdefend.io" deve usar, "101[.]99.94.116" para enviar e-mails. Para confirmar esta situação, podemos consultar os servidores MX ativamente utilizados por "letsdefend.io"

- O site [MX Lookup](https://mxtoolbox.com/) ajuda mostrando-lhe os servidores MX utilizados pelo domínio que você pesquisou.

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/mxtoolbox.PNG)

Se olharmos para a imagem acima, o domínio "letdefend.io" usa endereços do Google como um servidor de e-mail. Portanto, não há nenhuma relação com os endereços emkei[.]cz ou "101[.]99.94.116".

Nesta verificação, foi determinado que o e-mail não veio do endereço original, mas foi falsificado.
### Os dados "De" e "Return-Path / Reply-To" são os mesmos? 
Exceto em casos excepcionais, esperamos que o remetente do e-mail e a pessoa que recebe as respostas sejam as mesmas. Um exemplo de por que essas áreas são usadas de forma diferente em ataques de phishing:

Alguém envia um e-mail (gmail, hotmail etc.) com o mesmo sobrenome de alguém que trabalha para o Google para LetsDefend, LetsDefend diz ao funcionário que ele emitiu a fatura e eles devem fazer o pagamento em sua conta XXX. Ele coloca o endereço de e-mail do verdadeiro funcionário do Google no campo "Reply-to" para que o endereço de e-mail falso não se destaque no caso de responder a um possível e-mail.  
  
Retornando ao e-mail que baixamos acima, tudo o que temos a fazer é comparar os endereços de e-mail nos campos "De" e "Rep-to".

![](https://letsdefend-images.s3.us-east-2.amazonaws.com/Courses/Phishing+Email+Analysis/reply-to.PNG)

Como você pode ver, os dados são diferentes. Em outras palavras, quando quisermos responder a este e-mail, enviaremos uma resposta para o endereço do Gmail abaixo. Só porque esses dados são diferentes *nem sempre* significa que é definitivamente um e-mail de phishing, precisamos **considerar o evento como um todo**. Em outras palavras, além dessa situação suspeita, se houver um anexo prejudicial, URL ou conteúdo enganoso no conteúdo do e-mail, podemos entender que o e-mail é phishing. Na continuação do treinamento, analisaremos os dados na parte do corpo do e-mail.

# Análise estática
Os aplicativos de e-mail fornecem **suporte HTML**, permitindo a criação de e-mails que podem atrair mais atenção dos usuários. Os atacantes podem criar e-mails com HTML, ocultando endereços de URL que são prejudiciais por trás de botões / textos que parecem inofensivos.

![](https://letsdefend.io/blog/wp-content/uploads/2020/08/Screen-Shot-2020-08-22-at-10.45.13-1024x242.png)

Como visto na imagem acima, o endereço que o usuário vê pode ser diferente quando o link é clicado (o endereço real é visto quando o link é pairado).

> Os invasores tomam um novo endereço de domínio na maioria dos ataques de phishing e fazem um ataque de phishing em poucos dias e terminam seu trabalho. Por esse motivo, se o nome de domínio no e-mail for novo, é mais provável que seja um ataque de phishing.

É possível descobrir se os mecanismos antivírus detectam o endereço da Web como prejudicial, pesquisando os endereços da Web no e-mail no [**VirusTotal**](https://www.virustotal.com/gui/). Se alguém já analisou o mesmo endereço / arquivo no VirusTotal, o VirusTotal não analisa do zero, ele mostra o resultado de análise antigo. Podemos usar esse recurso como uma vantagem e uma desvantagem.

![](https://umuttosun.com/wp-content/uploads/2020/05/Screen-Shot-2020-05-04-at-05.07.11-1024x156.png)

Se o invasor pesquisar o endereço de domínio no VirusTotal sem conter conteúdo nocivo, esse endereço aparecerá inofensivo no VirusTotal e se ele passar despercebido, você pode ser confundido com esse endereço como inofensivo. Na imagem acima, você pode ver que o endereço umuttosun.com parece inofensivo, mas se você olhar para a seção marcada com a seta vermelha, você verá que este endereço foi pesquisado há 9 meses, e esse resultado é há 9 meses. Para que ele seja analisado novamente, o botão marcado com a seta azul deve ser pressionado.

Se a página foi pesquisada anteriormente no VirusTotal, isso pode significar que o invasor queria ver a taxa de detecção do site durante a fase de preparação. Se o analisarmos novamente, o mecanismo antivírus o detecta como phishing, o que significa que o invasor tem um movimento para enganar os analistas.

Realizar a análise estática dos arquivos no e-mail pode permitir o aprendizado da capacidade / capacidades desse arquivo. No entanto, como a análise estática leva muito tempo, você pode obter as informações necessárias mais rapidamente com a análise dinâmica.

[A Cisco Talos Intelligence](https://talosintelligence.com/) tem seções de pesquisa onde podemos aprender reputações de endereços IP. Ao pesquisar o endereço SMTP do e-mail que detectamos no Talos, podemos ver a reputação do endereço IP e descobrir se ele está incluído na lista negra. Se o endereço SMTP estiver na lista negra, pode-se entender que um ataque foi feito em um servidor comprometido.

![](https://umuttosun.com/wp-content/uploads/2020/05/Screen-Shot-2020-05-10-at-15.26.00-1-1024x453.png)

Da mesma forma, o endereço SMTP pode ser pesquisado no VirusTotal e no AbuseIPDB para determinar se o endereço IP esteve envolvido anteriormente em atividades maliciosas.

# Análise dinâmica
URLs e arquivos podem ser encontrados no e-mail. Esses arquivos e endereços de URL precisam ser examinados. Você não quer que seus dados sejam roubados por hackers executando esses arquivos em seu computador pessoal. Por esse motivo, os sites e arquivos no e-mail devem ser executados em ambientes de sandbox e as alterações feitas no sistema devem ser examinadas, e deve ser verificado se eles são prejudiciais ou não.

![](https://letsdefend.io/blog/wp-content/uploads/2020/08/Screen-Shot-2020-08-22-at-10.52.32-1024x498.png)

Se você quiser verificar rapidamente os endereços da web no e-mail, você pode ver o conteúdo do site usando navegadores da web on-line, como [o Browserling](https://www.browserling.com/). A coisa boa sobre esses serviços é que você não será afetado por uma possível vulnerabilidade de dia zero que afeta os navegadores, já que você não vai para a página da web em seu próprio computador. A desvantagem de usar navegadores da Web, como o Browserling, é que, se o arquivo malicioso for baixado no site, você não poderá executar esse arquivo. Por esta razão, sua análise será interrompida.

![](https://letsdefend.io/blog/wp-content/uploads/2020/08/Screen-Shot-2020-08-22-at-10.45.13-1024x242.png)

Antes de ir para os endereços no correio, deve ser verificado se há informações importantes no endereço. Quando examinamos o exemplo na imagem acima, quando o usuário clica em popularshoppingsite[.]com, é visto que o endereço do usuário é realmente visitado e o endereço de e-mail do usuário no parâmetro de e-mail. Mesmo que o usuário não insira sua senha na página de phishing, isso significa que o link no e-mail é acessado quando esse endereço é acessado e o invasor entende que esse usuário é válido. Ele pode aumentar a taxa de sucesso do ataque que realizará fazendo ataques de engenharia social sobre os usuários que são válidos nos ataques que realizarão mais tarde. Por esse motivo, é necessário alterar as informações, como o endereço de e-mail, antes de acessar os endereços.

![](https://letsdefend.io/blog/wp-content/uploads/2020/08/Screen-Shot-2020-08-22-at-10.48.01.png)

Você pode examinar arquivos e sites suspeitos em ambientes sandbox. Quando você examina os arquivos nesses ambientes, você remove o risco de infectar seu computador com malware. Muitos serviços / produtos de sandbox estão disponíveis. Estes produtos / serviços estão disponíveis para uso pago e gratuito. Você pode escolher um / mais destes serviços de acordo com suas necessidades.

Algumas sandboxes comumente usadas:

- [VMRay](https://www.vmray.com/)
- [Cuckoo Sandbox](https://cuckoosandbox.org/)
- [JoeSandbox](https://www.joesandbox.com/)
- [AnyRun](https://any.run/)
- [Hybrid Analysis](https://www.hybrid-analysis.com/)

# Técnicas adicionais
Outra técnica que os invasores usam é realizar ataques de phishing usando sites normalmente legais. Alguns deles são os seguintes.

- **Usando serviços que oferecem serviços de Cloud Storage, como Google e Microsoft**
    - Os atacantes tentam clicar em endereços de unidade do Google / Microsoft que parecem inofensivos para o usuário, carregando arquivos nocivos na unidade.
- **Usando serviços que permitem a criação de subdomínios gratuitos, como Microsoft, Wordpress, Blogspot, Wix**
    - Os atacantes tentam enganar os produtos e analistas de segurança criando um subdomínio gratuito desses serviços. Como a informação whois não pode ser pesquisada como um subdomínio, pode-se ver que esses endereços foram tomados no passado e pertencem a instituições como a Microsoft, Wordpress.
- **Aplicações de formulários**
    - Estão disponíveis serviços que permitem a criação de formulários livres. Os atacantes usam esses serviços em vez de criar um site de pesca. Como o domínio é inofensivo em condições normais, ele pode passar para o usuário sem ficar preso no software antivírus. O formulário do Google é um exemplo desses serviços. Ao olhar para a informação whois, o domínio pode ser visto como Google, para que o invasor possa enganar os analistas.