# Módulo 00 — Seu laboratório

**Objetivo:** ter um Linux isolado para estudar e saber por que ele precisa ser isolado.

**Pré-requisitos:** nenhum. Claude Code instalado e o onboarding feito.

**Por que importa para o curso:** segurança se aprende quebrando coisas. Quebrar coisas
na máquina onde está o seu banco, o seu e-mail e o seu trabalho é o primeiro erro de
segurança que dá para cometer. O laboratório é o primeiro controle de segurança do curso.

---

## Lição 0.1 — O que é um ambiente de estudo isolado

**Conceito-âncora:** um laboratório é um ambiente separado da máquina principal, onde
um erro ou um código malicioso não alcança o que importa. Isolar é limitar o estrago
possível.

### Abertura

1. Imagine que você baixa da internet um programa que promete "testar a segurança da
   sua rede", e ele é malicioso. O que ele consegue alcançar se você rodar no seu
   computador do dia a dia?
   - Uma boa resposta contém: os arquivos do usuário, senhas salvas no navegador, sessões
     abertas, outras máquinas da rede de casa. Basta citar dois.
2. Por que um médico que estuda vírus perigosos não faz isso na cozinha de casa?
   - Uma boa resposta contém: o estrago escapa do lugar onde ele estava contido; o
     laboratório tem barreiras que limitam o alcance.
3. Que tipo de "parede" você imagina que dá para criar dentro de um computador?
   - Uma boa resposta contém: qualquer ideia de separação, como outro usuário, outra
     máquina, máquina virtual ou container. Não precisa ser precisa: é uma pergunta de
     curiosidade.

### Missão

Sem código nesta lição. Com o Claude, ele faz um inventário: o que existe hoje na
máquina dele que um programa malicioso poderia alcançar. Ele dirige a investigação: decide
onde olhar e pede ao Claude os comandos para olhar.

Perguntas de especificação:
1. Quais categorias de coisas valiosas você vai procurar?
   - Uma boa resposta contém: pelo menos três categorias, como documentos, credenciais e
     sessões, chaves SSH ou tokens, dispositivos na rede.
2. Como você vai saber que o inventário está bom o suficiente?
   - Uma boa resposta contém: um critério de parada, como "uma lista com o que existe e
     onde fica, para cada categoria".

### Verificação

1. Do inventário, qual item seria o pior de vazar e por quê?
   - Uma boa resposta contém: um item concreto e o impacto: o que alguém faria com ele.
2. Se o laboratório for uma máquina virtual dentro deste mesmo computador, o que ainda
   estaria compartilhado entre os dois?
   - Uma boa resposta contém: o hardware, a rede, e a possibilidade de pastas
     compartilhadas. O isolamento é forte, mas não é absoluto.

### Ferramenta

Apresente as duas opções de laboratório que a lição 0.2 vai montar: **WSL2** (Linux
dentro do Windows, leve, menos isolado) e **VirtualBox** ou similar (máquina virtual
completa, mais pesada, mais isolada). Pergunte: "Pelo que você viu hoje, qual delas
isola mais, e qual você usaria para rodar um malware de verdade?"

### Explicar de volta

"Explique para um amigo por que você não vai estudar ataques na sua máquina do dia a
dia." Critério: fala em limitar o alcance do estrago e cita pelo menos uma coisa
concreta que ficaria protegida.

### Para o Mentor

- **Erros comuns:** achar que antivírus substitui isolamento; achar que "não tenho nada
  de valor". Desfaça perguntando quais sessões estão logadas no navegador agora.
- **Ponte para segurança:** isolamento e contenção do estrago (*blast radius*) aparecem
  de novo em containers (18), cloud e IAM (20) e agentes de IA com sandbox (38.3).

---

## Lição 0.2 — Montando o Linux (WSL2 ou VM)

**Conceito-âncora:** o laboratório é um sistema operacional inteiro rodando sobre o
seu. Saber em qual dos dois você está e o que passa de um para o outro é a primeira
habilidade de quem trabalha com isolamento.

### Abertura

1. O que é um sistema operacional? Para que ele serve?
   - Uma boa resposta contém: o programa que gerencia o hardware e deixa os outros
     programas usarem CPU, memória, disco e rede sem que cada um precise controlar o
     hardware sozinho.
2. Como podem rodar dois sistemas operacionais ao mesmo tempo no mesmo computador?
   - Uma boa resposta contém: alguma ideia de uma camada que divide o hardware ou finge
     ser um hardware. A palavra "hipervisor" não é necessária.

### Missão

Instalar o laboratório, com o Claude como guia, e provar que ele funciona. No Windows,
a recomendação é o WSL2 com Ubuntu. Se ele já usa Linux, uma VM no VirtualBox. Ele
pede ao Claude os passos, mas precisa entender o que cada comando faz antes de rodar.

Perguntas de especificação:
1. Antes de pedir os passos ao Claude: o que você precisa dizer a ele sobre a sua
   máquina para que os passos sirvam?
   - Uma boa resposta contém: o sistema operacional e a versão, e o que ele quer como
     resultado (qual Linux, para quê).
