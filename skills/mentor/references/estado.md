# Estado do aluno: `~/.mentor`

O estado mora na máquina do aluno, fora do plugin. Atualizar ou reinstalar o plugin
nunca apaga o progresso. Tudo é Markdown, para ele poder abrir e ler o próprio histórico.

```
~/.mentor/
├── perfil.md                         # quem é, curso ativo, ritmo combinado
└── <curso>/                          # um diretório por curso iniciado
    ├── progresso.md                  # onde está, o que concluiu, o que revisar
    └── diario/
        └── AAAA-MM-DD.md             # tudo o que aconteceu no dia
```

## Templates

Crie cada arquivo copiando o template correspondente e preenchendo os campos:

| Arquivo | Template |
|---------|----------|
| `~/.mentor/perfil.md` | `<raiz>/skills/mentor/templates/perfil.md` |
| `~/.mentor/<curso>/progresso.md` | `<raiz>/skills/mentor/templates/progresso.md` |
| `~/.mentor/<curso>/diario/AAAA-MM-DD.md` | `<raiz>/skills/mentor/templates/diario.md` |

O `progresso.md` começa com a trilha do `curso.md`: copie a lista de módulos e lições do
curso para a seção "Trilha", todas desmarcadas.

## Regras de escrita

- **Datas em ISO** (`2026-10-02`), sempre a data real do dia. Para saber a data, use
  `date +%F`.
- **O diário só cresce.** Acrescente ao fim e nunca reescreva entradas antigas. Ele é o
  registro do que aconteceu.
- **O progresso reflete o agora.** Pode ser editado: marcar lição, mover o "Onde parei",
  atualizar "Para revisar".
- **Resumo fiel da resposta.** No diário, resuma o que ele disse com as palavras dele.
  Não melhore a resposta: o `/mentor:feedback` precisa ver o que ele de fato respondeu.
- **Curso novo, diretório novo.** Trocar de curso não apaga o outro; o `perfil.md` só
  muda o curso ativo.
- **Versão do curso.** Anote no `progresso.md` a versão do plugin em que ele começou
  cada módulo (`version` em `<raiz>/.claude-plugin/plugin.json`). Se o
  módulo mudar numa atualização, você sabe que a lição em andamento pode ter mudado.
