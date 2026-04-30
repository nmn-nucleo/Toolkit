# Aba 9 — Custos & Planos

## Quanto sai do bolso, em reais

---

## INTRO (topo da aba)

### Eyebrow
> Calculadora + comparativo + cenarios reais

### Titulo principal
> # Sem dolar virando susto. Calculo em real, com cenario seu.

### Lead paragraph
Conteudo gringo cota custo em dolar e nao serve pra voce planejar. Esta aba traduz tudo pra **reais**, com cenarios reais (estudante, freelancer, time pequeno, projeto pesado), comparativo Claude Code vs Codex, e calculadora interativa pra estimar custo mensal antes de assinar.

### Atualizacao
> Ultima revisao de precos: **abril 2026**. Cambio de referencia: **R$ 5,40 / USD**. Confira valores atuais no checkout do provider.

---

## SECAO 1 — Os planos hoje (lado a lado)

### Anthropic — Claude Code

| Plano | Preco USD | Preco R$ (~5,40) | Limites principais |
|---|---|---|---|
| **Pro** | $20/mes | ~R$ 108/mes | Sonnet 4.6 + uso moderado de Opus 4.7. Limites diarios. Adequado pra uso pessoal. |
| **Max 5x** | $100/mes | ~R$ 540/mes | 5x o uso do Pro. Acesso priorizado a Opus 4.7. |
| **Max 20x** | $200/mes | ~R$ 1.080/mes | 20x o uso do Pro. Limites altos pra trabalho profissional intensivo. |
| **API** | Pay-per-token | Variavel | Sonnet 4.6: ~$3/$15 por M tokens (input/output). Opus 4.7: ~$15/$75. |

### OpenAI — Codex

| Plano | Preco USD | Preco R$ (~5,40) | Limites principais |
|---|---|---|---|
| **ChatGPT Plus** | $20/mes | ~R$ 108/mes | Codex incluso. GPT-5.4 com limites moderados. |
| **ChatGPT Pro** | $200/mes | ~R$ 1.080/mes | Codex sem limite pratico, reasoning high, Codex Cloud incluso. |
| **API** | Pay-per-token | Variavel | GPT-5.4: ~$2/$8 por M tokens. |

### Comparativo direto

| | **Pro / Plus ($20)** | **Max 5x / (sem equivalente)** | **Max 20x / Pro ($200)** |
|---|---|---|---|
| **Claude Code** | Pro — Sonnet ilimitado moderado, Opus limitado | Max 5x — todos modelos, 5x uso | Max 20x — todos modelos, 20x uso |
| **Codex** | ChatGPT Plus — Codex incluso, limites moderados | (nao tem tier intermediario) | ChatGPT Pro — Codex sem limite pratico, Cloud incluso |

**Observacao:** Codex pula o tier intermediario. Voce paga $20 ou $200 — entre os dois nao ha opcao.

---

## SECAO 2 — Cenarios reais em R$

> 4 personas com uso tipico. Numero estimado, varia conforme intensidade.

### Cenario 1 — Estudante / hobbyista
**Perfil:** 1-2h por dia, projetos pessoais, aprendizado.

| Recomendacao | Custo mensal |
|---|---|
| **Codex via ChatGPT Plus** | **R$ 108/mes** |
| Alternativa: API pay-per-token (uso leve) | R$ 30-80/mes |

**Justificativa:** ChatGPT Plus inclui Codex + ChatGPT regular pra outras necessidades. Melhor custo-beneficio pra quem nao depende profissionalmente.

### Cenario 2 — Freelancer / dev solo
**Perfil:** 4-6h por dia, projetos pagos, varios clientes simultaneos.

| Recomendacao | Custo mensal |
|---|---|
| **Claude Code Max 5x** | **R$ 540/mes** |
| Alternativa: ChatGPT Plus + Claude Pro (combo) | ~R$ 216/mes |
| Alternativa frugal: Codex Plus + skills bem feitas | R$ 108/mes |

**Justificativa:** Max 5x da headroom suficiente pra trabalho profissional sem ansiedade de limite. Combo de dois Pro ($20 cada) custa ~metade e ainda permite revisao cruzada.

**Dica:** comece com combo Plus + Pro ($40 = R$ 216). Se sentir limitacao, sobe pra Max 5x.

