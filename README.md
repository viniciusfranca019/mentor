# Mentor

Um mentor socrático dentro do Claude Code. O Mentor conduz um curso lição a lição: faz
perguntas em vez de dar respostas, deixa você construir com IA enquanto questiona cada
decisão e, no fim do dia, avalia como você foi.

O Mentor não proíbe a IA: ensina a dirigir a IA. Você usa o Claude Code para escrever
código o tempo todo, mas antes de gerar qualquer coisa você especifica o que quer, e
depois explica o que recebeu. Ferramenta, inclusive de IA, é atalho de algo que você já
entende.

## Cursos

| Curso | Para quem | Aonde chega | Situação |
|-------|-----------|-------------|----------|
| `security-engineer` | Quem tem formação em TI mas pouca prática de programação, redes e infraestrutura | Engenheiro de segurança na era da IA | Módulos 00 e 01 disponíveis, de 42 |

A trilha completa de cada curso está em [`cursos/`](cursos/catalogo.md).

## Setup

Pré-requisito: [Claude Code](https://code.claude.com) instalado.

```bash
claude plugin marketplace add viniciusfranca019/mentor
claude plugin install mentor@mentor
```

Depois, dentro do Claude Code:

| Comando | Quando usar |
|---------|-------------|
| `/mentor:onboarding` | Na primeira vez: mostra os cursos, o caminho e faz o diagnóstico. Depois: ver os cursos, trocar de curso ou ajustar o ritmo |
| `/mentor:mentor-mode` | Sempre que for estudar. Retoma de onde você parou |
| `/mentor:feedback` | Ao terminar as lições do dia. Avalia como você foi |

> Use o prefixo `mentor:` no feedback: o `/feedback` sem prefixo é o comando do próprio
> Claude Code para mandar feedback à Anthropic.

### Receber atualizações

Módulos e cursos novos chegam como novas versões do plugin. Para recebê-las sozinho,
ligue o auto-update deste marketplace (vem desligado para marketplaces de terceiros):
`/plugin` → **Marketplaces** → `mentor` → **Enable auto-update**. Ou atualize na mão:

```bash
claude plugin update mentor@mentor
```

Uma sessão aberta continua na versão antiga até `/reload-plugins` ou uma sessão nova.

## Seu progresso

Fica na sua máquina, em `~/.mentor`, e nunca é apagado por uma atualização do plugin:

```
~/.mentor/
├── perfil.md                    # você, o curso ativo e o ritmo combinado
└── <curso>/
    ├── progresso.md             # onde parou, o que concluiu, o que revisar
    └── diario/AAAA-MM-DD.md     # cada pergunta, sua resposta e o feedback
```

## Como funciona por dentro

| Peça | O que é |
|------|---------|
| `skills/mentor/` | O motor: o método socrático, o formato do estado, o onboarding e a rubrica do feedback. É o mesmo para todos os cursos |
| `cursos/<curso>/` | O conteúdo: a trilha (`curso.md`) e um arquivo por módulo, com as perguntas de cada lição e o critério de uma boa resposta |
| `commands/` | Os três comandos de entrada |

Para escrever um curso novo, veja
[`skills/mentor/references/anatomia-do-curso.md`](skills/mentor/references/anatomia-do-curso.md).

## Versionamento

[Semantic Versioning](https://semver.org/lang/pt-BR/), com tags `vX.Y.Z`. A versão em
`.claude-plugin/plugin.json` é o que dispara a atualização para quem já instalou: um
commit novo sem subir a versão não chega a ninguém. As mudanças estão no
[CHANGELOG](CHANGELOG.md).

## Licença

[Apache 2.0](LICENSE).
