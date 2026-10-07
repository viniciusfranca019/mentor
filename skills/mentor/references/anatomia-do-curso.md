# Anatomia de um curso

Leitura para quem **escreve** cursos, não para o aluno. O motor (`skills/mentor`) é o
mesmo para todos os cursos. Um curso é só dado: um diretório em `cursos/` que segue esta
estrutura.

```
cursos/
├── catalogo.md                      # tabela de cursos disponíveis
└── <curso>/                         # nome em kebab-case, ex.: security-engineer
    ├── curso.md                     # visão, trilha, diagnóstico
    └── modulos/
        ├── 00-<nome>.md             # um arquivo por módulo
        └── 01-<nome>.md
```

## Criar um curso novo

1. Crie `cursos/<curso>/curso.md` com as seções abaixo.
2. Escreva pelo menos o primeiro módulo completo em `modulos/`.
3. Acrescente uma linha em `cursos/catalogo.md` e na tabela de cursos do `README.md`.
4. Registre no `CHANGELOG.md` e suba a versão MINOR do plugin.

## `curso.md`

| Seção | Conteúdo |
|-------|----------|
| **Para quem é** | O aluno-alvo e o ponto de partida esperado |
| **Aonde chega** | O que ele sabe fazer ao terminar |
| **Princípio do curso** | A ideia que costura o curso inteiro |
| **Diagnóstico** | 5 a 8 perguntas de ponto de partida, usadas no onboarding |
| **Trilha** | Fases → módulos → lições, com o status de cada módulo (`disponível` ou `planejado`) |

## Módulo (`modulos/NN-nome.md`)

Cabeçalho do módulo: **Objetivo** (uma frase), **Pré-requisitos** (módulos anteriores) e
**Por que importa para o curso** (a ligação com o objetivo final).

Cada lição tem exatamente estas partes:

```markdown
## Lição N.M — <nome>

**Conceito-âncora:** <a ideia que ele precisa conseguir explicar ao fim, em 1 ou 2 frases>

### Abertura
1. <pergunta>
   - Uma boa resposta contém: <critérios>
2. ...

### Missão
<O que construir com o Claude, em 2 ou 3 frases, e por que isso torna o conceito visível.>

Perguntas de especificação (antes de gerar o código):
1. <pergunta>
   - Uma boa resposta contém: <critérios>

### Verificação
1. <pergunta de previsão, de quebra ou de explicação>
   - Uma boa resposta contém: <critérios>

### Ferramenta
<A ferramenta do mercado e a pergunta que liga a ferramenta à missão.>

### Explicar de volta
<O pedido final. Critério: o que a explicação precisa conter para a lição fechar.>

### Para o Mentor
- **Erros comuns:** <confusões típicas e como desfazê-las>
- **Ponte para segurança:** <por que este conceito importa para o objetivo do curso>
```

## Regras de escrita

- **Uma ideia por lição.** Se o conceito-âncora precisa de "e" para juntar duas ideias,
  são duas lições.
- **Perguntas sem a resposta dentro.** Ver a tabela de perguntas boas e ruins em
  `references/metodo.md`.
- **Critério observável.** "Uma boa resposta contém" lista ideias que dá para conferir na
  resposta, não "entende bem o assunto".
- **Missão pequena.** De 10 a 60 linhas de código, rodando na máquina dele, sem serviço
  pago.
- **Mudanças em módulo publicado.** Corrigir texto é PATCH. Mudar perguntas ou missão de
  lição publicada é MINOR, com nota no CHANGELOG, porque alunos podem estar no meio dela.
