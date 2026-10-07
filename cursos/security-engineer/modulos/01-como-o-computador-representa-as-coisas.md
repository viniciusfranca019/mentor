# Módulo 01 — Como o computador representa as coisas

**Objetivo:** entender que tudo dentro do computador (número, texto, imagem, programa) é
uma sequência de bytes, e que o significado depende de quem interpreta.

**Pré-requisitos:** módulo 00 (laboratório funcionando).

**Por que importa para o curso:** quase todo ataque explora uma diferença de
interpretação. O atacante manda bytes que um lado lê como dado e o outro executa como
comando, ou que a validação lê como imagem e o servidor executa como script. Quem vê os
bytes por trás do significado enxerga essas brechas.

---

## Lição 1.1 — Tudo é número: bits, bytes e hexadecimal

**Conceito-âncora:** o computador guarda só bits (0 e 1), agrupados em bytes de 8 bits,
que valem de 0 a 255. Hexadecimal é só uma forma compacta de escrever bytes: dois dígitos
hex são um byte.

### Abertura

1. Se o computador só entende 0 e 1, como ele guarda o número 200?
   - Uma boa resposta contém: alguma ideia de combinação de 0s e 1s em posições, cada
     posição com um peso. Não precisa fazer a conta.
2. Com 8 interruptores (ligado ou desligado), quantas combinações diferentes você
   consegue fazer?
   - Uma boa resposta contém: 256 (2⁸), ou o raciocínio de dobrar a cada interruptor.
     Se ele chegar a "muitas", suba a escada até ele achar o 256.
3. Por que você acha que programadores escrevem `FF` em vez de `11111111`?
   - Uma boa resposta contém: é mais curto e mais fácil de ler. Cada dígito hex
     representa 4 bits.

### Missão

Com o Claude, ele constrói um conversor em Python: recebe um número de 0 a 255 e mostra
o número em decimal, binário (8 dígitos) e hexadecimal (2 dígitos).

Perguntas de especificação:
1. O que o programa faz se receber 300? E −1? E "abc"?
   - Uma boa resposta contém: uma decisão explícita para entradas fora do intervalo,
     como recusar com uma mensagem.
2. Como a saída deve aparecer na tela?
   - Uma boa resposta contém: um exemplo concreto da saída, como
     `200 = 11001000 = C8`.
3. Que números você vai usar para testar, e por que esses?
   - Uma boa resposta contém: casos de borda, como 0, 255 e um do meio. Se ele escolher
     só números "normais", pergunte o que acontece nas pontas.

### Verificação

1. Antes de rodar: qual é o binário de 255? E o de 128? Depois confira no programa.
   - Uma boa resposta contém: `11111111` e `10000000`, ou um raciocínio certo mesmo com
     erro de conta.
2. Por que 255 é o maior número que cabe num byte?
   - Uma boa resposta contém: são 8 bits, todos ligados; 256 combinações, contando a
     partir do zero.
3. O que acontece com 255 + 1 se o resultado tiver que caber num byte? Pergunte ao
   Claude como testar isso em Python e explique o resultado.
   - Uma boa resposta contém: o valor "dá a volta" para 0 (overflow). Python não limita
     inteiros, então o teste precisa forçar um byte, por exemplo com `% 256` ou
     `bytes([256])`, que dá erro. Ele precisa explicar a diferença entre os dois.

### Ferramenta

A calculadora do sistema no modo programador, e o comando `printf '%x\n' 200` no shell.
Pergunta: "Agora que você fez o conversor, o que a calculadora no modo programador faz
que o seu programa também faz?"

### Explicar de volta

"Explique o que é um byte e por que hexadecimal existe." Critério: 8 bits, valores de 0
a 255, e hex como forma compacta, com dois dígitos por byte.

### Para o Mentor

- **Erros comuns:** achar que hexadecimal é "outro tipo de dado". É só outra forma de
  escrever o mesmo número. Pergunte: "C8 e 200 são números diferentes?"
- **Ponte para segurança:** overflow de inteiro já causou vulnerabilidades reais; dumps
  de memória, hashes e chaves são lidos em hex (módulos 2.2 e 24).

---

## Lição 1.2 — Texto também é número: codificação

**Conceito-âncora:** texto é guardado como números, por uma tabela de codificação
(ASCII, UTF-8). O mesmo byte pode virar letras diferentes conforme a tabela que se usa
para ler.

### Abertura

