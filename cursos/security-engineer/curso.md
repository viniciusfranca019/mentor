# Curso: Engenheiro de Segurança na era da IA

## Para quem é

Para quem tem formação em TI (por exemplo, tecnólogo em Análise e Desenvolvimento de
Sistemas) mas pouca prática de programação, redes, virtualização e infraestrutura. O
ponto de partida esperado: já ouviu falar de quase tudo, mas aprendeu pelo nome da
ferramenta, não pelo funcionamento por baixo.

## Aonde chega

Ao final, o aluno:

- explica como um computador, uma rede e uma aplicação web funcionam por dentro;
- lê e escreve código com a ajuda de IA, sabendo dirigir e revisar o que a IA produz;
- desenha a arquitetura de um sistema e acha suas fronteiras de confiança;
- modela ameaças, encontra e corrige as vulnerabilidades mais comuns;
- detecta e responde a incidentes a partir de logs;
- entende os riscos novos de sistemas com LLMs e agentes, e usa IA a favor da defesa.

## Princípio do curso

**Ferramenta é atalho de algo que você já entende.** Todo módulo constrói o fundamento
antes de mostrar a ferramenta. Um engenheiro de segurança é chamado justamente quando a
ferramenta não basta: quando o scanner não acha nada, o log não faz sentido, ou o ataque
é novo. Quem só conhece o botão não tem para onde ir nessa hora.

Na era da IA isso vale em dobro: o Claude é a ferramenta mais poderosa que o aluno vai
usar, e também a mais fácil de virar muleta. Aqui ele usa a IA o tempo todo, mas sempre
como o arquiteto que especifica e revisa.

## Diagnóstico

Perguntas do onboarding, uma por vez. Não corrigir, só registrar.

1. Quando você digita um endereço no navegador e aperta Enter, o que acontece até a
   página aparecer? Conte do jeito que souber.
2. Qual a diferença entre um programa e um processo?
3. Você já usou um terminal (Linux, PowerShell, cmd)? Para quê?
4. Já escreveu algum programa? Em qual linguagem e o que ele fazia?
5. O que você entende por "máquina virtual" e por "container"?
6. Se um sistema "foi hackeado", o que você imagina que aconteceu?
7. O que você já usou de IA para estudar ou trabalhar, e como foi?

## Trilha

Uma lição leva de 30 a 60 minutos. Os módulos `planejado` serão publicados nas próximas
versões do plugin.

### Fase 1 — A máquina

Ao fim: sabe o que acontece dentro de um computador quando um programa roda, e opera um
Linux pelo terminal.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 00 | Seu laboratório | 0.1 O que é um ambiente de estudo isolado · 0.2 Montando o Linux (WSL2 ou VM) · 0.3 Primeira conversa com o Claude como arquiteto | disponível |
| 01 | Como o computador representa as coisas | 1.1 Tudo é número: bits, bytes e hexadecimal · 1.2 Texto também é número: codificação · 1.3 Arquivos e formatos: a extensão mente · 1.4 Do código ao programa: compilado e interpretado | disponível |
| 02 | Processos e memória | 2.1 Programa vs processo · 2.2 Memória de um processo · 2.3 Processos conversando: sinais e pipes · 2.4 O que é um serviço (daemon) | planejado |
| 03 | O shell do Linux | 3.1 O que o shell faz com o que você digita · 3.2 Sistema de arquivos e caminhos · 3.3 Entrada, saída e redirecionamento · 3.4 Variáveis de ambiente e PATH · 3.5 Encontrar e filtrar: find, grep, pipes | planejado |
| 04 | Usuários, permissões e privilégio | 4.1 Usuários e grupos · 4.2 Permissões rwx · 4.3 root e sudo · 4.4 setuid e escalada de privilégio | planejado |

### Fase 2 — A rede

Ao fim: explica o caminho de uma requisição do navegador ao servidor, camada por camada.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 05 | Endereços e roteamento | 5.1 Por que existem camadas · 5.2 Endereço IP e máscara · 5.3 Roteamento e gateway · 5.4 NAT e IP privado | planejado |
| 06 | Transporte: TCP e UDP | 6.1 Portas · 6.2 O handshake TCP · 6.3 Confiabilidade vs velocidade: UDP · 6.4 Sockets: rede vista pelo programa | planejado |
| 07 | DNS | 7.1 Nomes viram endereços · 7.2 A hierarquia de servidores · 7.3 Cache e TTL · 7.4 Ataques ao DNS | planejado |
| 08 | HTTP | 8.1 Requisição e resposta · 8.2 Métodos e status · 8.3 Cabeçalhos · 8.4 Cookies e estado | planejado |
| 09 | TLS | 9.1 O problema do canal aberto · 9.2 O handshake TLS · 9.3 Certificados e cadeia de confiança · 9.4 O que o TLS não protege | planejado |

### Fase 3 — Construir com IA

Ao fim: dirige o Claude para construir programas pequenos e lê o código gerado com
segurança.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 10 | Ler código Python | 10.1 Variáveis, tipos e fluxo · 10.2 Funções · 10.3 Estruturas de dados · 10.4 Erros e exceções | planejado |
| 11 | Git | 11.1 O que é uma versão · 11.2 Commit, branch e merge · 11.3 Remoto e GitHub · 11.4 O que nunca vai para o Git | planejado |
| 12 | Automação com shell e Python | 12.1 Scripts no shell · 12.2 Ler e processar arquivos · 12.3 Chamar programas e APIs | planejado |
| 13 | APIs | 13.1 O que é uma API · 13.2 REST e JSON · 13.3 Construir uma API pequena · 13.4 Consumir uma API | planejado |
| 14 | Testes e revisão de código gerado por IA | 14.1 Por que testar · 14.2 Escrever um teste · 14.3 Revisar o que a IA escreveu | planejado |

