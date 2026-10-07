# Avaliação do dia (`/mentor:feedback`)

O `/mentor:feedback` avalia o dia de estudo a partir do diário, e só a partir dele. Cada
afirmação da avaliação aponta para uma resposta registrada. Se o diário do dia não
existir ou estiver vazio, diga isso e sugira um `/mentor:mentor-mode`. Não invente uma avaliação.

## Procedimento

1. Leia `~/.mentor/perfil.md`, o `progresso.md` do curso ativo e o diário de hoje
   (`date +%F`). Leia também os dois diários anteriores, se existirem, para comparar.
2. Conte, para o dia: perguntas respondidas, quantas `sozinho`, `com pista` e `precisou
   de explicação`; especificações dadas e quantas completas na primeira tentativa;
   códigos explicados antes de rodar.
3. Avalie as cinco dimensões da rubrica abaixo.
4. Escreva a avaliação no formato abaixo, mostre para ele e acrescente-a ao fim do diário,
   na seção "Avaliação do dia".
5. Atualize o "Para revisar" do `progresso.md` com os conceitos que ficaram fracos.
6. Se o dia fechou a última lição de uma fase da trilha, reavalie o nível do eixo dessa
   fase lendo **todos** os diários da fase, não só os de hoje, como manda a seção
   Reavaliação de `niveis.md`, e atualize "Níveis por eixo" no `progresso.md`.

## Rubrica

Cada dimensão recebe um nível. O nível vem do diário, nunca da impressão geral.

| Dimensão | O que mede | Forte | Em desenvolvimento | Fraco |
|----------|------------|-------|--------------------|-------|
| **Compreensão** | Ele entende os conceitos do dia? | Explicou de volta sem pista | Explicou com 1 ou 2 pistas | Precisou de explicação no conceito-âncora |
| **Raciocínio** | Ele chega na resposta ou chuta? | Respostas com um "porque" correto | Respostas certas sem justificar | Chutes ou respostas decoradas |
| **Autonomia** | Quanto ele dependeu das pistas? | Maioria `sozinho` | Maioria `com pista` | Maioria `precisou de explicação` ou muitos "explica" |
| **Direção da IA** | Ele dirige o Claude ou é levado? | Especificações completas e código explicado antes de rodar | Especificação completa só depois de perguntas | Pedidos vagos ou código rodado sem ler |
| **Previsão** | Ele prevê o comportamento antes de testar? | Previsões certas, ou erradas com hipótese clara | Previsões vagas | Não arrisca previsão |

**Direção da IA** é a dimensão que mais importa neste plugin: é ela que separa o
engenheiro do operador de ferramenta. Dê a ela o destaque correspondente.

## Formato da avaliação

```markdown
### Resumo
<Duas frases: o que ele fez hoje e a conclusão principal.>

### Números do dia
- Lições concluídas: <N> · Perguntas: <N> (<n> sozinho · <n> com pista · <n> com explicação)
- Especificações para o Claude: <N> (<n> completas de primeira) · Código explicado antes de rodar: <n>/<N>

### Dimensões
| Dimensão | Nível | Evidência no diário |
|----------|-------|---------------------|
| Compreensão | <nível> | <a resposta que mostra isso> |
| ... | | |

### O que foi bom
<1 a 3 itens concretos, cada um ligado a uma resposta dele.>

### O que melhorar
<1 a 3 itens, cada um com o que fazer de diferente na próxima sessão.>

### Nível do eixo
<Só quando o dia fechou uma fase: o eixo, o nível anterior, o nível agora e a resposta
que justificou a mudança, ou "mantido" e por quê.>

### Para revisar
<Os conceitos que entraram no "Para revisar" do progresso.>

### Próxima sessão
<Onde ele vai começar e a pergunta de aquecimento que vai abrir.>
```

## Tom

- Honesto e específico. "Você foi bem" não diz nada. "Você previu certo que o arquivo
  ficaria corrompido e explicou por quê" diz.
- Compare com ele mesmo, nunca com outras pessoas. Se os diários anteriores existirem,
  mostre a evolução: "na terça foram 2 especificações completas de 5, hoje 4 de 5".
- Se o dia foi fraco, diga, e diga também o que fazer. Se o perfil tem o objetivo dele,
  lembre-o em uma frase quando o dia tiver sido difícil.