### Cenario 3 — Time pequeno (3-5 devs)
**Perfil:** trabalho intensivo, multiplos projetos paralelos, codigo critico.

| Recomendacao | Custo mensal (time) |
|---|---|
| **Claude Code Max 20x (1 conta) + 4x Pro** | **R$ 1.080 + R$ 432 = R$ 1.512/mes** |
| Alternativa: 5x ChatGPT Pro (se fluxo predomina Codex) | R$ 5.400/mes (caro) |
| Alternativa hibrida: 2x Max 5x + 3x ChatGPT Plus | R$ 1.080 + R$ 324 = R$ 1.404/mes |

**Justificativa:** time precisa balancear conta principal forte (Max 20x pra codigo critico) + contas regulares pra dev individual. Codex Pro a $200 fica caro pra todo dev — usa em 1-2 contas-chave.

### Cenario 4 — Projeto critico (financeiro/saude/legal)
**Perfil:** codigo precisa de revisao cruzada, baixa tolerancia a bug, custo justifica qualidade.

| Recomendacao | Custo mensal |
|---|---|
| **Combo Claude Max 20x + Codex Pro (revisao cruzada)** | **R$ 1.080 + R$ 1.080 = R$ 2.160/mes** |
| Alternativa: API pay-per-token com uso controlado | Variavel (R$ 1.000-3.000) |

**Justificativa:** Claude escreve, Codex revisa (ou vice-versa). Custo dobra, qualidade tambem. **Bug em producao em projeto critico custa muito mais que R$ 1.080/mes.**

---

## SECAO 3 — Calculadora interativa de custo

> Componente JavaScript inline. 5 perguntas, resultado em R$ estimado.

### Como usar
Responde 5 perguntas e a calculadora estima seu custo mensal. Use como **referencia, nao previsao exata** — uso real varia.

### As 5 perguntas

**1. Quantas horas por dia voce usa o agente?**
- Menos de 1h
- 1-3h
- 3-6h
- Mais de 6h

**2. Que tipo de tarefa predomina?**
- Aprendizado / hobby (consultas, exemplos, codigo simples)
- Trabalho normal (features pequenas/medias, bug fix)
- Trabalho pesado (refactor grande, multi-arquivo, contexto longo)
- Critico (codigo de producao, revisao cruzada essencial)

**3. Voce ja sabe se prefere Claude ou Codex?**
- Claude (qualidade primaria)
- Codex (eficiencia/velocidade)
- Os dois (revisao cruzada)
- Recomendar pra mim

**4. Voce trabalha solo ou em time?**
- Solo
- Time pequeno (2-5)
- Time medio (6-15)
- Time grande (15+)

**5. Voce cobra pelo trabalho?**
- Nao (estudo / pessoal)
- Sim, freelance individual
- Sim, salario CLT
- Sim, empresa propria

### Resultado gerado

A calculadora cruza as respostas e retorna:
- **Plano recomendado** (com nome especifico)
- **Custo mensal estimado em R$**
- **Custo anual em R$**
- **ROI** (quanto economizou em horas vs custo) — se respondeu que cobra

> Exemplo de output:
> ```
> Pra voce, recomendamos: Claude Code Max 5x
> Custo mensal: R$ 540
> Custo anual: R$ 6.480
> ROI estimado: economiza ~40h/mes em produtividade.
>   Se voce cobra R$ 100/h: economia de R$ 4.000/mes vs custo de R$ 540 = 7.4x ROI
> ```

---

## SECAO 4 — Quando vale ter os dois (revisao cruzada)

> Bloco em destaque. Decisao financeira importante.

A pergunta nao e "qual escolher" — e "quando vale pagar pelos dois?"

### Vale pagar pelos dois quando...

#### 1. Voce trabalha em codigo critico
Bug em producao em sistema de pagamento, saude, juridico, ou qualquer area regulada custa **muito** mais que R$ 1.080/mes. Revisao cruzada (Claude escreve + Codex revisa) pega 53-80% mais bugs que solo.

#### 2. Voce cobra projetos premium
Cliente que paga R$ 30k pra entrega merece codigo revisado em pipeline de qualidade. Custo de R$ 2.160/mes vira 7% de **uma** entrega. Negocio.

#### 3. Voce esta em time profissional
Em time, voce nao pode arriscar bug por economia de R$ 1k/mes. Combo justifica facil.

