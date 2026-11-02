# Estado do aluno: `~/.socrates`

O estado mora na máquina do aluno, fora do plugin. Atualizar ou reinstalar o plugin
nunca apaga o progresso. Tudo é Markdown, para ele poder abrir e ler o próprio histórico.

```
~/.socrates/
├── profile.md                         # quem é, curso ativo, ritmo combinado
├── <extension>/                       # o estado de uma extensão, ex.: pdi/ (extension-contract.md)
└── <course>/                          # um diretório por curso iniciado
    ├── progress.md                  # onde está, o que concluiu, o que revisar
    └── journal/
        └── YYYY-MM-DD.md             # tudo o que aconteceu no dia
```

## Migração do Mentor

O plugin se chamava Mentor e guardava o estado em `~/.mentor`. Antes de ler qualquer
estado, veja com `ls -d ~/.mentor ~/.socrates` quais existem:

| Existe | O que fazer |
|--------|-------------|
| Só `~/.mentor` | Pare e peça ao aluno que mova a pasta ele mesmo, digitando no Claude Code `! mv ~/.mentor ~/.socrates`, e que repita o que pediu (o comando, ou o pedido que abriu a sessão). Os arquivos não mudam de formato, só de lugar. Você não move: escrever fora da pasta da sessão pede uma aprovação que nem sempre aparece |
| As duas | Não mova nada. Use `~/.socrates` e avise em uma linha que `~/.mentor` ficou para trás e pode ser apagada quando ele quiser |
| Só `~/.socrates`, ou nenhuma | Nada a migrar. Siga sem falar disso |

## Templates

Crie cada arquivo copiando o template correspondente e preenchendo os campos:

| Arquivo | Template |
|---------|----------|
| `~/.socrates/profile.md` | `<root>/skills/socrates/templates/profile.md` |
| `~/.socrates/<course>/progress.md` | `<root>/skills/socrates/templates/progress.md` |
| `~/.socrates/<course>/journal/YYYY-MM-DD.md` | `<root>/skills/socrates/templates/journal.md` |

O `progress.md` começa com a trilha do `course.md`: copie a lista de módulos e lições do
curso para a seção "Trilha", todas desmarcadas.

## Regras de escrita

- **Datas em ISO** (`2026-10-02`), sempre a data real do dia. Para saber a data, use
  `date +%F`.
- **O diário só cresce.** Acrescente ao fim e nunca reescreva entradas antigas. Ele é o
  registro do que aconteceu.
- **O progresso reflete o agora.** Pode ser editado: marcar lição, mover o "Onde parei",
  atualizar "Para revisar" e os "Níveis por eixo".
- **Camadas em toda resposta.** Cada pergunta no diário registra a camada que ela pedia e as
  camadas que a resposta demonstrou (`references/levels.md`). É a evidência da reavaliação de nível.
- **Resumo fiel da resposta.** No diário, resuma o que ele disse com as palavras dele.
  Não melhore a resposta: o `/socrates:feedback` precisa ver o que ele de fato respondeu.
- **Curso novo, diretório novo.** Trocar de curso não apaga o outro; o `profile.md` muda
  o curso ativo e a situação dos dois na tabela "Cursos" (`em andamento` e `pausado`).
- **Versão do curso.** Anote no `progress.md` a versão do plugin em que ele começou
  cada módulo: a versão do plugin do curso, que a skill `socrates-<course>:course` indica. Se o
  módulo mudar numa atualização, você sabe que a lição em andamento pode ter mudado.
