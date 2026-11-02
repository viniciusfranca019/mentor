# Changelog: socrates-pdi

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/), versões
em [Semantic Versioning](https://semver.org/lang/pt-BR/).

## [Unreleased]

## [0.1.0] - 2026-11-02

### Adicionado

- `/socrates-pdi:pdi`: monta o PDI do aluno (objetivo com sinal de chegada, de 3 a 5
  competências, nível atual pela escala do Socrates, nível alvo, ações 70-20-10 com prazo
  e evidência) e, com o PDI já criado, faz o check-in.
- O nível de uma competência segue a escala do Socrates: vem do registro do curso ou do
  diagnóstico (M, depois D ou R), com as camadas demonstradas registradas, nunca da
  declaração. Sem curso, o alvo vai até 4, porque as camadas 6 a 9 só saem da prova de
  saída de um módulo. Os critérios são lidos do Socrates pela skill `socrates:criterios`.
- O check-in atualiza as tabelas do plano (ações, níveis, próximo check-in) e acrescenta
  a seção do dia; os check-ins antigos não mudam.
- O PDI fica em `~/.socrates/pdi/pdi.md`, com os check-ins acrescentados ao fim.

[Unreleased]: https://github.com/viniciusfranca019/mentor/compare/socrates-pdi--v0.1.0...HEAD
[0.1.0]: https://github.com/viniciusfranca019/mentor/releases/tag/socrates-pdi--v0.1.0
