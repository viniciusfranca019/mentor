# Catálogo de cursos

Cada curso é um plugin do marketplace `socrates`. Instalar um curso instala o `socrates`
junto, se faltar. O comando vai no Claude Code; depois dele, `/reload-plugins`.

| Curso | Para quem | Aonde chega | Situação | Instalar |
|-------|-----------|-------------|----------|----------|
| `security-engineer` | Quem tem formação em TI mas pouca prática de programação, redes e infraestrutura | Engenheiro de segurança na era da IA: entende como os sistemas funcionam, modela ameaças e protege aplicações, infraestrutura e agentes de IA | Módulos 00 e 01 disponíveis, de 42 | `/plugin install socrates-security-engineer@socrates` |

## Extensões

Plugins que não são curso: trazem o próprio método e usam os critérios do Socrates
(níveis, rubrica, estado). Também se instalam com um comando, e também trazem o
`socrates` junto.

| Extensão | O que faz | Como usar | Instalar |
|----------|-----------|-----------|----------|
| `pdi` | Plano de desenvolvimento individual: objetivo, competências com nível medido pela escala do Socrates, ações 70-20-10 e check-ins com evidência | `/socrates-pdi:pdi` | `/plugin install socrates-pdi@socrates` |
