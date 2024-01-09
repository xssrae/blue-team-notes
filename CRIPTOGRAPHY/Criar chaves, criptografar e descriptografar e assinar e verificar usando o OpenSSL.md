---
tags:
  - CRIPTOGRAPHY
---
# Gerar chaves

Antes de criptografar ou descriptografar qualquer item, você precisa de uma chave privada e uma pública. Então vamos criá-las primeiro.
### **Chave privada**
Um par de chaves consiste em uma chave pública que você pode divulgar e uma chave privada que precisa ser mantida em segredo. Psiu. :) Quando alguém quiser enviar dados e garantir que ninguém os veja, eles podem ser criptografados com sua chave pública. Os dados criptografados com essa chave só podem ser descriptografados com sua chave privada. Assim só você consegue ver os dados originais. Por isso é tão importante manter as chaves privadas em segredo. Se alguém tiver uma cópia dela, poderá descriptografar os dados enviados a você. Isso não é nada bom!

Primeiro vamos gerar e analisar uma chave RSA privada de 2.048 bits. Para gerar a chave, insira este comando no terminal:

```shell
openssl genrsa -out private_key.pem 2048
```

Esse comando cria uma chave RSA de 2.048 bits chamada "private_key.pem". O nome da chave é informado depois da sinalização "-out" e geralmente termina em ".pem". O número de bits é indicado no último argumento.
### **Chave pública**
Use a chave privada para gerar a chave pública e depois faça a verificação dela. Agora que você tem uma chave privada, você precisa gerar a chave pública correspondente. Você pode dar essa chave para qualquer pessoa que quiser enviar dados criptografados a você. Quando os dados são criptografados com sua chave pública, eles só podem ser descriptografados por alguém com sua chave privada. Para criar uma chave pública com base em uma chave privada, insira o comando a seguir. Você vai ver esta resposta:

```shell
openssl rsa -in private_key.pem -outform PEM -pubout -out public_key.pem
```

# Criptografar e Descriptografar

Vamos simular que um arquivo foi criptografado com sua chave pública e enviado para você, a única pessoa que consegue descriptografar com a chave privada. Da mesma forma, é possível criptografar arquivos com as chaves públicas de outras pessoas, sabendo que eles só poderão ser descriptografados por elas.

Crie um arquivo de texto com informações que você quer proteger pela criptografia. Depois criptografe e inspecione o arquivo. Para começar, insira o comando abaixo. Ele vai criar um novo arquivo chamado "secret.txt", que contém apenas o texto "This is a secret message, for authorized parties only" ("Esta é uma mensagem secreta somente para pessoas autorizadas"). Você pode mudar essa mensagem se quiser.

```shell
echo 'This is a secret message, for authorized parties only' > secret.txt
```

Depois, para criptografar o arquivo usando sua chave pública, insira este comando:

```shell
openssl rsautl -encrypt -pubin -inkey public_key.pem -in secret.txt -out secret.enc
```

Será criado o arquivo "secret.enc", que é uma versão criptografada do "secret.txt". Se você tentar ver o conteúdo do arquivo criptografado, notará que a saída está distorcida. Isso é completamente normal para mensagens criptografadas. A ideia é que o conteúdo não seja exibido.

Veja um exemplo de como o arquivo criptografado "secret.enc" aparece no editor nano usando o comando abaixo:

```shell
nano ~/secret.enc
```

O arquivo criptografado está pronto e pode ser enviado para quem tiver a chave privada correspondente. Como neste caso é você, descriptografe o arquivo e recupere o conteúdo original. A chave privada precisa ser usada para descriptografar a mensagem, já que ela foi criptografada com a chave pública. Use o comando a seguir para descriptografar o arquivo:

```shell
openssl rsautl -decrypt -inkey private_key.pem -in secret.enc
```

# Gerar um resumo de hash
Agora você vai criar um resumo de hash da mensagem e gerar uma assinatura digital correspondente. Em seguida, você vai verificar a assinatura do resumo. Assim poderá confirmar que a mensagem não foi alterada nem falsificada. Se a mensagem tiver sido modificada, os hashes dela e da assinatura serão diferentes e ocorrerá uma falha na verificação.

Para criar um resumo de hash da mensagem, insira este comando:

```shell
openssl dgst -sha256 -sign private_key.pem -out secret.txt.sha256 secret.txt
```

Esse comando usa a chave privada para gerar o arquivo "secret.txt.sha256", que contém o resumo de hash do arquivo de texto secreto.

Com esse arquivo, qualquer pessoa pode usar a chave pública e o resumo de hash para verificar se o arquivo não foi modificado desde a criação dele e a geração do hash. Para fazer a verificação, insira este comando:

```shell
openssl dgst -sha256 -verify public_key.pem -signature secret.txt.sha256 secret.txt
```


