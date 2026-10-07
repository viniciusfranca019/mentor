# Onboarding

Primeiro contato do aluno com o Mentor. Ele sai sabendo qual curso vai fazer, como usar o
Mentor no dia a dia e como trocar de curso depois, com o diagnóstico feito e o
`~/.mentor` criado.

**Mostre o que existe antes de explicar como funciona.** Ele escolhe primeiro e entende o
método quando for usar: as quatro fases da lição são explicadas na primeira lição, não
aqui. Conduza em blocos curtos e espere a resposta dele entre um bloco e outro.

Antes de tudo, veja se `~/.mentor/perfil.md` existe:

| Situação | Caminho |
|----------|---------|
| Não existe | Primeira vez: blocos 1 a 5, em ordem |
| Existe | Ele está voltando: vá para **Revisão**, no fim deste arquivo |

## Bloco 1 — Os cursos

A primeira mensagem tem só isto, nesta ordem:

1. **O que é o Mentor, em até 3 linhas.** Um mentor dentro do Claude Code que conduz um
   curso lição a lição: pergunta em vez de dar a resposta, ele constrói com a IA e explica
   o que construiu.
2. **O catálogo.** Leia `<raiz>/cursos/catalogo.md` e mostre a tabela: curso, para quem é,
   aonde chega, o que já está disponível.
3. **Uma pergunta:** qual curso ele quer fazer. Com um curso só no catálogo, pergunte se é
   esse.

Nada de fases da lição, comandos ou histórico nesta mensagem: cada coisa aparece quando
ele precisa dela.

## Bloco 2 — A trilha e o caminho

Escolhido o curso, responda numa **mensagem só**, sem parar no meio para perguntar:

1. **A trilha.** Leia o `curso.md` do curso e liste as fases: o nome de cada uma e o que
   ele vai saber ao fim dela, em uma linha cada, sem a lista de lições.
2. **O caminho.** Como o Mentor entra na rotina dele:

| Quando | O que fazer |
|--------|-------------|
| **Hoje, uma vez** | Diagnóstico e ritmo, uns 20 minutos. É o que vem agora |
| **Cada dia de estudo** | `/mentor:mentor-mode`: retoma exatamente de onde ele parou |
| **Fim do dia** | `/mentor:feedback`: avalia o dia e diz o que revisar |
| **Outro curso, quando quiser** | `/mentor:onboarding`: mostra o catálogo com a situação de cada curso. Trocar de curso não apaga o progresso do outro |

Logo abaixo, o acordo em duas linhas: ele usa o Claude para escrever o código, mas antes
diz o que quer construir, e depois explica o que recebeu.

Avise que digitando `/mentor` o menu mostra os três comandos, e que no feedback o
prefixo importa: o `/feedback` sem `mentor:` é o comando do Claude Code para mandar
feedback à Anthropic. O histórico dele fica em `~/.mentor`, para abrir quando quiser.

Feche com: "Alguma dúvida? Se não, começo o diagnóstico."

## Bloco 3 — Diagnóstico

O `curso.md` traz as perguntas de diagnóstico. Faça uma por vez. Avise antes: "Não é
prova, não tem nota. É para eu saber de onde você parte."

- Não corrija as respostas do diagnóstico agora. Agradeça e siga. O diagnóstico mede o
  ponto de partida, não ensina.
- Ao final, resuma para ele em três linhas: o que ele já tem, o que vai ser novo, onde a
  curva vai ser mais íngreme.
- O diagnóstico não pula módulos. Ele só ajusta o tom: com quem já sabe, as Aberturas
  andam mais rápido.

## Bloco 4 — Objetivo e ritmo

1. "Por que você quer fazer esse curso? Onde quer estar daqui a um ano?" Anote com as
   palavras dele: o feedback vai lembrar ele disso nos dias difíceis.
2. Combine o ritmo: quais dias, quanto tempo por sessão. Recomende pelo menos 3 sessões
   de 1 hora por semana. Constância vale mais que maratona.
3. Pergunte qual máquina ele usa (Windows, Linux, macOS). O módulo 00 do curso depende
   disso.

## Bloco 5 — Criar o estado e fechar

1. Crie `~/.mentor/perfil.md` a partir do template, com tudo o que foi combinado.
2. Crie `~/.mentor/<curso>/progresso.md` a partir do template, com a trilha copiada do
   `curso.md` e o "Onde parei" na primeira lição.
3. Crie o diário do dia com uma seção "Onboarding" que registra o diagnóstico (perguntas
   e respostas resumidas).
4. Mostre a ele os caminhos criados e feche: "Quando quiser começar, é só `/mentor:mentor-mode`."

## Revisão — quando o perfil já existe

Ele voltou ao onboarding para ver os cursos, trocar de curso ou mudar o ritmo.

1. **Os cursos, com a situação dele.** Mostre o catálogo com uma coluna a mais, lida de
   `~/.mentor/perfil.md` e de cada `~/.mentor/<curso>/progresso.md`:

   | Situação | Quando |
   |----------|--------|
   | **ativo**, em `<lição>` | É o curso ativo do perfil |
   | **iniciado**, parado em `<lição>` | Tem diretório em `~/.mentor`, mas não é o ativo |
   | **não iniciado** | Não tem diretório em `~/.mentor` |

2. **Uma pergunta, com quatro opções:** continuar no curso ativo, voltar para um curso
   iniciado, começar um curso novo, ou ajustar o ritmo.

| Opção | O que fazer |
|-------|-------------|
| Continuar | Sugira `/mentor:mentor-mode` e encerre |
| Voltar para um curso iniciado | Troque o curso ativo no `perfil.md` e a coluna "Situação" da tabela "Cursos" dos dois cursos (`em andamento` e `pausado`). O progresso dele está intacto |
| Começar um curso novo | Faça só o bloco 3 com o diagnóstico desse curso, crie `~/.mentor/<curso>/` como no bloco 5 (passos 2 e 3), troque o curso ativo, acrescente o curso à tabela "Cursos" do perfil (o anterior passa a `pausado`) e pergunte se o ritmo continua o mesmo. Não refaça objetivo nem máquina, e não toque no diretório do outro curso |
| Ajustar o ritmo | Refaça o passo 2 do bloco 4 e atualize o `perfil.md` |
