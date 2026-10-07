# Changelog

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/), versões
em [Semantic Versioning](https://semver.org/lang/pt-BR/).

## [Unreleased]

### Alterado

- Onboarding direto ao ponto: a primeira mensagem mostra o catálogo de cursos e pergunta
  qual o aluno quer, e o bloco "O caminho" mostra em uma tela o uso no dia a dia e como
  trocar de curso depois.
- As quatro fases da lição passam a ser explicadas no início da primeira lição, e não no
  onboarding.
- Rever o onboarding com perfil já criado mostra os cursos com a situação de cada um
  (ativo, iniciado, não iniciado) e as opções: continuar, voltar a um curso, começar um
  curso novo ou ajustar o ritmo. Começar outro curso faz só o diagnóstico dele.

## [0.1.0] - 2026-10-06

### Adicionado

- Motor de mentoria (`skills/mentor`): método socrático em quatro fases (Abertura,
  Missão, Verificação, Ferramenta), escada de pistas, construção com IA guiada por
  especificação, estado do aluno em `~/.mentor` e templates de perfil, progresso e diário.
- Comandos `/mentor:onboarding`, `/mentor:mentor-mode` e `/mentor:feedback`.
- Curso `security-engineer`: trilha de 42 módulos em 8 fases, diagnóstico inicial,
  módulo 00 (Seu laboratório) e módulo 01 (Como o computador representa as coisas).

[Unreleased]: https://github.com/viniciusfranca019/mentor/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/viniciusfranca019/mentor/releases/tag/v0.1.0
