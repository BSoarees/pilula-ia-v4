# 💊 Pílula de IA — Dose #2

**Data:** 2026-05-13
**Tema:** Contexto — como manter a memória da IA viva entre conversas
**Formato:** Recap publicado no grupo do WhatsApp

---

## Mensagem publicada no grupo

Galera, saiu a **Dose #2** da Pílula! 💊🤖

Tema de hoje: **Contexto**. Aquilo que separa uma IA que "esqueceu tudo" de uma IA que continua de onde parou.

### 🧠 O que é contexto, afinal?

É o conjunto de informações que a IA carrega na cabeça durante uma conversa. Quanto mais contexto certo, melhor a entrega. Igual a SAP: quem conhece as telas executa mais rápido — a IA é a mesma coisa.

### 📏 A janela de 1 milhão de tokens

Cada chat tem um limite: **1 milhão de tokens** (~200 mil caracteres no Claude). Quando estoura, o chat trava e você precisa abrir outro. Aí mora o problema: **se você não salvou o contexto, perdeu tudo.**

> Exemplo real: o projeto Fusame consumiu 877 mil tokens só na **fase 1** de 5. Sem estratégia, eu teria que explicar tudo de novo na fase 2.

### 📄 A solução: arquivos `.md` como cérebro externo

O `.md` (Markdown) é o formato que a IA lê mais rápido e gasta menos token que `.txt` ou Excel. Ele vira o **"cérebro" das suas conversas**.

**O fluxo é simples:**

1. Antes de fechar um chat importante: peça pra IA gerar um `.md` com o contexto
2. Salve numa pasta no seu PC (de preferência no disco `C:\`, primeiro nível — facilita a indexação)
3. No próximo chat: anexe o `.md` ou aponte a pasta — a IA "lembra" tudo

### 🛠️ Por que baixar o Antigravity + Claude Desktop

Com os dois rodando local, a IA **manipula sua pasta diretamente**: cria, renomeia, deleta, lê arquivos. Demonstrei ao vivo criando uma pasta `BARBAREX`, renomeando pra `KICKMONSTRAO` e deletando — tudo via comando direto pro Claude.

> Mais que isso: dá pra configurar **salvamento automático de contexto** ao final das sessões. Vira um diário do seu projeto.

### 🔁 Contexto + Skill + Conector = automação completa

Foi o que rolou na prática com a planilha de compras da Bárbara:

- **Contexto** = o que precisa ser feito (relatório de 2 fornecedores, valores e quantidade, **uma única aba**)
- **Skill** = como executar a tarefa recorrente
- **Conector (MCP Google Drive)** = a ferramenta que lê os PDFs direto da pasta

Resultado: IA leu as notas no Drive, identificou produtos e calculou totais — sem script, sem Python, sem robô.

### ⚠️ Lição da prática de hoje

A primeira tentativa da Bárbara virou uma planilha gigante com 8 abas porque **faltou contexto + exemplo de saída**. A correção foi simples:

> "Não quero uma planilha cheia de abas. Quero **um relatório simples, em uma única aba**, com quantidade e valor dos fornecedores X e Y."

Moral: **persona + objetivo + exemplo de saída** continua sendo a regra de ouro (lembra da Dose #1?).

### 📌 Tarefas pra Dose #3

1. 🛠️ **Praticar** o salvamento de contexto em `.md` ao longo da semana
2. 📝 **Trazer um `.md` com um problema real** — alguma tarefa que vocês tentaram fazer com IA e não saiu como queriam. Vamos **abrir ao vivo** na próxima dose e arrumar juntos
3. ⬇️ Quem ainda não baixou: **Antigravity** + **Claude Desktop** (links na Dose #1)

> Próxima dose vai ser **100% mão na massa**. Cada um traz seu `.md`, a gente debuga o prompt, ajusta o contexto e faz funcionar ao vivo. 🛠️

**Princípio que guia tudo:**
> Pessoas decidem, Máquinas executam, IA analisa.

Bora pra cima! 💪

---

## Notas internas (não publicadas)

### Pontos que rolaram na sessão mas não viraram mensagem

- TV da sala queimou no meio da aula (Mateus apertando botão) — Bárbara vai cotar TV nova
- Discussão sobre Claude no Antigravity — categoria correta: **conector**, não MCP (é uma extensão do Antigraph)
- Permissão de Drive corporativo bloqueou listagem de arquivos pelo Claude → resolvido com **"qualquer pessoa com o link"** (atenção: revisar se é OK pra notas fiscais reais)
- Caso Ariel das notas fiscais (200 NFs) — usado como exemplo de "às vezes MCP vence robô" pela simplicidade

### Action items por pessoa

- **Gabriela Santos** — configurar Claude + Antigravity no computador pessoal
- **Bárbara** — cotar TV nova pra sala de reuniões
- **Grupo todo** — criar `.md` com problema/dificuldade real até a Dose #3
- **Grupo todo** — instalar Antigravity (quem ainda não tem)

### Decisões técnicas registradas

- Padrão da casa: relatórios consolidados **em uma única aba**, não múltiplas abas-dashboard
- Disco `C:\` no primeiro nível como local padrão pra pastas indexáveis pela IA
- `.md` é o formato preferido pra contexto (mais leve, formatação preservada, menos tokens que `.txt` ou tabela)

### Ideias pra próxima dose

- Abrir os `.md` de problemas que o grupo trouxer e debugar **prompt por prompt**
- Mostrar como gerar uma **skill** a partir de uma tarefa recorrente (ex.: a planilha de compras da Bárbara virar `skill compras-mensal`)
- Demonstrar criação de robô via Claude (Augusto pediu) — caso CL/CEG sem API
- Considerar mostrar **conector MCP Google Drive** já configurado no Claude Desktop
