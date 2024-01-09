---
tags:
  - CRIPTOGRAPHY
---
# Introdução
Neste laboratório, você terá lições práticas com demonstrações dos processos de geração e verificação de hashes usando as ferramentas "md5sum" e "shasum".

O _md5sum_ é um programa de geração de hashes que calcula e verifica hashes MD5 de 128 bits. Como acontece com todos os algoritmos de geração de hashes, teoricamente, há um número ilimitado de arquivos com qualquer hash MD5. O "md5sum" é usado para verificar a integridade dos arquivos.

Da mesma forma, o _shasum_ é um programa de criptografia que calcula e verifica hashes SHA. Ele também costuma ser usado para verificar a integridade dos arquivos.

**O que você vai aprender**

- **Calcular**: você vai criar um arquivo de texto e gerar hashes usando as ferramentas "md5sum" e "shasum".
- **Inspecionar**: depois de gerar os resumos de hash, você vai inspecionar os arquivos resultantes.
- **Verificar**: você vai verificar o hash usando as ferramentas "md5sum" e "shasum".
- **Modificar**: você vai modificar o arquivo de texto e comparar esses resultados com o hash original para observar como o resumo muda e identificar as falhas no processo de verificação.
# MD5
Primeiro vamos criar um arquivo de texto com alguns dados. Se você quiser, pode usar seus próprios dados de texto. Este comando cria um arquivo de texto chamado "file.txt" com uma única linha de texto básico:

Você vai ver a seguinte saída (ou algo muito parecido): 

```shell
echo 'This is some text in a file, just so we have some data' > file.txt
```

Agora vamos gerar a soma de MD5 para o arquivo e armazená-la. Para gerar essa soma, digite este comando do "md5sum":

```shell
md5sum file.txt > file.txt.md5
```

Além disso, você pode verificar se o hash está correto e se o arquivo original não foi adulterado após a soma. Para fazer isso, insira este comando e veja a seguinte saída, que indica a validade do hash:

```shell
md5sum -c file.txt.md5
```

# Verificação de um arquivo inválido

Agora, para você ver a segurança desse processo, vamos mostrar como até a alteração de um caractere no arquivo resulta em um hash diferente. Primeiro crie uma cópia do arquivo de texto e insira um único espaço ao final do documento. Use o editor de texto de sua preferência. Incluímos instruções para você fazer essa alteração no editor Nano. Faça uma cópia do arquivo ao digitar este comando:

```shell
cp file.txt badfile.txt
```

Depois gere um novo "md5sum" para o arquivo:

```shell
md5sum badfile.txt > badfile.txt.md5
```

O hash resultante é **idêntico** ao hash do arquivo original "file.txt", apesar da diferença nos nomes. Isso acontece porque, no processo de geração de hashes, só os dados do arquivo são consultados, e não os metadados.

```shell
cat badfile.txt.md5
cat file.txt.md5
```

Após isso, vamos alterar um caractere no texto por meio do `nano`, apenas adicionando um espaço a mais ao final.

Desta vez, ocorrerá uma falha na verificação, mostrando que qualquer mudança resulta em um hash diferente. Insira este comando novamente para verificar:

```shell
md5sum -c badfile.txt.md5
```

Para ver a diferença de hash do arquivo editado, gere um novo hash e faça uma inspeção:

```shell
md5sum badfile.txt > new.badfile.txt.md5

cat new.badfile.txt.md5
```

# SHA1
```shell
shasum file.txt > file.txt.sha1

shasum -c file.txt.sha1
```

# SHA256
```shell
shasum -a 256 file.txt > file.txt.sha256

shasum -c file.txt.sha256
```