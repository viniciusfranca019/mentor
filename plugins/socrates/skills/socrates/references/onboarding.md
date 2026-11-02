# Onboarding

Primeiro contato do aluno com o Socrates. Ele sai sabendo qual curso vai fazer, como usar o
Socrates no dia a dia e como trocar de curso depois, com o diagnóstico feito e o
`~/.socrates` criado.

**Mostre o que existe antes de explicar como funciona.** Ele escolhe primeiro e entende o
método quando for usar: as quatro fases da lição são explicadas na primeira lição, não
aqui. Conduza em blocos curtos e espere a resposta dele entre um bloco e outro.

Antes de tudo, veja se `~/.socrates/perfil.md` existe:

| Situação | Caminho |
|----------|---------|
| Não existe | Primeira vez: blocos 1 a 5, em ordem |
| Existe | Ele está voltando: vá para **Revisão**, no fim deste arquivo |

## Bloco 1 — Os cursos

A primeira mensagem tem só isto, nesta ordem:

1. **O que é o Socrates, em até 3 linhas.** Um mentor dentro do Claude Code que conduz um
   curso lição a lição: pergunta em vez de dar a resposta, ele constrói com a IA e explica
   o que construiu.
2. **O catálogo.** Leia `<raiz>/skills/socrates/catalogo.md` e mostre a tabela: curso, para
   quem é, aonde chega, o que já está disponível e se está **instalado** nesta máquina (a
   skill `socrates-<curso>:curso` aparece entre as skills da sessão).
3. **Uma frase sobre como os cursos chegam:** o Socrates é o mentor, e cada curso é um
   plugin à parte que ele conduz. Instalar um curso é um comando só. Não mostre as
   Extensões aqui: elas aparecem no bloco 2.
4. **Uma pergunta:** qual curso ele quer fazer. Com um curso só no catálogo, pergunte se é
   esse.

Se o curso escolhido não está instalado, a resposta seguinte é só esta: o comando da
coluna "Instalar" do catálogo, para ele rodar no Claude Code, depois `/reload-plugins` e
`/socrates:onboarding` de novo, que agora mostra o curso instalado. Não
siga sem o curso: a trilha e o diagnóstico vêm dele.

Nada de fases da lição, comandos ou histórico nesta mensagem: cada coisa aparece quando
ele precisa dela.

## Bloco 2 — A trilha e o caminho

Escolhido o curso, responda numa **mensagem só**, sem parar no meio para perguntar:

1. **A trilha.** Carregue a skill `socrates-<curso>:curso`, leia o `curso.md` da raiz que
   ela indica e liste as fases: o nome de cada uma e o que
   ele vai saber ao fim dela, em uma linha cada, sem a lista de lições.
2. **O caminho.** Como o Socrates entra na rotina dele:

| Quando | O que fazer |
|--------|-------------|
| **Hoje, uma vez** | Diagnóstico e ritmo, uns 20 minutos. É o que vem agora |
| **Cada dia de estudo** | `/socrates:mentor-mode`: retoma exatamente de onde ele parou |
| **Fim do dia** | `/socrates:feedback`: avalia o dia e diz o que revisar |
| **Plano de carreira, quando quiser** | O PDI é uma extensão do Socrates: monta o plano de desenvolvimento dele com a mesma escala de níveis, e liga as ações aos módulos dos cursos. Mostre a linha da seção Extensões do catálogo, com o comando de instalar, ou `/socrates-pdi:pdi` se a skill `socrates-pdi:pdi` já está instalada |
| **Outro curso, quando quiser** | `/socrates:onboarding`: mostra o catálogo com a situação de cada curso. Um curso novo é um plugin: instala com o comando do catálogo. Trocar de curso não apaga o progresso do outro |

Logo abaixo, o acordo em duas linhas: ele usa o Claude para escrever o código, mas antes
diz o que quer construir, e depois explica o que recebeu.

Avise que digitando `/socrates` o menu mostra os três comandos, e que no feedback o
prefixo importa: o `/feedback` sem `socrates:` é o comando do Claude Code para mandar
feedback à Anthropic. O histórico dele fica em `~/.socrates`, para abrir quando quiser.

Feche com: "Alguma dúvida? Se não, começo o diagnóstico."

## Bloco 3 — Diagnóstico