1. Se tudo é número, como o computador guarda a letra "A"?
   - Uma boa resposta contém: alguma ideia de uma tabela que liga cada letra a um
     número.
2. Você já viu um texto com "Ã§" no lugar de "ç"? O que você acha que aconteceu?
   - Uma boa resposta contém: o texto foi gravado de um jeito e lido de outro. Não
     precisa usar a palavra "codificação".

### Missão

Ele constrói com o Claude um programa que recebe uma palavra e mostra, para cada
caractere, o caractere e os bytes que o representam em UTF-8, em hex.

Perguntas de especificação:
1. Qual palavra de teste você vai usar, e por que ela?
   - Uma boa resposta contém: uma palavra com acento ou "ç". Se ele escolher só letras
     sem acento, pergunte o que acontece com "ação".
2. Em que formato a saída mostra cada caractere?
   - Uma boa resposta contém: um exemplo, como `ç -> C3 A7`.

### Verificação

1. Antes de rodar com "ação": quantos bytes você prevê? Rode e compare.
   - Uma boa resposta contém: uma previsão; depois, a observação de que letras com
     acento ocupam 2 bytes em UTF-8, então são 6 bytes para 4 caracteres.
2. Peça ao Claude para ler os bytes de "ação" como se fossem Latin-1 (outra tabela). O
   que aparece, e por quê?
   - Uma boa resposta contém: "aÃ§Ã£o", porque cada byte foi lido como um caractere
     separado na outra tabela. É a explicação do "Ã§" da Abertura.
3. Uma senha "ação" digitada num sistema UTF-8 e verificada num sistema Latin-1 é a
   mesma senha?
   - Uma boa resposta contém: não; os bytes comparados são diferentes. Ou ele percebe
     que depende de como cada lado converte, o que já é uma boa intuição.

### Ferramenta

O comando `xxd` (ou `hexdump -C`): `echo -n "ação" | xxd`. Pergunta: "O que o `xxd`
mostrou que o seu programa também mostra?"

### Explicar de volta

"Explique por que às vezes aparece 'Ã§' no lugar de 'ç'." Critério: texto vira bytes
por uma tabela; gravar com uma tabela e ler com outra troca os caracteres.

### Para o Mentor

- **Erros comuns:** achar que um caractere é sempre um byte. A pergunta 1 da
  Verificação desfaz isso.
- **Ponte para segurança:** codificações diferentes são usadas para burlar filtros (um
  filtro procura `<script>` e o atacante manda o mesmo texto codificado de outro jeito).
  Volta em injeção (26) e XSS (28.2).

---

## Lição 1.3 — Arquivos e formatos: a extensão mente

**Conceito-âncora:** um arquivo é só uma sequência de bytes. O que diz o tipo de verdade
são os primeiros bytes (a assinatura, ou *magic bytes*); a extensão no nome é só uma
etiqueta que qualquer um pode trocar.

### Abertura

1. Se você renomear `foto.png` para `foto.txt`, a imagem vira texto?
   - Uma boa resposta contém: não, só o nome mudou; o conteúdo continua igual.
2. Então como um programa pode saber que um arquivo é uma imagem, sem olhar o nome?
   - Uma boa resposta contém: olhando o conteúdo. Se ele chegar em "algo no começo do
     arquivo", ótimo.

### Missão

Ele constrói com o Claude um mini identificador de arquivos: lê os primeiros bytes de um
arquivo, mostra esses bytes em hex e diz se o arquivo é PNG, PDF, ZIP ou "desconhecido",
comparando com as assinaturas.

Perguntas de especificação:
1. Quantos bytes do início você vai ler, e por quê?
   - Uma boa resposta contém: um número justificado, como "8, porque a assinatura do PNG
     tem 8 bytes". Ele pode pedir ao Claude as assinaturas, mas precisa decidir quantos
     bytes ler.
2. O que o programa faz com um arquivo vazio ou que não existe?
   - Uma boa resposta contém: uma decisão explícita.
3. Que arquivos você vai usar para testar?
   - Uma boa resposta contém: um de cada tipo, mais um com a extensão trocada.

### Verificação

1. Renomeie um PNG para `.pdf` e rode o identificador. O que você prevê?
   - Uma boa resposta contém: o programa diz PNG, porque olha os bytes e não o nome.
