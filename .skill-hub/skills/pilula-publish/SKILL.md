---
name: pilula-publish
description: Publica uma nova dose da Pílula de IA (treinamento interno V4 Company) no playbook online. Use quando o Bernardo trouxer o resumo do Gemini de uma gravação da Pílula e pedir "publica a próxima dose", "monta a dose X", "atualiza o playbook" ou similar. Gera o .md da dose, atualiza o index.html visual (TOC + nova article), atualiza README, commita e dá push — em ~30s a nova dose está no ar em https://bsoarees.github.io/pilula-ia-v4/.
---

# Pílula Publish — Automação da publicação semanal

## Contexto

A **Pílula de IA** é um treinamento interno semanal da V4 Company conduzido pelo Bernardo. Cada aula vira uma "dose" registrada num playbook visual online, atualizado semanalmente.

- **Repo público:** https://github.com/BSoarees/pilula-ia-v4
- **URL pública (GitHub Pages):** https://bsoarees.github.io/pilula-ia-v4/
- **Pasta local:** `~/Maestro/Pilula/`
- **Deploy:** automático via GitHub Pages após `git push origin main` (~30s)

Antes desta skill existir, cada dose nova exigia: ler transcrição do Gemini → escrever .md → editar index.html à mão (TOC + nova article) → atualizar README → commit + push. **Esta skill faz tudo isso a partir do resumo do Gemini.**

## Input esperado

O Bernardo cola/anexa o **resumo do Gemini da gravação**. Formato típico:

```
# Observações
[data]
## [Nome do evento]
### Resumo
[3-4 parágrafos do que rolou]
### Próximas etapas
- [ ] [Pessoa] [Tarefa]
### Detalhes
* **Tópico 1**: descrição com timestamp ([HH:MM:SS]).
* **Tópico 2**: ...
# Transcrição
[transcrição completa, muito ruído conversacional]
```

**Importante:** o Gemini gera muito ruído (TV pifando, conversa paralela, problemas técnicos). A skill deve **filtrar o sinal**: focar nos tópicos didáticos da seção "Detalhes" e ignorar conversa paralela.

## Passos da execução

### 1. Confirmar contexto da dose

Antes de gerar, perguntar (ou inferir do conteúdo):
- **Número da dose** — inferir do último arquivo `dose-XX-*.md` em `~/Maestro/Pilula/` (próximo número)
- **Data da aula** — extrair do header do resumo Gemini
- **Tema** — extrair da pauta / seção que ficou repetida nos tópicos (ex.: "contexto", "banco de dados", "front-end")
- **Slug** — kebab-case curto pra nome do arquivo (ex.: `contexto`, `banco-frontend`)

### 2. Gerar `dose-XX-slug.md`

Seguir EXATAMENTE o padrão da `dose-02-contexto.md` (em `~/Maestro/Pilula/`):

```markdown
# 💊 Pílula de IA — Dose #XX

**Data:** YYYY-MM-DD
**Tema:** Título da dose
**Formato:** Recap publicado no grupo do WhatsApp

---

## Mensagem publicada no grupo

[Mensagem de WhatsApp curta-média, didática, com emojis,
linguagem do Bernardo: direta, pragmática, "tá ligado"
quando informal mas sempre profissional. Sempre fecha com
o princípio "Pessoas decidem · Máquinas executam · IA analisa."]

### Tarefas pra Dose #XX+1
1. ...

---

## Notas internas (não publicadas)

### Pontos que rolaram na sessão mas não viraram mensagem
- [Caso engraçado / problema técnico / contexto da equipe]

### Action items por pessoa
- **[Nome]** — [tarefa]

### Decisões técnicas registradas
- [Decisão]

### Ideias pra próxima dose
- [Ideia]
```

### 3. Atualizar `index.html` (HTML do playbook)

Três mudanças no arquivo `~/Maestro/Pilula/index.html`:

**3a. Adicionar card no TOC:**
- Encontrar o último `<a href="#dose-N" class="toc-card ...">` ou o `<div class="toc-card planned">` (Dose futura/planejada)
- Inserir card da nova dose **antes** do card "planned"
- Atualizar card "planned" pra apontar pra dose+1

Cores alternadas:
- Dose ímpar: `class="toc-card"` (laranja terracota)
- Dose par: `class="toc-card blue"` (azul tinta)

**3b. Inserir nova `<article class="dose">`:**
- Inserir antes do `<!-- ============ TASKS ============ -->`
- Estrutura espelho da `<article class="dose" id="dose-2">`
- ID = `dose-N`, num = `Dose #N`
- Data formatada em PT-BR ("13 de maio de 2026")
- Cor da blockquote/dose-num segue mesma alternância (par = azul)

