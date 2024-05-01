---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
## **Registros de Login do Windows**

Um invasor geralmente quer fazer login no servidor para assumir o controle do sistema. Para este fim, ele pode executar ataque de força bruta ou fazer login diretamente com a senha em mãos. Em ambos os casos (inscreção bem-sucedida / tentativa de login mal sucedida) o log será criado.

Vamos considerar um invasor conectado ao servidor após um ataque de força bruta. Para analisar melhor o que o atacante fez depois de entrar no sistema, precisamos encontrar a data de login. Para isso, precisamos de “ID de evento 4624 – Uma conta foi registrada com sucesso”.

Cada log de eventos tem seu próprio valor de ID. Filtrar, analisar e pesquisar o título do log é mais difícil, por isso é fácil usar o valor de ID.

Você pode encontrar os detalhes de qual valor de ID do evento significa o que a partir do endereço URL abaixo.

[https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx)

Para alcançar o resultado, abrimos o “Visitador de Eventos” e selecionamos logs de “Segurança”.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-1.jpeg)

Em seguida, criamos um filtro para o ID de evento “4624”.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-2-1024x585.jpeg)

E agora vemos que o número de logs diminuiu significativamente e estamos apenas listando registros para atividades de login bem-sucedidas. Olhando para os detalhes do log, vemos que o usuário de “LetsDefendTest” fez login pela primeira vez às 23/02/2021 22:17.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-3.jpeg)

Quando olhamos para o campo “Tipo de Logon”, vemos o valor 10. Isso indica que você está conectado com “Serviços de Área de Trabalho Remota” ou “Protocolo de Área de Trabalho Remota”.

Você pode encontrar o significado dos valores de tipo de logon na página da Microsoft.

[https://docs.microsoft.com/pt-us/windows/security/threat-protection/audição/event-4624](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624)

Na próxima seção, detectaremos o ataque da força Brute que o atacante fez antes de fazer login.

  

## **7.2 Detecção de força bruta do Windows RDP**

  

Nesta seção, pegaremos um atacante que esteja na fase de movimento lateral. O atacante está tentando saltar para a outra máquina por força bruta sobre RDP.

Arquivo de log de download: Log_File.zip Pass

[Log_File.zip Pass ? 321](https://files-ld.s3.us-east-2.amazonaws.com/Log_File.zip) (https://files-ld.s3.us-east-2.amazonaws.com/Log_File.zip)

Quando uma operação de login malsucedida é feita no RDP, o log "ID do evento 4625 - Uma conta não conseguiu fazer logon". Se seguirmos este registo, podemos localizar o atacante.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-11.png)

Após a filtragem, vemos 4 logs com 4625 IDs de eventos.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-12.png)

Quando olhamos para as datas, vemos que os troncos são formados um após o outro. Quando olhamos para os detalhes, é visto que todos os logs são criados para o usuário "LetsDefendTest".

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-13.png)

Como resultado, entendemos que o invasor tentou, sem sucesso, fazer o login 4 vezes. Para entender se o ataque foi bem-sucedido ou não, podemos procurar os 4624 logs que vimos na seção anterior.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-14.png)

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-15.png)

Como pode ser visto a partir dos resultados, o invasor conseguiu se conectar ao sistema com o log 4624 após os 4625 logs.