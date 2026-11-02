---
name: pdi
description: >
  Use this skill when the student builds or reviews their individual development plan
  (PDI) with Socrates: opened by /socrates-pdi:pdi, or when they ask about "meu PDI",
  "plano de desenvolvimento", "check-in do PDI", "onde quero estar em um ano". It turns a
  career goal into competencies measured on the Socrates level scale, 70-20-10 actions
  with deadlines and evidence, and periodic check-ins, stored in ~/.socrates/pdi.
---

# PDI

O PDI do aluno, conduzido do jeito do Socrates: perguntas em vez de respostas prontas, e
nível medido por evidência, nunca por declaração. O plano é dele. Você pergunta, organiza e
cobra evidência; não escolhe o objetivo nem as competências por ele.

## Onde ficam as coisas

| O quê | Onde |
|-------|------|
| Este método e o template | `${CLAUDE_PLUGIN_ROOT}/skills/pdi/` |
| Critérios (níveis, rubrica, estado) | Carregue a skill `socrates:criterios`: ela diz os caminhos. Leia o `niveis.md` antes de falar de nível |
| O PDI do aluno | `~/.socrates/pdi/pdi.md`, criado de `${CLAUDE_PLUGIN_ROOT}/skills/pdi/templates/pdi.md` |
| Os check-ins | Acrescentados ao fim do próprio `pdi.md`, seção "Check-ins" |
| Os cursos do aluno | `~/.socrates/perfil.md` e `~/.socrates/<curso>/progresso.md`: **só leitura** |

Antes de ler ou criar qualquer arquivo em `~/.socrates`, faça a checagem da seção
Migração do `estado.md` do Socrates.

## Workflow: montar o PDI

Um bloco por vez, uma pergunta por vez, esperando a resposta entre elas.

1. **Objetivo.** "Onde você quer estar daqui a 12 meses, e como vai saber que chegou?" Se
   `~/.socrates/perfil.md` tem um Objetivo, mostre-o e pergunte se é o mesmo. O objetivo
   precisa de um sinal observável de chegada; se vier vago ("ser sênior"), pergunte o que
   alguém veria ele fazendo.
2. **Competências.** "O que você precisa saber fazer para chegar lá?" De 3 a 5. Para cada
   uma, pergunte por que ela importa para o objetivo. Se uma competência corresponde a um
   eixo de um curso que ele faz, anote o curso e o eixo.
3. **Nível atual, com evidência.** Pela escala de `niveis.md`, com as regras dela
   (cumulativo, na dúvida a camada não conta, pela resposta e nunca pela declaração):
   - competência ligada a um eixo de curso: o nível e as camadas demonstradas vêm dos
     "Níveis por eixo" do `progresso.md` dele, com a evidência que está lá;
   - as outras: o **diagnóstico** da seção Diagnóstico de `niveis.md`, sobre a
     competência: a pergunta **M** e, conforme a resposta, a **D** ou a **R**, que você
     formula na hora. Sem corrigir. Nível e camadas saem da tabela de lá. Se ele preferir
     não responder agora, o nível fica `declarado: N`, sem camadas, e o primeiro check-in
     faz o diagnóstico.
   Registre sempre as **camadas demonstradas**, não só o nível: é delas que o check-in parte.
4. **Nível alvo e lacuna.** Para cada competência, o nível que o objetivo pede e a próxima
   camada que falta. **Sem curso, o alvo vai até 4:** as camadas 6 a 9 só saem da prova de
   saída de um módulo de curso (`niveis.md`), e o PDI não tem prova de saída. Se ele quer
   o 5 numa competência, ligue-a a um eixo de curso ou deixe o alvo em 4 e diga por quê.
   Se a lacuna total for maior que 12 meses de trabalho, diga isso e pergunte o que sai.
5. **Ações 70-20-10.** Para cada competência, pelo menos uma ação de cada tipo, cada uma
   com prazo e a **evidência de conclusão** (o que outra pessoa veria):
   - **70, prática:** um projeto ou uma responsabilidade no trabalho;
   - **20, com outras pessoas:** mentoria, par, revisão, ensinar alguém;
   - **10, estudo:** de preferência um módulo de um curso do Socrates, citado pelo nome; se
     não houver, o material que ele escolher.
6. **Ritmo e registro.** Combine a data dos check-ins (sugira uma vez por mês). Crie
   `~/.socrates/pdi/pdi.md` do template, mostre o caminho e feche com: "No dia do check-in,
   é só `/socrates-pdi:pdi`."

## Workflow: check-in

1. Leia o `pdi.md` e, de cada curso ligado a uma competência, o `progresso.md`.
2. Para cada ação vencida ou em andamento, pergunte o que foi feito e peça a evidência.
   Ação sem evidência não fecha, mesmo que ele diga que fez.
3. **Níveis**, por competência, sempre pelas regras de `niveis.md`:
   - **ligada a um eixo de curso:** copie do `progresso.md` o nível e as camadas da
     reavaliação mais recente do curso. O PDI não mede o que o curso já mede;
   - **`declarado: N`:** faça o diagnóstico (M e depois D ou R), como no passo 3 do montar.
     A declaração não escolhe a pergunta;
   - **medida, sem curso:** pergunte pelas camadas que faltam para o nível seguinte, a
     partir da "Próxima camada", uma por vez, sem pista. A camada que ele demonstrar entra
     em "Camadas demonstradas", e o nível só sobe quando **todas** as camadas até o peso
     do nível seguinte estão lá (regra cumulativa), no máximo até 4. Desce pela regra de
     descida da seção Reavaliação de `niveis.md`.
4. **Atualize o plano e registre.** No `pdi.md`, atualize as tabelas para o agora:
   Situação de cada ação (`aberta`, `fechada` com a evidência, ou `cancelada` com o
   motivo), Nível atual, Camadas demonstradas, Evidência do nível, Próxima camada e
   Próximo check-in. Depois acrescente a seção do check-in ao fim (data, ações fechadas
   com a evidência, camadas e níveis que mudaram e por quê, o que muda no plano). As
   seções de check-ins antigos nunca são reescritas. Mostre a ele o resumo com o tom da
   rubrica do Socrates: honesto, específico, comparando com ele mesmo.
5. Pergunte se o objetivo ainda é o mesmo. Se mudou, refaça os blocos 2 a 5 do montar.

## Critical Rules

- MUST NOT escolher objetivo, competência ou ação por ele. Por quê: um PDI que ele não
  escolheu é um PDI que ele não cumpre.
- MUST medir o nível pela resposta ou pelo registro do curso, nunca pela declaração. Por
  quê: é a regra do Socrates, e um plano montado sobre um nível inflado erra a lacuna.
- MUST NOT escrever no estado de um curso (`progresso.md`, diários). Por quê: é do motor,
  e a reavaliação de nível depende dele estar intacto.
- MUST pedir evidência para fechar uma ação. Por quê: sem evidência, o check-in vira lista
  de intenções.
