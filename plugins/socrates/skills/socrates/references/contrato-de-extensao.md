# Contrato de extensão

Leitura para quem **escreve** uma extensão do Socrates que não é curso: um método que
usa os critérios do Socrates para outra coisa, como o PDI (`socrates-pdi`). Um curso
segue o `contrato-de-curso.md`; este contrato é para o resto. Versão: **1**.

A diferença: um curso é só dado, e quem conduz é o motor. Uma extensão traz o próprio
workflow (skill e comando), e usa do Socrates só os critérios e o estado.

## O plugin da extensão

```
plugins/socrates-<extensão>/
├── .claude-plugin/plugin.json      # name socrates-<extensão>, version, "dependencies": ["socrates"]
├── commands/<extensão>.md          # a entrada: /socrates-<extensão>:<extensão>
├── skills/<extensão>/
│   ├── SKILL.md                    # o método da extensão
│   └── templates/                  # o formato do estado dela
├── CHANGELOG.md
└── LICENSE
```

| O contrato exige | Por quê |
|------------------|---------|
| `"dependencies": ["socrates"]` no `plugin.json` e na entrada do marketplace | Instalar a extensão instala o Socrates, que tem os critérios |
| Carregar a skill `socrates:criterios` antes de usar uma escala ou uma rubrica, e ler os arquivos que ela indica | Os critérios são do Socrates, um lugar só. A extensão não copia a escala de níveis nem a rubrica: cópia diverge na primeira mudança |
| O estado em `~/.socrates/<extensão>/`, com a mesma checagem de migração do `estado.md` antes de ler ou criar qualquer arquivo | O aluno tem um lugar só para o histórico dele, e a extensão sobrevive a atualizações como os cursos |
| Ler o estado dos cursos (`perfil.md`, `progresso.md`, diários), **nunca escrever** nele | O progresso de um curso é do motor. Uma extensão que escreve ali quebra a reavaliação de nível, que depende do diário |
| Comandos com `disable-model-invocation: true` e `allowed-tools` com `Read(/${CLAUDE_PLUGIN_ROOT}/**)`, `Read(~/.claude/plugins/cache/socrates/**)` e o acesso a `~/.socrates/**` | É o que deixa o primeiro turno ler a extensão, os critérios e o estado sem pedir aprovação |
| A skill de entrada **sem** `allowed-tools` | Com ele, carregar a skill pede aprovação |
| Uma linha na seção Extensões de `plugins/socrates/skills/socrates/catalogo.md` | O onboarding do Socrates mostra o que existe antes de estar instalado |

O nome `<extensão>` não pode ser o de um curso: os dois dividem `~/.socrates/`.
