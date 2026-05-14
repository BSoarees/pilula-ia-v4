# 💊 Pílula de IA — Dose #1

**Data:** 2026-05-05
**Tema:** Skills, MCPs, APIs, Agentes & Engenharia de Prompt
**Formato:** Recap publicado no grupo do WhatsApp

---

## Mensagem publicada no grupo

Galera, saiu a primeira dose da nossa **Pílula de IA semanal**! 🤖

Tema de estreia: **Skills, MCPs, APIs, Agentes e Engenharia de Prompt** — os 5 pilares que sustentam qualquer automação inteligente de verdade.

**O que rolou:**

🧩 **Skills** — pacotes de conhecimento especializado que a IA carrega sob demanda (ex.: `conciliacao-bancaria`, `sap-s4hana`). Cada skill é uma "expertise" plugável: quando o contexto pede, ela entra em cena.

🔌 **MCPs (Model Context Protocol)** — a "tomada universal" que conecta a IA direto às ferramentas (Supabase, n8n, Gmail, Drive, etc.). Em vez de copiar/colar dados, o modelo lê e age na fonte.

🌐 **APIs** — a camada que permite a IA conversar com sistemas externos (SAP, gateways, plataformas de venda). É o "braço executor" que tira a IA do chat e leva pra dentro do processo.

🤖 **Agentes** — a junção de tudo: skills + MCPs + APIs orquestrados pra executar tarefas de ponta a ponta com autonomia (ex.: ler e-mail → extrair NF → conciliar com contas a pagar → registrar no SAP).

✍️ **Engenharia de Prompt** — a habilidade de *falar com a IA do jeito certo*. Não é mágica, é método: persona, objetivo, regras, exemplos e formato de saída. Um bom prompt é a diferença entre uma resposta genérica e um resultado pronto pra produção.

### 🎯 Anatomia de um bom prompt

```
[PERSONA]
Você é um analista financeiro sênior da V4 Company,
especialista em conciliação entre gateway e SAP.

[OBJETIVO]
Analisar a planilha de vendas do EasyFlow e identificar
transações que não bateram com o extrato bancário do dia.

[REGRAS]
- Considerar divergência apenas valores acima de R$ 1,00
- Ignorar estornos já marcados como "REFUND"
- Agrupar por método de pagamento (PIX, Cartão, Boleto)
- Nunca inventar dados — se faltar informação, sinalizar

[EXEMPLO DE SAÍDA ESPERADA]
| Método | Qtd Divergências | Valor Total | Ação Sugerida |
|--------|------------------|-------------|---------------|
| PIX    | 3                | R$ 450,00   | Revisar D+1   |

[CONTEXTO]
Empresa: Staage (1420) | Data: 03/05/2026
```

📌 **Por que funciona:** a IA sabe *quem ela é*, *o que entregar*, *o que não pode fazer* e *como formatar* — eliminando 90% das idas e voltas.

### 💡 Bônus mostrado ao vivo: Skill `/ideia`

Uma skill que combina **ideação socrática** (expandir a ideia) + **sabatina implacável** (estressar antes de executar). Use quando bater aquele "tenho uma ideia, mas será que faz sentido?" — ela ajuda a validar antes de gastar energia construindo.

> 🚀 **Vou liberar a `/ideia` pra todos instalarem!** Em breve mando o passo a passo de instalação aqui no grupo.

### 📌 Tarefas pra próxima dose

1. ⬇️ Baixar o **Antigravity** (Google) — https://antigravity.google
2. ⬇️ Baixar o **Claude** (Desktop App) — https://claude.ai/download

> Chega na #2 com as duas ferramentas já instaladas pra gente colocar a mão na massa juntos. 🛠️

### 💊 Próxima dose — Banco de Dados & Front-End

Como conectar IA ao seu banco (Supabase/Postgres) e gerar interfaces de verdade — do schema à tela funcional.

**Princípio que guia tudo:**
> Pessoas decidem, Máquinas executam, IA analisa.

Bora pra cima! 💪

---

## Material de apoio enviado

### Instalação da Skill `/ideia`

Arquivo `SKILL.md` disponibilizado em `~/Downloads/SKILL.md` para envio no grupo.

**Passo a passo divulgado:**

1. Pegar o `SKILL.md` (anexo no grupo)
2. Criar a pasta:
   - Windows: `C:\Users\SEU_USUARIO\.claude\skills\ideia\`
   - Mac/Linux: `mkdir -p ~/.claude/skills/ideia`
3. Colar o `SKILL.md` dentro da pasta
4. Reiniciar o Claude Desktop
5. Testar: `/ideia tenho uma ideia de automatizar o fechamento mensal`

---

## Notas internas (não publicadas)

- Skill canônica em: `~/.claude/skills/ideia/SKILL.md`
- Próxima dose deve mostrar Antigravity + Claude juntos (banco + front-end)
- Considerar: criar uma `dose-02-tarefas.md` com checklist de quem instalou as ferramentas