# Catálogo de cursos

A vitrine dos cursos que existem no marketplace `socrates`, para o aluno ver o que pode
instalar. Cada curso é um plugin; instalar um curso instala o `socrates` junto, se faltar.
O comando vai no Claude Code; depois dele, `/reload-plugins`.

Este catálogo só serve para curso **não instalado**. De um curso instalado, quem diz para
quem é, aonde chega e o que está disponível é a `description` da skill
`socrates-<course>:course`, que muda junto com o curso. Um curso instalado que não está aqui
aparece mesmo assim.

| Curso | Para quem | Aonde chega | Instalar |
|-------|-----------|-------------|----------|
| `security-engineer` | Quem tem formação em TI mas pouca prática de programação, redes e infraestrutura | Engenheiro de segurança na era da IA: entende como os sistemas funcionam, modela ameaças e protege aplicações, infraestrutura e agentes de IA | `/plugin install socrates-security-engineer@socrates` |

## Extensões

Plugins que não são curso: trazem o próprio método e usam os critérios do Socrates
(níveis, rubrica, estado). Também se instalam com um comando, e também trazem o
`socrates` junto. Como nos cursos, uma extensão instalada aparece pela skill dela
(`socrates-<extension>:<extension>`), mesmo que não esteja aqui.

| Extensão | O que faz | Como usar | Instalar |
|----------|-----------|-----------|----------|
| `pdi` | Plano de desenvolvimento individual: objetivo, competências com nível medido pela escala do Socrates, ações 70-20-10 e check-ins com evidência | `/socrates-pdi:pdi` | `/plugin install socrates-pdi@socrates` |
