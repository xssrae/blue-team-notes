---
tags:
  - SECURITY-OPERATIONS
  - LetsDefend
---
Senhas simples usadas no servidor com um ataque de força bruta SSH podem ser facilmente encontradas pelos invasores. Se tais ataques falharem, o invasor tentará apenas um certo número de senhas com falha. Se for bem-sucedida, a senha é inserida com sucesso após um certo número de tentativas de login malsucedidas.

Em um exemplo de análise de força bruta SSH, quando visualizamos um log da máquina linux com o conteúdo do arquivo “/var/log/auth.log.1” e tentativas de login com falha, podemos ver a quem pertencem as tentativas de login com falha.

  
```shell
cat auth.log.1 | grep "Failed password" | cut -d " -f10 | sort | sort | uniq -c | sort
```

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-6-1024x208.png)

Um comando como o abaixo pode ser usado para localizar os endereços IP que fizeram essas tentativas.

```shell
cat auth.log.1 | grep "Failed password" | cut -d "" -f12 | sort | uniq -c | sort
```

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-7-1024x170.png)

Os usuários que fizer login com sucesso também podem ser detectados com o seguinte comando.

```shell
cat auth.log.1 | grep "Accepted password"
```

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-8-1024x223.png)

Como pode ser visto aqui, tentativas de login bem-sucedidas são vistas com dois usuários diferentes de dois endereços IP diferentes.

Quando as tentativas de login falhadas anteriores são comparadas, é visto que o usuário "analista" não teve uma tentativa de login malsucedida antes do endereço IP que ele fez login com sucesso. No entanto, é claramente visto que muitas tentativas malsucedidas foram feitas com o usuário "letsdefend" no endereço IP de 188.58.65.203. Isso nos mostra que o invasor fez login com sucesso com o usuário letsdefend durante a força bruta.

![](https://ld-images-2.s3.us-east-2.amazonaws.com/Detecting+Brute+Force+Attacks/images/image-9-1024x317.png)

Como visto acima, usuários registrados bem-sucedidos e malsucedidos podem ser facilmente encontrados com comandos básicos do Linux. Quando esses dois resultados são examinados em detalhes, vê-se que há uma entrada bem-sucedida após muitas tentativas frustradas pelo usuário letsdefend do endereço IP 188.58.65.203.3.