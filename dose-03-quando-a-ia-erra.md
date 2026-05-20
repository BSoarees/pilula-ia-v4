# 💊 Pílula de IA — Dose #3

**Data:** 2026-05-20
**Tema:** Quando a IA erra — por que a base de dados é a fonte da verdade
**Formato:** Recap publicado no grupo do WhatsApp

---

## Mensagem publicada no grupo

Galera, saiu a **Dose #3** da Pílula! 💊🤖

Tema de hoje: **Quando a IA erra** — e por que você PRECISA olhar pra base de dados antes de confiar.

### ⚠️ A IA não erra "às vezes". Ela erra com confiança.

O problema não é a IA inventar algo absurdo que você percebe na hora. O problema é quando ela inventa algo **plausível** — um número que parece certo, um CNPJ que tem o formato correto, um fornecedor que "faz sentido". Aí você usa, manda pro SAP, e só descobre o erro no fechamento.

> Isso tem nome: **alucinação**. A IA gera texto estatisticamente provável, não necessariamente verdadeiro.

### 🧪 Exemplos reais de onde a IA escorrega no financeiro

**1. Fornecedor fantasma**
Você pede: *"lista os 10 maiores fornecedores da empresa no Q1"*
A IA não tem acesso à base → ela **inventa nomes que parecem reais**. "Distribuidora Nacional Ltda" soa legítimo, mas não existe no seu cadastro de Business Partners no SAP.

**2. NF com valor "arredondado"**
Você joga uma foto de NF e pede pra extrair os dados. A IA lê R$ 14.832,**50** mas o valor real é R$ 14.832,**57**. Diferença de centavos? No fechamento de 500 NFs, vira divergência no SPED.

**3. CNPJ com formato certo mas número errado**
A IA sabe que CNPJ tem 14 dígitos e formatação XX.XXX.XXX/XXXX-XX. Então ela gera um que **parece** válido. Mas os dígitos verificadores não batem — e o SAP rejeita na hora de cadastrar o BP.

**4. Cálculo de imposto "criativo"**
Você pergunta: *"qual a alíquota de ISS pra esse serviço?"*
A IA responde 5% com toda confiança. Mas a alíquota do seu município é 2,5%. Ela pegou a **alíquota máxima permitida**, não a real.

### 🔍 A regra de ouro: Base de Dados > Output da IA

A IA é uma **assistente de análise**, não uma **fonte de dados**. A fonte é sempre:

- O **SAP** (cadastro de BPs, saldos, lançamentos)
- O **extrato bancário** (conciliação real)
- A **NF original** (XML, não foto)
- O **Supabase/banco de dados** (registros validados)

**Fluxo correto:**

```
IA gera output → Você confere na base → Bateu? Usa. Não bateu? Corrige.
```

**Fluxo perigoso:**

```
IA gera output → Você confia → Manda pro SAP → Erro no fechamento → Retrabalho
```

### 🛡️ 3 técnicas pra não cair em alucinação

**1. Sempre dê a fonte**
Não pergunte "quais são meus fornecedores" — **anexe a planilha** ou **conecte ao banco**. IA com dados reais alucina muito menos que IA no vácuo.

**2. Peça pra IA citar de onde tirou**
Inclua no prompt: *"cite a linha exata do arquivo / registro de onde veio cada dado"*. Se ela não conseguir apontar a fonte, é sinal de que inventou.

**3. Teste com um dado que você já sabe a resposta**
Antes de confiar num resultado novo, jogue uma pergunta que você **já sabe a resposta**. Se a IA acertar, bom sinal. Se errar, você sabe que o contexto tá fraco.

### 🛠️ Debug ao vivo

_[Nesta sessão, abrimos os `.md` que o grupo trouxe e debugamos prompts ao vivo — detalhes em breve]_

### 📌 Tarefas pra Dose #4

1. 🔍 **Testar a técnica do "dado conhecido"** — perguntar algo que você já sabe a resposta e ver se a IA acerta
2. 📎 **Na próxima vez que usar IA no trabalho**: conferir pelo menos 1 dado no SAP/banco antes de usar o output
3. 💡 **Trazer um caso** onde a IA errou (ou onde você quase usou um dado errado) — vamos montar um "mural de alucinações" da V4

> Dose #4 vai aprofundar: como **conectar a IA direto na base de dados** pra ela parar de adivinhar e começar a consultar. 🔌

**Princípio que guia tudo:**
> Pessoas decidem, Máquinas executam, IA analisa.

Bora pra cima! 💪

---

## Notas internas (não publicadas)

### Pontos que rolaram na sessão mas não viraram mensagem

_[preencher após a gravação]_

### Action items por pessoa

_[preencher após a gravação]_

### Decisões técnicas registradas

- Output de IA sempre validar contra fonte primária (SAP, extrato, XML da NF)
- IA sem acesso a dados = alto risco de alucinação — sempre alimentar com arquivo/conexão

### Ideias pra próxima dose

- Conectar IA direto ao banco (Supabase/MCP) — eliminar o "vácuo" que causa alucinação
- Mostrar consulta real: IA pergunta pro banco ao invés de inventar
- Criar checklist padrão de validação pós-IA pro time financeiro
