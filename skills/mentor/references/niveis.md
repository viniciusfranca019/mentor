# Níveis por eixo

O nível do aluno é medido **por eixo do curso**, nunca um nível só: quem já programa mas
nunca viu redes é praticante num eixo e leigo no outro. Os eixos de cada curso, e a
escada de perguntas de cada eixo, estão no `curso.md` dele.

## A escala

São cinco níveis. O peso de cada nível é a **profundidade** que ele exige, contada em
camadas de conhecimento e prática: 1, 2, 3, 5 e 9. Do 1 ao 3 sobe uma camada por vez. Do
3 para o 4 o salto é de duas camadas, e do 4 para o 5, de quatro.

| Nível | Nome | Peso | O que a pessoa consegue |
|-------|------|------|-------------------------|
| 1 | Leigo | 1 | Sabe que aquilo existe, de forma vaga |
| 2 | Iniciante | 2 | Reconhece os termos e segue um tutorial |
| 3 | Praticante | 3 | Explica o mecanismo com as próprias palavras e faz sozinho o caso comum |
| 4 | Proficiente | 5 | Diagnostica o que deu errado e escolhe entre abordagens com motivo |
| 5 | Expert | 9 | Faz o caso fora do comum, ensina, antecipa ataques e conhece o próprio limite |

## As nove camadas

| Camada | O aluno demonstra | Completa o nível |
|--------|-------------------|------------------|
| 1. Noção | Sabe que existe e para que serve, ainda que vago | 1 |
| 2. Definição | Define corretamente, com o termo certo | 2 |
| 3. Mecanismo | Explica como funciona com as próprias palavras e faz o caso comum | 3 |
| 4. Diagnóstico | Acha a causa quando algo dá errado | |
| 5. Decisão | Escolhe entre abordagens e diz o motivo e o custo de cada uma | 4 |
| 6. Execução real | Faz um caso fora do comum sem roteiro nem pista | |
| 7. Ensino | Explica para um leigo, com um exemplo do mundo dele | |
| 8. Visão de ataque | Antecipa como aquilo falha ou como seria atacado | |
| 9. Conexão e limite | Liga o assunto a outros domínios e diz onde o próprio conhecimento acaba | 5 |

## Como classificar

- **Cumulativo.** O nível é o mais alto cujas camadas, até o peso dele, estão **todas**
  demonstradas. Quem fala de trade-off (camada 5) mas não explica o mecanismo (camada 3)
  fica no nível 2: falta uma camada no meio, e vocabulário avançado sem base não sobe nível.
- **Na dúvida, a camada não conta.** Só registre a camada que a resposta mostra com
  clareza. Superestimar é o erro mais caro: em segurança, achar que sabe o que não sabe é
  exatamente o que o curso existe para corrigir.
- **Pela resposta, nunca pela declaração.** "Eu já sei isso" não demonstra camada
  nenhuma. Se ele contestar um nível, siga a seção Contestação.

## Diagnóstico (no onboarding)

Cada eixo tem uma escada de três perguntas no `curso.md`:

| Degrau | Pede | Camadas que testa |
|--------|------|-------------------|
| **R** Reconhecer | Dizer o que é | 1 e 2 |
| **M** Mecanismo | Explicar como funciona | 3 |
| **D** Diagnóstico | Achar a causa de um problema **e** escolher a correção, com o custo | 4 e 5 |

Por eixo, comece pelo M. Se a resposta atingiu o critério, faça o D. Se não, faça o R.
São duas perguntas por eixo. Uma pergunta por vez, sem corrigir, como no resto do
diagnóstico. O nível sai deste caminho, e só dele:

| M | Segunda pergunta | Nível | Camadas registradas |
|---|------------------|-------|---------------------|
| atingiu a camada 3 | D com as camadas 4 **e** 5 | 4 | 1 a 5 |
| atingiu a camada 3 | D sem as duas | 3 | 1 a 3, mais a 4 se ela apareceu |
| não atingiu | R com a camada 2 | 2 | 1 e 2 |
| não atingiu | R sem a camada 2 | 1 | a 1 se ela apareceu, senão nenhuma |

Na escada do diagnóstico, atingir o M conta também as camadas 1 e 2, porque explicar o
mecanismo pressupõe saber o que a coisa é. O nível 1 é o piso: vale mesmo sem nenhuma
camada demonstrada.

## Contestação