2. Como você vai provar que o laboratório está funcionando?
   - Uma boa resposta contém: um teste concreto, como abrir o terminal do Linux e rodar
     um comando que mostra o nome do sistema.

Com o laboratório pronto, ele roda dentro dele `uname -a`, `whoami` e `pwd` e explica o
que cada um mostrou.

### Verificação

1. Crie um arquivo dentro do Linux. Você consegue vê-lo do Windows (ou do sistema
   principal)? E o contrário? Antes de testar: o que você prevê?
   - Uma boa resposta contém: uma previsão antes do teste. No WSL2, os dois lados se
     enxergam (`\\wsl$` de um lado e `/mnt/c` do outro). Ele deve concluir que o WSL2
     não é um isolamento forte.
2. Se um programa malicioso rodar dentro do seu WSL2, ele alcança os seus documentos do
   Windows? Por quê?
   - Uma boa resposta contém: sim, pelo `/mnt/c`. Por isso o WSL2 serve para estudar,
     mas não para rodar malware de verdade.

### Ferramenta

O comando `wsl` (ou o painel do VirtualBox): listar, parar e exportar a distribuição.
Pergunta: "Como você voltaria o laboratório a um estado limpo se estragasse tudo?"
Conecta com snapshot, que volta no módulo 17.

### Explicar de volta

"Explique onde o seu Linux está rodando e o que ele compartilha com a sua máquina."
Critério: diz que é um sistema rodando sobre o outro e cita pelo menos um ponto de
contato (arquivos, rede).

### Para o Mentor

- **Erros comuns:** copiar os comandos de instalação sem ler. Se ele colar um comando
  sem explicar, pare e peça a explicação daquele comando. Também é comum confundir o
  terminal do Windows com o do Linux: peça que ele mostre o resultado do `uname`.
- **Ponte para segurança:** a pergunta "o que atravessa a fronteira?" é a mesma de toda
  análise de fronteira de confiança (21.3).

---

## Lição 0.3 — Primeira conversa com o Claude como arquiteto

**Conceito-âncora:** quem especifica decide. Uma especificação completa diz o que
entra, o que sai, o que acontece e como saber que funcionou. O que ela não diz, a IA
decide no lugar dele.

### Abertura

1. Você pede a um pedreiro "faz um muro". O que pode dar errado?
   - Uma boa resposta contém: o pedreiro decide altura, material e lugar; o resultado
     pode não servir para o que ele queria.
2. Quando você pede algo à IA sem detalhes, quem decide o que ficou faltando?
   - Uma boa resposta contém: a IA, por suposição. Ele não fica sabendo do que ela
     decidiu, a não ser que leia o resultado.

### Missão

Ele pede ao Claude um script de até 20 linhas que conte quantos arquivos existem numa
pasta. O Mentor não aceita o primeiro pedido se ele for vago: faz as perguntas de
especificação até o pedido estar completo. Depois, ele lê o script antes de rodar.

Perguntas de especificação:
1. O que o script recebe?
   - Uma boa resposta contém: uma pasta, e como ela é informada (argumento ou pasta
     atual).
2. O que conta como "arquivo"? Pastas entram? E as subpastas?
   - Uma boa resposta contém: uma decisão explícita. Qualquer uma serve, desde que seja
     dele.
3. O que o script mostra no final?
   - Uma boa resposta contém: o formato da saída, por exemplo só o número ou uma frase.
4. Como você vai testar?
   - Uma boa resposta contém: uma pasta com uma quantidade conhecida de arquivos, para
     comparar com o resultado.

### Verificação

1. Aponte no script a linha que faz a contagem. O que ela faz?
   - Uma boa resposta contém: a linha certa e uma explicação aproximada do comando.
2. O que acontece se você passar uma pasta que não existe? Preveja antes de testar.
   - Uma boa resposta contém: uma previsão. Depois do teste, ele conclui se o script
     trata o erro ou não, e se isso estava na especificação.
3. Que decisão o Claude tomou que você não especificou?
   - Uma boa resposta contém: algo real do script, como a linguagem escolhida, arquivos
     ocultos ou mensagem de erro. Esta é a pergunta mais importante da lição.

### Ferramenta

O próprio Claude Code: o modo de planejamento (o Claude propõe um plano antes de
escrever código) e o hábito de pedir "me explique o que você vai fazer antes de fazer".
Pergunta: "Em que tipo de tarefa você pediria o plano antes do código?"

### Explicar de volta

"Explique o que uma boa especificação precisa ter, e o que acontece quando ela não tem."
Critério: cita entrada, saída, comportamento e teste, e diz que o que faltar a IA decide
por ele.

### Para o Mentor

- **Erros comuns:** achar que a IA "sabe o que eu quis dizer". A pergunta 3 da
  Verificação desfaz isso: sempre há uma decisão que ele não tomou.
- **Ponte para segurança:** código gerado por IA com decisões que ninguém revisou é uma
  das fontes de vulnerabilidade da era da IA (14.3, 40.2). Revisar o que a IA decidiu é
  uma tarefa de segurança.
