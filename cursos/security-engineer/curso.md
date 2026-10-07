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

## Eixos e diagnóstico

Eixos do curso e a escada de perguntas de cada um. Como usar a escada está em
`<raiz>/skills/mentor/references/niveis.md`.

| Eixo | Fases da trilha |
|------|-----------------|
| Sistemas | 1. A máquina |
| Redes | 2. A rede |
| Construir com IA | 3. Construir com IA |
| Infraestrutura | 4. Arquitetura e infraestrutura |
| Segurança | 5 a 8, e o projeto final |

### Sistemas

- **R:** O que é um processo?
  - Camada 2: um programa em execução, com memória e recursos próprios.
- **M:** Você dá dois cliques num programa. O que acontece dentro do computador até a
  janela aparecer? Conte do jeito que souber.
  - Camada 3: o arquivo sai do disco para a memória, o sistema operacional cria o
    processo e divide a CPU e a memória entre ele e os outros. Com as palavras dele.
- **D:** Um programa que funcionava ontem hoje diz "permissão negada" ao abrir um arquivo.
  Onde você investiga, e como resolveria sem liberar o arquivo para todo mundo?
  - Camada 4: hipóteses concretas: o dono e as permissões do arquivo mudaram, o programa
    roda com outro usuário, o caminho mudou.
  - Camada 5: dar a permissão só a quem precisa, e por que liberar para todos ou rodar
    como administrador custa caro.
- **D2:** Um programa fica cada vez mais lento até travar a máquina, e só volta ao normal
  depois de reiniciar. Onde você investiga, e o que faria?
  - Camada 4: olha o uso de memória e de CPU do processo ao longo do tempo e suspeita de
    vazamento de memória ou de um processo que se multiplica.
  - Camada 5: compara reiniciar o programa periodicamente, limitar a memória dele e
    corrigir a causa, e o custo de cada um.

### Redes

- **R:** O que é um endereço IP?
  - Camada 2: o endereço que identifica uma máquina na rede, para os dados chegarem a ela.
- **M:** Você digita o endereço de um site e aperta Enter. Como o computador descobre
  para onde mandar o pedido, e o que volta?
  - Camada 3: o nome vira um IP (DNS), o computador abre uma conexão com aquele IP e
    manda um pedido HTTP, o servidor devolve a página.
- **D:** O site abre quando você digita o IP, mas não abre pelo nome. Onde você procura o
  problema, e qual correção escolheria?
  - Camada 4: o problema está na tradução do nome: o servidor DNS configurado, o cache, ou
    um arquivo `hosts` que sobrescreve o nome.
  - Camada 5: compara as correções, como trocar o DNS, limpar o cache ou editar o `hosts`,
    e o custo de cada uma.
- **D2:** Seu computador acessa sites normalmente, mas não consegue acessar a impressora
  da rede de casa. Onde você procura, e o que mudaria?
  - Camada 4: hipóteses na rede local: a impressora mudou de IP, está em outra rede, ou
    um firewall bloqueia.
  - Camada 5: compara fixar o IP da impressora, reservar no roteador ou usar o nome, e o
    custo de cada um.

### Construir com IA

- **R:** O que é uma função num programa?
  - Camada 2: um trecho de código com nome, que recebe entradas, faz uma tarefa e
    devolve um resultado.
- **M:** Você pede ao Claude um script que lê um arquivo e conta as linhas. Antes de
  rodar, como você confere que ele faz o que você pediu?
  - Camada 3: ler o código e achar a parte que conta, prever a saída para um arquivo que
    ele conhece, e testar com esse arquivo.
- **D:** O script funciona no seu arquivo, mas quebra no arquivo de um colega. Como você
  acha a causa, e você corrige o código ou pede de novo à IA? Por quê?
  - Camada 4: comparar as duas entradas (arquivo vazio, codificação, quebra de linha,
    caminho) e reproduzir o erro com a menor entrada possível.
  - Camada 5: corrigir entendendo a causa, ou pedir de novo dizendo a causa à IA, e o
    risco de pedir de novo sem saber a causa.
- **D2:** A IA escreveu uma função que funciona, mas você não entende uma parte dela. O
  código vai para produção amanhã. O que você faz?
  - Camada 4: isola o trecho e testa com entradas para ver o que ele faz de verdade.
  - Camada 5: decide entre reescrever de um jeito que entende, pedir explicação e
    conferir, ou atrasar a entrega, e o risco de cada um.

### Infraestrutura

- **R:** O que é um container?
  - Camada 2: um jeito de empacotar e rodar uma aplicação isolada, com tudo de que ela
    precisa.
- **M:** Qual a diferença entre uma máquina virtual e um container? O que cada um isola?
  - Camada 3: a máquina virtual tem um sistema operacional inteiro sobre um hipervisor; o
    container compartilha o kernel da máquina e isola os processos e os arquivos.
- **D:** Uma aplicação num container precisa da senha do banco de dados. Onde você guarda
  essa senha, e o que muda se alguém invadir o container?
  - Camada 4: os lugares onde a senha vaza: dentro da imagem, no código, em variável de
    ambiente visível, no log.
  - Camada 5: compara variável de ambiente, arquivo montado e cofre de segredos, e diz o
    estrago de cada um se o container for invadido.
- **D2:** Uma aplicação funciona na sua máquina mas não no servidor. Os dois rodam o
  mesmo container. Onde você procura?
  - Camada 4: o que está fora da imagem: variáveis de ambiente, volumes, rede, a versão do
    kernel ou a arquitetura do processador.
  - Camada 5: compara levar a configuração para a imagem ou mantê-la fora, e o custo de
    cada um.

### Segurança

- **R:** O que é uma vulnerabilidade?
  - Camada 2: uma falha num sistema que alguém pode usar para fazer o que não devia.
- **M:** Um site tem login. Como alguém poderia entrar na conta de outra pessoa sem saber
  a senha dela?
  - Camada 3: um caminho concreto, explicado: roubar a sessão (o cookie), reaproveitar
    uma senha vazada de outro site, enganar a pessoa com phishing, ou uma falha que deixa
    ver a conta de outro mudando um número no endereço.
- **D:** O chatbot de uma empresa lê os e-mails dos clientes e pode enviar respostas.
  Que risco isso cria, e como você reduziria sem desligar o chatbot?
  - Camada 4: um e-mail pode trazer instruções que o modelo obedece (prompt injection
    indireta) e fazer o chatbot vazar dados ou mandar o que não devia.
  - Camada 5: mitigação pela arquitetura, como aprovação humana antes de enviar, só as
    permissões necessárias e separar o que é dado do que é instrução, com o custo de cada.
- **D2:** Um funcionário recebe um e-mail do "suporte" pedindo para instalar um programa.
  Ele instalou. O que você investiga primeiro, e o que faz agora?
  - Camada 4: o que o programa fez: processos, conexões de rede, contas usadas, o que
    ele alcançou na máquina e na rede.
  - Camada 5: compara isolar a máquina, trocar as senhas e investigar antes, e o custo de
    cada ordem.

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
