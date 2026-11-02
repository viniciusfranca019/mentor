# Estado do aluno: `~/.socrates`

O estado mora na máquina do aluno, fora do plugin. Atualizar ou reinstalar o plugin
nunca apaga o progresso. Tudo é Markdown, para ele poder abrir e ler o próprio histórico.

```
~/.socrates/
├── perfil.md                         # quem é, curso ativo, ritmo combinado
└── <curso>/                          # um diretório por curso iniciado
    ├── progresso.md                  # onde está, o que concluiu, o que revisar
    └── diario/
        └── AAAA-MM-DD.md             # tudo o que aconteceu no dia
```

## Migração do Mentor

O plugin se chamava Mentor e guardava o estado em `~/.mentor`. Se `ls -d ~/.mentor`
encontra a pasta e `~/.socrates` não existe, rode `mv ~/.mentor ~/.socrates` antes de
ler qualquer estado, e avise o aluno em uma linha: "Seu progresso do Mentor agora fica em
`~/.socrates`." Os arquivos não mudam de formato, só de lugar. Se as duas pastas
existirem, não mova nada: use `~/.socrates` e diga a ele que `~/.mentor` ficou para trás.

## Templates

Crie cada arquivo copiando o template correspondente e preenchendo os campos:

| Arquivo | Template |
|---------|----------|
| `~/.socrates/perfil.md` | `<raiz>/skills/socrates/templates/perfil.md` |
| `~/.socrates/<curso>/progresso.md` | `<raiz>/skills/socrates/templates/progresso.md` |
| `~/.socrates/<curso>/diario/AAAA-MM-DD.md` | `<raiz>/skills/socrates/templates/diario.md` |

O `progresso.md` começa com a trilha do `curso.md`: copie a lista de módulos e lições do
curso para a seção "Trilha", todas desmarcadas.

## Regras de escrita

- **Datas em ISO** (`2026-10-02`), sempre a data real do dia. Para saber a data, use
  `date +%F`.
- **O diário só cresce.** Acrescente ao fim e nunca reescreva entradas antigas. Ele é o
  registro do que aconteceu.
- **O progresso reflete o agora.** Pode ser editado: marcar lição, mover o "Onde parei",
  atualizar "Para revisar" e os "Níveis por eixo".
- **Camadas em toda resposta.** Cada pergunta no diário registra a camada que ela pedia e as
  camadas que a resposta demonstrou (`references/niveis.md`). É a evidência da reavaliação de nível.
- **Resumo fiel da resposta.** No diário, resuma o que ele disse com as palavras dele.
  Não melhore a resposta: o `/socrates:feedback` precisa ver o que ele de fato respondeu.
- **Curso novo, diretório novo.** Trocar de curso não apaga o outro; o `perfil.md` muda
  o curso ativo e a situação dos dois na tabela "Cursos" (`em andamento` e `pausado`).
- **Versão do curso.** Anote no `progresso.md` a versão do plugin em que ele começou
  cada módulo (`version` em `<raiz>/.claude-plugin/plugin.json`). Se o
  módulo mudar numa atualização, você sabe que a lição em andamento pode ter mudado.
