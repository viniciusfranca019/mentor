# Contrato de curso

Leitura para quem **escreve** cursos, não para o aluno. O motor (`socrates:socrates`) é o
mesmo para todos os cursos e não muda quando um curso entra. Um curso é só dado, num
plugin à parte do marketplace `socrates`, e este arquivo é o contrato que esse plugin
cumpre. Versão do contrato: **1**.

## O plugin do curso

```
plugins/socrates-<course>/                # <course> em kebab-case, ex.: security-engineer
├── .claude-plugin/plugin.json           # name, version, "dependencies": ["socrates"]
├── skills/course/SKILL.md                # a ponte: diz ao motor onde está o conteúdo
├── curso/
│   ├── course.md                         # visão, eixos e diagnóstico, trilha
│   └── modules/
│       ├── 00-<nome>.md                 # um arquivo por módulo
│       └── 01-<nome>.md
├── CHANGELOG.md
└── LICENSE
```

| Peça | O que o contrato exige | Por quê |
|------|------------------------|---------|
| `plugin.json` | `name` igual a `socrates-<course>`, `version` SemVer e `"dependencies": ["socrates"]` | Instalar o curso instala o motor junto; o nome é o prefixo da skill que o motor procura |
| `skills/course/SKILL.md` | `name: curso`. A `description` começa com `Curso do Socrates: <course>.` e traz para quem é, aonde chega e a situação (o que está disponível). É a **única** fonte desses dados para um curso instalado: atualize-a no mesmo PR de cada módulo novo. O corpo diz a **raiz do curso** com `${CLAUDE_PLUGIN_ROOT}/course` e a versão do contrato. **Sem** `allowed-tools` e **sem** `disable-model-invocation` | O motor não lê arquivos de outro plugin por caminho relativo: é carregando esta skill que ele descobre o caminho absoluto. Com `allowed-tools`, carregar a skill passa a pedir aprovação, e no teste headless ela foi negada |
| `curso/course.md` | As seções abaixo | O diagnóstico e a trilha saem daqui |
| `curso/modules/NN-nome.md` | O formato de módulo abaixo | As lições saem daqui |
| Marketplace | Uma entrada em `.claude-plugin/marketplace.json` da raiz, com `source: "./plugins/socrates-<course>"` e `dependencies: ["socrates"]` | É o que o aluno instala |
| Catálogo | Uma linha em `plugins/socrates/skills/socrates/catalog.md`: para quem, aonde chega e o comando de instalar, sem a situação | É a vitrine para quem ainda não instalou. O curso instalado aparece mesmo sem ela, pela skill, então o curso funciona sem esperar uma release do motor |

Nos arquivos do curso, `<root>` continua sendo a raiz do plugin `socrates` (o motor
conhece), e `<course>` é a raiz do curso que a skill dele indica. O formato de dado é
Markdown: quem lê é o modelo, e o aluno abre e entende os mesmos arquivos.

## Criar um curso novo

1. Copie a estrutura acima de `plugins/socrates-security-engineer/`, troque o nome e a
   `description` da skill `curso`.
2. Escreva `curso/course.md` com as seções abaixo e pelo menos o primeiro módulo completo.
3. Acrescente a entrada no `marketplace.json`, a linha no catálogo do motor e a linha na
   tabela do `README.md` da raiz.
4. `claude plugin validate plugins/socrates-<course>` e `claude plugin validate .`.
5. O curso começa na versão `0.1.0`, com o próprio `CHANGELOG.md`. A linha do catálogo
   sobe um PATCH do `socrates`, mas o curso não depende dela para funcionar: só para
   aparecer na vitrine de quem ainda não o instalou.
6. A cada módulo novo: suba o curso (MINOR) e a situação na `description` da skill `curso`.
   O motor não muda.

## `course.md`

| Seção | Conteúdo |
|-------|----------|
| **Para quem é** | O aluno-alvo e o ponto de partida esperado |
| **Aonde chega** | O que ele sabe fazer ao terminar |
| **Princípio do curso** | A ideia que costura o curso inteiro |
| **Eixos e diagnóstico** | De 3 a 6 eixos, cada um ligado a fases da trilha. Por eixo, uma escada de três perguntas: **R** (reconhecer, camadas 1 e 2), **M** (mecanismo, camada 3) e **D** (diagnóstico e decisão, camadas 4 e 5), cada uma com o critério da camada, mais uma **D2** (outro problema de diagnóstico e decisão) para quem contesta o nível 3. Escala e regras em `<root>/skills/socrates/references/levels.md` |
| **Trilha** | Fases → módulos → lições, com o status de cada módulo (`disponível` ou `planejado`) |

## Módulo (`modules/NN-nome.md`)

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

### Para o Socrates
- **Erros comuns:** <confusões típicas e como desfazê-las>
- **Ponte para segurança:** <por que este conceito importa para o objetivo do curso>
```

## Regras de escrita

- **Uma ideia por lição.** Se o conceito-âncora precisa de "e" para juntar duas ideias,
  são duas lições.
- **Perguntas sem a resposta dentro.** Ver a tabela de perguntas boas e ruins em
  `references/method.md`.
- **Critério observável.** "Uma boa resposta contém" lista ideias que dá para conferir na
  resposta, não "entende bem o assunto".
- **Missão pequena.** De 10 a 60 linhas de código, rodando na máquina dele, sem serviço
  pago.
- **Mudanças em módulo publicado.** Corrigir texto é PATCH. Mudar perguntas ou missão de
  lição publicada é MINOR, com nota no CHANGELOG, porque alunos podem estar no meio dela.
