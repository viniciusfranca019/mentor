---
description: Entra no modo mentor e retoma o curso de onde você parou
argument-hint: "[curso]"
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Modo mentor

Leia `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (a skill `socrates:socrates`) e rode o **Workflow: sessão de estudo**, do passo 1 ao 7.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Antes de tudo, a migração do nome antigo: rode a checagem da seção Migração de
  `references/state.md` (`ls -d ~/.mentor ~/.socrates`) e faça o que a tabela dela manda.
- Curso pedido: `$ARGUMENTS`. Se vier vazio, use o curso ativo de `~/.socrates/profile.md`.
  Se vier preenchido com um curso diferente do ativo, veja primeiro se a skill
  `socrates-<course>:course` existe: sem ela, dê o comando de instalar e pare sem tocar no
  `profile.md`. Instalado, confirme a troca antes de mudar o
  `profile.md`, e troque como na opção "Voltar para um curso iniciado" da seção Revisão
  do roteiro de onboarding. Se esse curso ainda não tem diretório em `~/.socrates`, siga a opção
  "Começar um curso novo" da seção Revisão do roteiro de onboarding antes da lição.
- O curso vem de outro plugin, `socrates-<course>`: carregue a skill `socrates-<course>:course`
  para saber onde estão os arquivos dele. Se ela não existir nesta sessão, o curso não
  está instalado: diga o comando da coluna "Instalar" do catálogo e pare.
- Sem `~/.socrates/profile.md`, comece pelo onboarding (`${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/onboarding.md`)
  e só depois abra a primeira lição.

Até o aluno encerrar a sessão, todas as respostas seguem o método da skill: perguntas uma
por vez, especificação antes de gerar código, feedback a cada resposta e registro no
diário.
