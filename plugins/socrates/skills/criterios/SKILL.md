---
name: criterios
description: >
  Critérios do Socrates para as extensões dele: a escala de níveis por eixo, a rubrica da
  avaliação, o formato do estado em ~/.socrates e os contratos de curso e de extensão.
  Use only when a Socrates extension (a socrates-<x> plugin such as socrates-pdi) needs
  the Socrates scale, rubric, state format or contracts; it runs no workflow by itself.
---

# Critérios do Socrates

Este arquivo não conduz nada. Ele diz a uma extensão do Socrates onde estão os critérios
que valem para todas, porque um plugin não lê o outro por caminho relativo.

- **Raiz do Socrates:** `${CLAUDE_PLUGIN_ROOT}`. Nos arquivos abaixo, `<raiz>` é esse caminho.
- **Versão do Socrates:** a `version` de `${CLAUDE_PLUGIN_ROOT}/.claude-plugin/plugin.json`.

| Critério | Arquivo | Para quê |
|----------|---------|----------|
| Níveis por eixo | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/niveis.md` | A escala de 1 a 5, as nove camadas e a regra "pela resposta, nunca pela declaração" |
| Avaliação | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/feedback.md` | A rubrica e o tom: honesto, específico, cada afirmação ligada a um registro |
| Estado do aluno | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/estado.md` | O formato de `~/.socrates`, a migração do Mentor e as regras de escrita |
| Contrato de curso | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/contrato-de-curso.md` | O que um plugin de curso precisa ter |
| Contrato de extensão | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/contrato-de-extensao.md` | O que um plugin que não é curso (como o PDI) precisa ter e pode fazer |