O diagnóstico mede o nível dele **em cada eixo do curso**, com as escadas da seção "Eixos
e diagnóstico" do `curso.md` e as regras de `<raiz>/skills/socrates/references/niveis.md`.
Avise antes: "Não é prova, não tem nota. É para eu saber de onde você parte em cada
assunto."

- Uma pergunta por vez, duas por eixo: a **M** e, conforme a resposta, a **D** ou a **R**.
- Não corrija as respostas agora. Agradeça e siga. O diagnóstico mede o ponto de partida,
  não ensina.
- Ao final, mostre a tabela do resultado: eixo, nível, a próxima camada que falta e o que
  isso muda na trilha dele. Se ele contestar um nível, siga a seção Contestação de
  `niveis.md`.

## Bloco 4 — Objetivo e ritmo

Uma pergunta por vez, na ordem, esperando a resposta entre elas.

1. Como ele quer ser chamado. Vai para o `perfil.md`.
2. "Por que você quer fazer esse curso? Onde quer estar daqui a um ano?" Anote com as
   palavras dele: o feedback vai lembrar ele disso nos dias difíceis.
3. Combine o ritmo: quais dias, quanto tempo por sessão. Recomende pelo menos 3 sessões
   de 1 hora por semana. Constância vale mais que maratona.
4. Pergunte qual máquina ele usa (Windows, Linux, macOS). O módulo 00 do curso depende
   disso.

## Bloco 5 — Criar o estado e fechar

1. Crie `~/.socrates/perfil.md` a partir do template, com tudo o que foi combinado.
2. Crie `~/.socrates/<curso>/progresso.md` a partir do template, com a trilha copiada do
   `curso.md`, o "Onde parei" na primeira lição e a seção "Níveis por eixo" preenchida
   com o resultado do diagnóstico.
3. Crie o diário do dia com uma seção "Onboarding" que registra o diagnóstico: cada
   pergunta, a resposta resumida, a camada que ela pedia e as camadas que a resposta
   demonstrou.
4. Mostre a ele os caminhos criados e feche: "Quando quiser começar, é só `/socrates:mentor-mode`."

## Revisão — quando o perfil já existe

Ele voltou ao onboarding para ver os cursos, trocar de curso ou mudar o ritmo.

1. **Os cursos, com a situação dele.** Mostre o catálogo com uma coluna a mais, lida de
   `~/.socrates/perfil.md` e de cada `~/.socrates/<curso>/progresso.md`:

   | Situação | Quando |
   |----------|--------|
   | **ativo**, em `<lição>` | É o curso ativo do perfil |
   | **iniciado**, parado em `<lição>` | Tem diretório em `~/.socrates`, mas não é o ativo |
   | **não iniciado** | Não tem diretório em `~/.socrates`, mas o plugin está instalado |
   | **não instalado** | O plugin do curso não está instalado (não há a skill `socrates-<curso>:curso`) |

   Um curso iniciado cujo plugin foi desinstalado aparece como **iniciado**, com a nota
   "reinstale para continuar": o progresso dele em `~/.socrates` continua lá.

2. **Uma pergunta, com quatro opções:** continuar no curso ativo, voltar para um curso
   iniciado, começar um curso novo, ou ajustar o ritmo. Abaixo das opções, uma linha com
   as Extensões do catálogo e a situação de cada uma (instalada ou o comando de instalar).

| Opção | O que fazer |
|-------|-------------|
| Continuar | Sugira `/socrates:mentor-mode` e encerre |
| Voltar para um curso iniciado | Troque o curso ativo no `perfil.md` e a coluna "Situação" da tabela "Cursos" dos dois cursos (`em andamento` e `pausado`). O progresso dele está intacto |
| Começar um curso novo | Se o curso não está instalado, dê o comando de instalar e pare, como no bloco 1. Instalado: faça só o bloco 3 com o diagnóstico desse curso, crie `~/.socrates/<curso>/` como no bloco 5 (passos 2 e 3), troque o curso ativo, acrescente o curso à tabela "Cursos" do perfil (o anterior passa a `pausado`) e pergunte se o ritmo continua o mesmo. Não refaça objetivo nem máquina, e não toque no diretório do outro curso |
| Ajustar o ritmo | Refaça o passo 3 do bloco 4 e atualize o `perfil.md` |
