---
name: curso
description: >
  Curso do Socrates: security-engineer. Para quem tem formação em TI mas pouca prática de
  programação, redes e infraestrutura. Aonde chega: engenheiro de segurança na era da IA.
  Situação: módulos 00 e 01 disponíveis, de 42. Use only when the Socrates engine
  (socrates:socrates) lists, diagnoses or teaches this course; never on its own.
---

# Curso security-engineer

Este arquivo é o contrato de curso do Socrates, versão 1. Ele não ensina nada: diz ao
motor (`socrates:socrates`) onde está o conteúdo deste curso.

- **Curso:** `security-engineer`
- **Raiz do curso:** `${CLAUDE_PLUGIN_ROOT}/course`
- **Trilha, eixos e diagnóstico:** `${CLAUDE_PLUGIN_ROOT}/course/course.md`
- **Módulos:** `${CLAUDE_PLUGIN_ROOT}/course/modules/<NN-name>.md`
- **Versão do curso:** a `version` de `${CLAUDE_PLUGIN_ROOT}/.claude-plugin/plugin.json`

Nos arquivos do curso, `<course>` significa a raiz do curso acima, e `<root>` significa a
raiz do plugin `socrates`, que o motor conhece.