### Fase 4 — Arquitetura e infraestrutura

Ao fim: desenha um sistema real com cliente, servidor, banco, containers e cloud, e
aponta onde estão os dados e os acessos.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 15 | Arquitetura de uma aplicação web | 15.1 Cliente, servidor e banco · 15.2 Estado e sessão · 15.3 Filas e serviços | planejado |
| 16 | Bancos de dados e SQL | 16.1 Tabelas e consultas · 16.2 Relacionamentos · 16.3 Quem acessa o banco | planejado |
| 17 | Virtualização | 17.1 Hipervisor e VM · 17.2 Isolamento e o que escapa dele · 17.3 Snapshot e lab descartável | planejado |
| 18 | Containers | 18.1 Namespaces e cgroups · 18.2 Imagem vs container · 18.3 Docker na prática · 18.4 Container não é VM | planejado |
| 19 | Orquestração | 19.1 Por que Kubernetes existe · 19.2 Pods, services e secrets · 19.3 Superfície de ataque do cluster | planejado |
| 20 | Cloud e IAM | 20.1 O modelo de responsabilidade compartilhada · 20.2 Identidades e políticas · 20.3 Menor privilégio na prática · 20.4 Buckets e dados expostos | planejado |

### Fase 5 — Fundamentos de segurança

Ao fim: pensa como atacante e como defensor sobre qualquer sistema que vê.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 21 | Pensar em segurança | 21.1 Confidencialidade, integridade e disponibilidade · 21.2 Ativos, ameaças e riscos · 21.3 Fronteiras de confiança | planejado |
| 22 | Modelagem de ameaças | 22.1 Diagrama de fluxo de dados · 22.2 STRIDE · 22.3 Priorizar riscos | planejado |
| 23 | Identidade | 23.1 Autenticação vs autorização · 23.2 Senhas e hash · 23.3 Sessões e tokens · 23.4 OAuth e OIDC · 23.5 MFA | planejado |
| 24 | Criptografia aplicada | 24.1 Hash · 24.2 Simétrica · 24.3 Assimétrica e assinatura · 24.4 Erros comuns de cripto | planejado |
| 25 | Segredos | 25.1 Onde segredos vazam · 25.2 Cofres de segredo · 25.3 Rotação e resposta a vazamento | planejado |

### Fase 6 — Segurança de aplicações

Ao fim: encontra, explora em laboratório e corrige as vulnerabilidades mais comuns em
aplicações web.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 26 | Injeção | 26.1 Dado que vira comando · 26.2 SQL injection · 26.3 Command injection · 26.4 A correção certa | planejado |
| 27 | Controle de acesso | 27.1 IDOR · 27.2 Escalada horizontal e vertical · 27.3 Autorização no lugar certo | planejado |
| 28 | Ataques no navegador | 28.1 Same-origin policy · 28.2 XSS · 28.3 CSRF · 28.4 CORS | planejado |
| 29 | SSRF e confiança no servidor | 29.1 O servidor como intermediário · 29.2 SSRF · 29.3 Metadados de cloud | planejado |
| 30 | Supply chain de software | 30.1 Dependências · 30.2 Pacotes maliciosos · 30.3 SBOM e assinatura | planejado |
| 31 | Revisão de código e testes de segurança | 31.1 Code review com olho de atacante · 31.2 SAST · 31.3 DAST · 31.4 Pentest de uma aplicação | planejado |

### Fase 7 — Defesa e operação

Ao fim: monta a visibilidade de um sistema, detecta um ataque nos logs e conduz a
resposta.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 32 | Logs e observabilidade | 32.1 O que registrar · 32.2 Centralizar logs · 32.3 Logs que vazam dados | planejado |
| 33 | Detecção | 33.1 Do log ao alerta · 33.2 Escrever uma regra de detecção · 33.3 Falso positivo e falso negativo | planejado |
| 34 | Resposta a incidentes | 34.1 O ciclo de resposta · 34.2 Contenção e evidência · 34.3 Pós-incidente | planejado |
| 35 | Hardening | 35.1 Linux · 35.2 Containers · 35.3 Rede e firewall | planejado |

### Fase 8 — Segurança na era da IA

Ao fim: entende os riscos de sistemas com LLMs e agentes, ataca e protege um agente em
laboratório, e usa IA a favor da defesa.

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 36 | Como um LLM funciona | 36.1 Tokens e contexto · 36.2 Por que o modelo não separa instrução de dado · 36.3 Alucinação e confiança | planejado |
| 37 | Prompt injection | 37.1 Injeção direta · 37.2 Injeção indireta: o documento que manda · 37.3 Por que não existe filtro perfeito · 37.4 Mitigações por arquitetura | planejado |
| 38 | Agentes, tools e MCP | 38.1 O que um agente pode fazer · 38.2 Excesso de autonomia · 38.3 Permissões e sandbox · 38.4 MCP: servidores e confiança | planejado |
| 39 | Dados e modelos | 39.1 Vazamento de dados pelo LLM · 39.2 Envenenamento de dados · 39.3 Supply chain de modelos e plugins (inclusive este) | planejado |
| 40 | IA a favor da defesa | 40.1 Triagem de alertas com IA · 40.2 Revisão de código com IA · 40.3 Os limites: quando não confiar | planejado |

### Projeto final

| # | Módulo | Lições | Situação |
|---|--------|--------|----------|
| 41 | Projeto final | 41.1 Construir uma aplicação com um agente · 41.2 Modelar as ameaças · 41.3 Atacar · 41.4 Corrigir e escrever o relatório | planejado |
