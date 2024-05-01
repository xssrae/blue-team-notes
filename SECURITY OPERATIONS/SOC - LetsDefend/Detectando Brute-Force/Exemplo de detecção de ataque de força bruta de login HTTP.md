---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
Em ataques de força bruta de login HTTP, o invasor geralmente tenta uma senha com um ataque de dicionário em uma página de login. Para analisar isso, o conteúdo do arquivo de log relevante deve ser aberto com um editor de texto e os logs devem ser examinados.

A imagem a seguir mostra um ataque de força bruta de login HTTP. Ver-se que o usuário encontrou a senha inserindo com sucesso a senha após um certo número de tentativas de login malsucedidas. Aqui, a diferença entre os tamanhos dos pacotes na resposta retornada às tentativas de login fracassadas e os tamanhos dos pacotes na resposta retornadas às tentativas de login bem-sucedidas são claramente vistos.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-10-1024x539.png)