#### 4. Voce e early adopter querendo entender ambos
Vale por 2-3 meses pra entender qual encaixa melhor no seu fluxo, depois decide.

### NAO vale pagar pelos dois quando...

#### 1. Voce esta comecando
Antes de pagar pelos dois, **domine um**. So o tempo de aprendizado dobra se voce divide foco.

#### 2. Tarefas sao simples / repetitivas
Codigo nao-critico, projeto pessoal, automacao basica — um agente sozinho da conta de sobra.

#### 3. Orcamento aperta
R$ 2.160/mes e dinheiro real. Se isso afeta seu orcamento mensal, **comeca com um plano basico e escala depois**.

---

## SECAO 5 — Hacks pra reduzir custo

### 1. Use API quando uso for irregular
Se voce usa muito em alguns dias e zero em outros, **API pay-per-token** pode sair mais barato que assinatura mensal. Calcula 2-3 meses de uso real antes de migrar pra plano fixo.

### 2. Skills bem feitas reduzem token
Cada skill bem documentada e cada CLAUDE.md/AGENTS.md curto economiza token em **toda** sessao. Investimento de 1h em skills boas paga em 1 mes.

### 3. /clear religiosamente
Sessao acumula contexto. Tarefa nova = `/clear`. Voce evita re-processar contexto antigo desnecessariamente.

### 4. Subagent pra trabalho pesado
Subagent tem contexto proprio. Pesquisa pesada nele nao polui (e nao consome token de) o agente principal.

### 5. /effort low ou reasoning="low" pra tarefa simples
Nao precisa "pensar profundo" pra renomear variavel. Reduz token em 30-50% sem perda de qualidade pra trabalho rotineiro.

### 6. Plan Mode antes de implementar
Custo: 1 prompt extra. Beneficio: evita 5-10 prompts de re-implementacao quando abordagem inicial estava errada.

### 7. Local enxuto + global enxuto
**O Globalzao custa caro**. Cada token de contexto carregado e token gasto antes do trabalho comecar. Audita seus skills regularmente.

---

## SECAO 6 — Comparativo de eficiencia (token por tarefa)

> Dados reais de benchmarks publicos.

| Tarefa | Claude Code (tokens) | Codex (tokens) | Diferenca |
|---|---|---|---|
| Bug fix simples | 50-100k | 15-40k | Codex 2-3x mais barato |
| Feature pequena | 200-400k | 50-150k | Codex 2.5-3x mais barato |
| Refactor medio | 800k-1.5M | 250-600k | Codex 2-3x mais barato |
| Clone Figma → React | 6.2M | 1.5M | Codex 4x mais barato |

**Trade-off:** Claude Code produz **output mais minucioso e completo**. Em avaliacoes cegas, vence 67% das comparacoes vs 25% do Codex (8% empate).

**Conclusao adulta:**
- **Codex:** mais eficiente em token. Otimo pra volume.
- **Claude Code:** mais minucioso. Otimo pra qualidade que justifica custo.

**Nem um nem outro e sempre melhor.** Depende do que voce esta fazendo.

---

## SECAO 7 — Custos invisiveis (que ninguem fala)

### Custo 1 — Tempo de aprendizado
Trocar de agente custa **30-60h** de re-aprendizado de fluxo. Se voce ja domina um, nao troca por causa de R$ 50/mes de diferenca. Mas se esta comecando, pega o que voce vai conseguir aprender mais rapido (geralmente Codex).

### Custo 2 — Bug em producao
Bug em codigo de IA aceito sem revisao custa **horas/dias** de debug + impacto em cliente. Vale a economia que ela trouxe? Sempre depende. Em codigo critico, **nunca**.

### Custo 3 — Re-trabalho por contexto inflado
Globalzao + sessao bagunçada custa em token **e** em qualidade. Voce paga 3x: token extra + retrabalho do output ruim + tempo seu corrigindo.

### Custo 4 — Plataform lock-in
Construir tudo em volta de uma ferramenta especifica e plataform lock. Se a empresa muda preco/politica, voce ta refem. **Por isso o metodo agnostico** — voce migra de provider sem refazer setup.

---

## SECAO 8 — Recomendacao final do Get It Easy

> Resumo executivo das nossas recomendacoes financeiras.