2. Agora crie um arquivo de texto que comece com os bytes da assinatura do PNG e tenha
   qualquer coisa depois. O que o identificador diz? Ele está certo?
   - Uma boa resposta contém: diz PNG e está errado; a assinatura também pode ser
     falsificada. Os primeiros bytes são um indício, não uma prova.
3. Um site aceita upload de "apenas imagens" e verifica só a extensão. O que um atacante
   faz?
   - Uma boa resposta contém: manda um arquivo perigoso (um script, por exemplo) com
     extensão de imagem. Melhor ainda se ele disser que verificar só os magic bytes
     também não basta.

### Ferramenta

O comando `file`: `file foto.png`. Pergunta: "O `file` olha o nome ou os bytes? Como
você testaria isso?" Ele testa com o arquivo renomeado.

### Explicar de volta

"Explique por que confiar na extensão de um arquivo é perigoso." Critério: a extensão é
só nome e pode ser trocada; o tipo está nos bytes; e mesmo os bytes podem ser forjados.

### Para o Mentor

- **Erros comuns:** concluir que os magic bytes resolvem tudo. A pergunta 2 da
  Verificação existe para desfazer isso.
- **Ponte para segurança:** validação de upload, arquivos poliglotas (válidos em dois
  formatos ao mesmo tempo), anexos de phishing. Volta em segurança de aplicações (Fase 6).

---

## Lição 1.4 — Do código ao programa: compilado e interpretado

**Conceito-âncora:** o processador só executa instruções de máquina (bytes). Um
compilador traduz o código-fonte para essas instruções antes de rodar; um interpretador
lê o código e executa enquanto lê. Nos dois casos, o que roda é o que o processador
recebe, não o que está escrito no código-fonte.

### Abertura

1. Você escreveu `print("oi")` em Python. O processador entende essa linha?
   - Uma boa resposta contém: não diretamente; alguém traduz para algo que o processador
     entende.
2. Qual a diferença entre um tradutor que traduz um livro inteiro antes e um intérprete
   que traduz uma conversa ao vivo?
   - Uma boa resposta contém: um faz tudo antes e entrega pronto; o outro traduz
     enquanto acontece. É a analogia de compilado e interpretado.

### Missão

Ele escreve com o Claude o mesmo programa pequeno em duas linguagens, C e Python (somar
dois números e mostrar o resultado). Compila o de C com `gcc` e roda os dois.

Perguntas de especificação:
1. Os dois programas precisam fazer exatamente o quê, para a comparação valer?
   - Uma boa resposta contém: o mesmo comportamento, com a mesma entrada e a mesma
     saída.
2. Depois de compilar o C, quais arquivos você espera que existam na pasta?
   - Uma boa resposta contém: o fonte `.c` e um executável novo.

### Verificação

1. Abra o executável do C com `xxd | head`. O que você vê? Dá para ler o código-fonte
   ali?
   - Uma boa resposta contém: bytes, a maioria ilegível, talvez alguns textos soltos; o
     código-fonte não está lá. Se ele notar `ELF` no início, ligue com os magic bytes da
     lição 1.3.
2. Apague o `.c` e rode o executável. Funciona? E se apagar o `.py`, o programa Python
   roda?
   - Uma boa resposta contém: o executável roda sem o fonte; o Python precisa do `.py`
     e do interpretador.
3. Se alguém te manda só um executável, como você sabe o que ele faz?
   - Uma boa resposta contém: não dá para saber só olhando o nome; seria preciso
     analisar os bytes ou executar num ambiente isolado. Ligue com o laboratório do
     módulo 00.

### Ferramenta

O comando `strings` (mostra os textos legíveis dentro de um binário) e o `file` no
executável. Pergunta: "O que o `strings` te conta sobre um executável desconhecido, e o
que ele não conta?"

### Explicar de volta

"Explique a diferença entre compilado e interpretado, e por que receber um executável
desconhecido é arriscado." Critério: compilado é traduzido antes e roda sem o fonte;
interpretado precisa do fonte e do interpretador; um executável não mostra o que faz.

### Para o Mentor

- **Erros comuns:** achar que Python "não é compilado de jeito nenhum" (ele gera
  bytecode, o `.pyc`). Só aprofunde se ele perguntar; o conceito-âncora não depende disso.
- **Ponte para segurança:** análise de malware, `strings` como primeira triagem,
  supply chain (o binário que você baixou é o mesmo que foi compilado do fonte?). Volta
  em 30 (supply chain) e 39.3 (modelos e plugins).
