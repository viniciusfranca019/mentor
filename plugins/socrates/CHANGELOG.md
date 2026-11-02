# Changelog

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/), versões
em [Semantic Versioning](https://semver.org/lang/pt-BR/).

## [Unreleased]

## [0.4.0] - 2026-11-02

### Adicionado

- Skill `socrates:criterios`: diz a uma extensão onde estão os níveis, a rubrica, o
  formato do estado e os contratos, porque um plugin não lê o outro por caminho relativo.
- `references/contrato-de-extensao.md`: o que um plugin que não é curso precisa ter (o
  próprio método, `dependencies: ["socrates"]`, estado em `~/.socrates/<extensão>/`, e
  nunca escrever no estado de um curso).
- O catálogo ganha a seção Extensões, com o PDI (`socrates-pdi`), e o onboarding mostra o
  PDI no caminho e na revisão.

## [0.3.0] - 2026-11-02

### Alterado

- O repositório vira um marketplace com um plugin por peça: `socrates` é o motor (método,
  níveis, avaliação, estado do aluno), e cada curso é um plugin à parte,
  `socrates-<curso>`, que exige o `socrates`. O primeiro é `socrates-security-engineer`.
  Versões e tags por plugin (`socrates--v0.3.0`).
- O motor acha um curso pela skill `socrates-<curso>:curso`, que diz a raiz do conteúdo.
  Curso não instalado: o Socrates mostra o comando de instalar e para.
- O onboarding mostra no catálogo se cada curso está instalado e ensina que os cursos são
  plugins. A revisão ganha a situação **não instalado**.
- `references/anatomia-do-curso.md` vira `references/contrato-de-curso.md`: o que um
  plugin de curso precisa ter, além do formato de curso e de módulo.

- O plugin passa a se chamar **Socrates**: o plugin e o marketplace são `socrates`
  (`claude plugin install socrates@socrates`), os comandos viram `/socrates:onboarding`,
  `/socrates:mentor-mode` e `/socrates:feedback`, e a skill vira `socrates:socrates`
  (`skills/socrates/`). O repositório continua `viniciusfranca019/mentor`.
- O estado do aluno muda de `~/.mentor` para `~/.socrates`, no mesmo formato. Se só a
  pasta antiga existe, o primeiro comando pede ao aluno que rode
  `! mv ~/.mentor ~/.socrates` e repita o comando.

### Corrigido

- Os comandos pré-autorizam a leitura dos arquivos do próprio plugin
  (`Read(/${CLAUDE_PLUGIN_ROOT}/**)`): instalado pelo marketplace, o `/socrates:onboarding`
  parava no primeiro turno sem conseguir ler o SKILL.md, as references e o catálogo.

## [0.2.0] - 2026-10-06

### Adicionado

- Níveis por eixo do curso, de 1 (leigo) a 5 (expert), com pesos de profundidade
  1, 2, 3, 5 e 9 medidos em nove camadas de conhecimento e prática
  (`skills/mentor/references/niveis.md`).
- Diagnóstico adaptativo por eixo no onboarding: duas perguntas por eixo, com o
  resultado mostrado ao aluno e registrado no `progresso.md`. No `security-engineer`,
  os eixos são Sistemas, Redes, Construir com IA, Infraestrutura e Segurança.
- Prova de saída: num eixo de nível 4 ou 5, o módulo pode ser validado provando as
  camadas 6 a 9, sem pular conteúdo por declaração.
- Reavaliação do nível do eixo pelo `/mentor:feedback` ao fim de cada fase. O diário
  registra as camadas de cada resposta.

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

[Unreleased]: https://github.com/viniciusfranca019/mentor/compare/socrates--v0.4.0...HEAD
[0.4.0]: https://github.com/viniciusfranca019/mentor/compare/socrates--v0.3.0...socrates--v0.4.0
[0.3.0]: https://github.com/viniciusfranca019/mentor/compare/v0.2.0...socrates--v0.3.0
[0.2.0]: https://github.com/viniciusfranca019/mentor/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/viniciusfranca019/mentor/releases/tag/v0.1.0