### Comecando do zero (orçamento R$ 100-200/mes)
**ChatGPT Plus (R$ 108)** ou **Claude Code Pro (R$ 108)** — escolhe um. Comeca, aprende. Em 2-3 meses voce vai saber se ficou bom ou se precisa subir.

### Profissional / freelance (orçamento R$ 200-600/mes)
Combo **Claude Pro + Codex Plus (R$ 216)** ou **Claude Code Max 5x (R$ 540)**. Combo da revisao cruzada, Max 5x da headroom. Depende do seu fluxo.

### Time pequeno ou projeto serio (orçamento R$ 1.000+/mes)
**Combo Claude Max 20x + Codex Pro (R$ 2.160)**. Justifica facil em qualquer projeto que paga > R$ 30k. Revisao cruzada vira diferencial competitivo.

### Time grande / empresa
Avaliacao caso a caso. Acima de 10 devs ja faz sentido conversar com Anthropic/OpenAI sobre **enterprise pricing** — descontos por volume, suporte dedicado, audit trail.

---

## CTA FINAL DA ABA

Voce viu os custos. Aplica:

- **Quer setup automatico (com plano sugerido)?** → Aba 7 (Quiz personalizado)
- **Quer ver as ferramentas em detalhe?** → Aba 4 (Stack)
- **Quer dominar o metodo (e economizar token)?** → Aba 2 (O Metodo)
- **Quer dicas avancadas de eficiencia?** → Aba 6 (Avancado, sub-aba Performance)

---

# Notas pro Claude Code (instrucoes de implementacao Aba 9)

### Estrutura geral
- Aba pratica e direta — UX foca em **pessoa decidindo plano**
- Disclaimer de cambio/data no topo (atualizavel)
- Calculadora interativa e o destaque

### Tabelas de planos (Secao 1)
- Tabelas responsivas, com badges de cor pra Claude (laranja/coral) e Codex (teal)
- Coluna "Preco R$" em destaque visual

### Cenarios (Secao 2)
- 4 cards lado a lado em desktop, stack em mobile
- Cada card com perfil + recomendacao + custo destacado
- Cores diferentes pra cada perfil (estudante azul, freelancer verde, time roxo, critico vermelho)

### Calculadora interativa (Secao 3)
- Componente JS inline, sem framework
- Estado em localStorage (continua de onde parou)
- Multi-step com progress bar
- Resultado mostra plano recomendado + custos + ROI

### Implementacao da calculadora
```javascript
// Logica simplificada
function calcularPlano(respostas) {
  const horas = respostas.horas;        // 0-3
  const tipo = respostas.tipo;          // 0-3
  const agente = respostas.agente;      // 0-3
  const time = respostas.time;          // 0-3
  const cobra = respostas.cobra;        // 0-3
  
  // Score de "intensidade"
  const intensidade = horas + tipo;
  
  if (intensidade <= 2) return { plano: 'pro', custo: 108 };
  if (intensidade <= 4) return { plano: 'max5x', custo: 540 };
  if (intensidade <= 6) return { plano: 'max20x', custo: 1080 };
  return { plano: 'combo', custo: 2160 };
}
```

### Quando vale ter os dois (Secao 4)
- 2 colunas: "Vale" e "Nao Vale"
- Cada item em card pequeno
- Cor sutil diferente nas duas colunas

### Hacks (Secao 5)
- Lista numerada de 7 dicas
- Cada uma com numero gigante + titulo + paragrafo

### Comparativo de eficiencia (Secao 6)
- Tabela com dados reais
- Barras de comparacao visual (Claude vs Codex em cada linha)
- "Conclusao adulta" em destaque

### Custos invisiveis (Secao 7)
- 4 cards de "custos escondidos"
- Cores de alerta sutis (amarelo/laranja)

### Recomendacao final (Secao 8)
- Bloco em destaque (fundo levemente diferente)
- 4 cenarios curtos com plano recomendado
- Tipo "manifesto" do Get It Easy

### Atualizacao de precos
- Add data de revisao no topo (ex: "Ultima revisao: abril 2026")
- Sugiro revisar essa aba **a cada release de plano** dos providers
- Possivel automacao futura: integrar com API que pega precos atuais

### Acessibilidade
- Calculadora navegavel por teclado
- Tabelas com headers semanticos
- Resultados gerados screen-reader-friendly