**3c. Atualizar seção de tarefas:**
- Substituir bloco `<section class="tasks">` com as tarefas da nova dose

### 4. Atualizar `README.md`

- Adicionar linha na tabela "Histórico de Doses"
- Atualizar título da próxima dose planejada (XX+1)
- Substituir bloco "Tarefas Abertas (pra Dose #XX+1)"

### 5. Commit + push

```bash
cd ~/Maestro/Pilula
git add -A
git -c user.email="despesas@v4company.com" -c user.name="Bernardo Soares" commit -m "feat: Dose #XX — Tema

[1-2 linhas resumindo a aula]

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>"
git push origin main
```

### 6. Validar deploy

Esperar ~30s, depois confirmar HTTP 200:

```powershell
Invoke-WebRequest -Uri "https://bsoarees.github.io/pilula-ia-v4/" -UseBasicParsing -Method Head
```

Retornar pro Bernardo: URL + link direto pra nova dose (`#dose-N` anchor).

## Regras de estilo

### Voz do Bernardo na mensagem do grupo
- Direta, prática, sem floreio
- Emojis técnicos com moderação (🧠 🔌 📄 🛠️ 🤖 💡 📌)
- Headers em H3 com emoji + termo + travessão + complemento
- `code inline` pra nomes de skills/tools/comandos
- Blockquotes pra reforçar lição-chave
- **Negrito** em termos-chave, não em frases inteiras
- *Itálico* pra ênfase suave / aspas implícitas
- Sempre fecha com o princípio + chamada à ação ("Bora pra cima! 💪")

### Filtragem de ruído da transcrição Gemini
**Ignorar:**
- Problemas técnicos da sala (TV, internet, áudio)
- Conversa paralela (saúde, ponto, fofoca interna)
- Comentários sobre nomes próprios de pessoas ausentes
- Repetições por causa de áudio cortado

**Capturar:**
- Conceitos novos explicados
- Exemplos práticos demonstrados ao vivo
- Erros corrigidos durante a aula (lição prática)
- Decisões de prática que ficaram pra próxima
- Tarefas concretas atribuídas (sem mencionar nomes pessoais nas tarefas públicas — usar "Todos do grupo")

### Tarefas públicas (visíveis no playbook) vs internas
**Públicas (mensagem + index.html + README):**
- Coisas que todo mundo precisa fazer ("praticar X", "baixar Y")
- Tarefas conceituais coletivas

**Internas (só no .md da dose, seção "Notas internas"):**
- Action items individuais com nome (Bárbara cotar TV, Gabriela configurar PC)
- Decisões pessoais do Bernardo
- Detalhes operacionais da empresa

## Troubleshoot

- **`git push` falha por not-fast-forward** → outro lugar deu push (raro neste repo); `git pull --rebase` antes do push.
- **GitHub Pages não atualiza** → checar `gh api repos/BSoarees/pilula-ia-v4/pages -q '.status'` (deve ser `built`). Se `building`, esperar; se `errored`, ver `gh api repos/BSoarees/pilula-ia-v4/pages/builds/latest`.
- **Card TOC quebra layout** → verificar se classes `.blue` / sem-classe estão alternando corretamente; cada par muda cor.
- **Resumo Gemini vem sem timestamps** → seguir os tópicos da seção "Detalhes" mesmo assim — a estrutura conceitual já está lá.
- **Resumo Gemini só veio em formato txt** → tratar como markdown, parsear seções por headers e bullets normalmente.

## Comandos rápidos

```bash
# Próximo número de dose
ls ~/Maestro/Pilula/dose-*.md | wc -l

# Diff do que vai pra produção
cd ~/Maestro/Pilula && git diff HEAD

# Status do último build do Pages
gh api repos/BSoarees/pilula-ia-v4/pages -q '.status'

# Forçar rebuild do Pages (caso necessário)
gh api repos/BSoarees/pilula-ia-v4/pages/builds -X POST
```

## Limites e não-fazer

1. **Não publicar nomes individuais em tarefas públicas** — quem aparece com nome próprio é só na seção "Notas internas" do .md.
2. **Não inventar conteúdo** — se o resumo Gemini for ralo, mostrar pro Bernardo o esboço e perguntar o que falta antes de publicar.
3. **Não trocar a estética do `index.html` sem pedir** — cores, fontes e layout são fixos (Fraunces + Inter + JetBrains Mono, paleta papel/terracota/azul tinta).
4. **Não pular o `git push`** — sem push, deploy não acontece. Sempre validar com HTTP 200 no final.

## Histórico

- **2026-05-14** — Skill criada após Dose #2 (Contexto). Repo `pilula-ia-v4` criado público em `BSoarees`. GitHub Pages habilitado branch `main` path `/`.