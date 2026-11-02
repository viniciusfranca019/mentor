# Socrates

Um mentor socrático dentro do Claude Code. O Socrates conduz um curso lição a lição: faz
perguntas em vez de dar respostas, deixa você construir com IA enquanto questiona cada
decisão e, no fim do dia, avalia como você foi.

O Socrates não proíbe a IA: ensina a dirigir a IA. Você usa o Claude Code para escrever
código o tempo todo, mas antes de gerar qualquer coisa você especifica o que quer, e
depois explica o que recebeu. Ferramenta, inclusive de IA, é atalho de algo que você já
entende.

## O marketplace

O Socrates é o mentor, e cada curso é um plugin à parte que ele conduz. Instalar um
curso instala o Socrates junto.

| Plugin | O que é |
|--------|---------|
| `socrates` | O mentor: método socrático, níveis por eixo, avaliação do dia e o seu progresso em `~/.socrates` |
| `socrates-security-engineer` | Curso: engenheiro de segurança na era da IA, para quem tem formação em TI mas pouca prática de programação, redes e infraestrutura |

O que cada curso já tem disponível aparece no `/socrates:onboarding`.

## Setup

Pré-requisito: [Claude Code](https://code.claude.com) instalado.

```bash
claude plugin marketplace add viniciusfranca019/mentor
claude plugin install socrates-security-engineer@socrates
```

O segundo comando instala o curso e o `socrates`. Outro curso, depois, é só mais um
`claude plugin install socrates-<curso>@socrates`; o `/socrates:onboarding` mostra o
catálogo e o comando de cada um.

Instalou quando ele ainda se chamava Mentor? Troque o plugin uma vez e mova o seu
progresso com `mv ~/.mentor ~/.socrates` (o primeiro comando também te lembra disso):

```bash
claude plugin uninstall mentor@mentor
claude plugin marketplace remove mentor
claude plugin marketplace add viniciusfranca019/mentor
claude plugin install socrates-security-engineer@socrates
```

Depois, dentro do Claude Code:

| Comando | Quando usar |
|---------|-------------|
| `/socrates:onboarding` | Na primeira vez: mostra os cursos, o caminho e faz o diagnóstico. Depois: ver os cursos, trocar de curso ou ajustar o ritmo |
| `/socrates:mentor-mode` | Sempre que for estudar. Retoma de onde você parou |
| `/socrates:feedback` | Ao terminar as lições do dia. Avalia como você foi |

> Use o prefixo `socrates:` no feedback: o `/feedback` sem prefixo é o comando do próprio
> Claude Code para mandar feedback à Anthropic.

### Receber atualizações

Módulos novos chegam como novas versões do plugin do curso, e melhorias do método como
novas versões do `socrates`. Para recebê-las sozinho,
ligue o auto-update deste marketplace (vem desligado para marketplaces de terceiros):
`/plugin` → **Marketplaces** → `socrates` → **Enable auto-update**. Ou atualize na mão:

```bash
claude plugin update socrates@socrates
claude plugin update socrates-security-engineer@socrates
```

Uma sessão aberta continua na versão antiga até `/reload-plugins` ou uma sessão nova.

## Seu progresso

Fica na sua máquina, em `~/.socrates`, e nunca é apagado por uma atualização do plugin:

```
~/.socrates/
├── perfil.md                    # você, o curso ativo e o ritmo combinado
└── <curso>/
    ├── progresso.md             # onde parou, o que concluiu, o que revisar
    └── diario/AAAA-MM-DD.md     # cada pergunta, sua resposta e o feedback
```

## Como funciona por dentro

| Peça | O que é |
|------|---------|
| `plugins/socrates/` | O motor: o método socrático, os níveis, a rubrica do feedback, o formato do estado e o catálogo de cursos. É o mesmo para todos os cursos |
| `plugins/socrates-<curso>/` | Um curso: a trilha (`curso/curso.md`), um arquivo por módulo e a skill `curso`, que diz ao motor onde está o conteúdo |
| `.claude-plugin/marketplace.json` | A lista de plugins que o `marketplace add` traz |

Para escrever um curso novo, veja o
[contrato de curso](plugins/socrates/skills/socrates/references/contrato-de-curso.md).

## Versionamento

[Semantic Versioning](https://semver.org/lang/pt-BR/) por plugin, com tags
`<plugin>--vX.Y.Z` (ex.: `socrates--v0.3.0`). A versão no `plugin.json` de cada plugin é
o que dispara a atualização para quem já instalou: um commit novo sem subir a versão não
chega a ninguém. Cada plugin tem o seu `CHANGELOG.md`.

## Licença

[Apache 2.0](LICENSE).