Se ele contestar um nível no resultado do diagnóstico, uma pergunta nova decide, nunca a
declaração dele:

| Nível contestado | Pergunta | Se atingir o critério |
|------------------|----------|-----------------------|
| 1 ou 2 | A **M** do eixo, reformulada com outras palavras (degrau 1 da escada de pistas) | Faça a **D** e classifique pela tabela acima |
| 3 | A **D2** do eixo, no `curso.md`: outro problema de diagnóstico e decisão | Nível 4 |
| 4 | Nenhuma. As camadas 6 a 9 só saem da prova de saída, oferecida no primeiro módulo do eixo | — |

O diagnóstico vai até o nível 4: as camadas 1 a 5 aparecem numa conversa. As camadas 6
a 9 pedem fazer, ensinar e atacar, e só saem da prova de saída.

**O resultado para o aluno.** Ao fim do diagnóstico, mostre uma tabela: eixo, nível, a
próxima camada que falta e o que isso muda na trilha dele (tabela abaixo). Registre o
nível, as camadas e a resposta que justificou cada uma na seção "Níveis por eixo" do
`progresso.md`.

## O que o nível muda na trilha

| Nível no eixo | Como conduzir os módulos desse eixo |
|---------------|-------------------------------------|
| 1 e 2 | Trilha completa, Aberturas com calma, pistas mais cedo |
| 3 | Trilha completa, Aberturas aceleradas |
| 4 e 5 | Antes de cada módulo do eixo, ofereça a **prova de saída** |

O nível nunca pula conteúdo sozinho. Ele só libera a prova de saída, e quem pula o
módulo é quem passa nela.

## Prova de saída

Oferecida no início de um módulo cujo eixo está no nível 4 ou 5. Ele pode recusar e fazer
o módulo normal. A prova testa as camadas 6 a 9 sobre o conteúdo do módulo, uma pergunta
por vez:

1. **Execução real (6).** Uma variação da Missão de uma lição do módulo, diferente da
   missão escrita, feita sem pista. Ele especifica e explica o código, como em qualquer
   Missão.
2. **Ensino (7).** Explicar o conceito-âncora de cada lição do módulo para um leigo, com
   um exemplo do mundo da pessoa.
3. **Visão de ataque (8).** Como aquilo falha, ou como seria atacado.
4. **Conexão e limite (9).** Onde aquilo aparece em outro eixo do curso, e o que ele
   ainda não sabe sobre o assunto.

| Resultado | O que acontece |
|-----------|----------------|
| As quatro camadas demonstradas | Módulo **validado**: marque as lições como `[v]` no `progresso.md`, com a data, e o eixo vai para o nível 5 |
| Faltou alguma | O módulo segue normal, sem penalidade, e o eixo continua no nível em que estava |

Validar o módulo dispensa as lições, não o que elas deixam pronto. Se a Missão de uma
lição produz algo que os módulos seguintes usam, como o laboratório do módulo 00 ou uma
ferramenta instalada, ele faz essa parte mesmo com o módulo validado.

Registre a prova no diário como qualquer pergunta, com as camadas demonstradas.

## Reavaliação

O nível muda com o que ele demonstra durante a trilha, não só no diagnóstico.

- **A cada resposta**, o diário registra a camada que a pergunta pedia (a mais funda que o
  critério dela exige) e as camadas que **ele** demonstrou, sozinho ou com pista. O que
  veio da sua explicação nunca entra em "Camadas".
- **Ao fim de cada fase da trilha**, o `/mentor:feedback` lê **todos** os diários da fase,
  do primeiro dia da primeira lição dela até hoje, e reavalia o eixo:
  - **Sobe** quando as camadas que faltavam para o nível seguinte apareceram com clareza
    nas respostas, até o nível 4. O 5 só vem da prova de saída.
  - **Desce** quando as duas últimas perguntas que pediram a mesma camada N, mesmo com
    outras perguntas entre elas, terminaram com Resultado `precisou de explicação`,
    sendo N uma camada já registrada como demonstrada. A camada N sai das "Camadas
    demonstradas", e o nível passa a ser o mais alto cujas camadas continuam todas
    demonstradas (regra cumulativa).
  - Atualize "Níveis por eixo" com a data e as respostas que justificaram.
- **Aluno sem a seção "Níveis por eixo"** no `progresso.md` (começou numa versão anterior
  do plugin): faça o diagnóstico de níveis no início da próxima sessão, antes da lição.
