# Get It Easy — README do Projeto

> Documento executivo. Cole essa pasta junto com as 9 abas markdown e use como bussola pro projeto.

---

## TL;DR (em 30 segundos)

**O que e:** toolkit + comunidade + personalizacao em portugues que ensina **o oficio de operar agentes de IA**, agnostico de ferramenta.

**Tagline:** "Pare de aprender ferramentas. Aprenda o oficio."

**Diferencial:** PT-BR + agnostico (Claude Code + Codex + Cursor) + personalizacao via quiz + comunidade brasileira ativa.

**Modelo de negocio:** free (quiz) → R$ 197 (manual) → R$ 47/mes (comunidade) → R$ 1.997+ (customizado).

**Estado atual:** 9 abas escritas em markdown (~24.500 palavras). Pronto pra implementar em HTML.

---

## A narrativa (nao esqueca)

Tres camadas concentricas:

1. **Fundacao (o metodo)** — mindset, contexto global vs local, organizacao, workflow. Vale pra qualquer agente.
2. **Stack (as ferramentas)** — Claude Code, Codex, Cursor, skills, MCP, plugins. Lado a lado, sem fanatismo.
3. **Personalizacao (o seu caminho)** — quiz que monta seu manual, suas skills, seus projetos. Sob medida.

A Camada 1 e o **moat conceitual**. Camada 2 e **commodity bem ensinada**. Camada 3 e **servico**.

**Tese estrategica:** ferramentas sao commodity (convergem release a release); metodo e oficio (sobrevive a qualquer release). Ensinando o oficio, o toolkit nao envelhece quando OpenAI/Anthropic lancam ferramenta nova.

---

## Mapa das 9 abas

| # | Aba | Palavras | Camada | Funcao |
|---|---|---|---|---|
| 1 | Comece aqui | 1.855 | Porta de entrada | Hero, manifesto, FAQs, bifurcacao iniciante/avancado, mapa do site |
| 2 | O Metodo | 1.713 | Fundacao | Conceito-mae: contexto global vs local. Cozinha + mochila. |
| 3 | Oficio | 3.605 | Fundacao | 4 pilares do prompt, templates, tabela de decisao, 6 cenarios, 6 regras, 5 anti-patterns, checklist |
| 4 | Stack | 2.525 | Stack | Claude Code vs Codex lado a lado, comparativo arquitetural, 11 cenarios "quero X" |
| 5 | Skills | 3.410 | Stack | Padrao aberto, anatomia SKILL.md, GSD, Spec-Kit, Superpowers, GSP em detalhe |
| 6 | Avancado | 4.165 | Stack | 11 sub-abas: CLAUDE.md, settings, MCP, subagents, hooks, custom skills, perf, CI/CD, troubleshooting, **Memoria (NOVO)**, **Plugins (NOVO)** |
| 7 | Setup Personalizado | 2.913 | Personalizacao | Quiz 6 perguntas, 4 cases reais, free vs premium, calculadora |
| 8 | Cola & Dicas Pro | 2.062 | Stack | Setup completo, comandos em grid Claude/Codex, 3 fluxos, 8 regras, 18 dicas pro |
| 9 | Custos & Planos | 2.315 | Stack | Tudo em R$, 4 cenarios, calculadora interativa, hacks de economia, custos invisiveis |

**Total:** 24.563 palavras. Cada aba tem **"Notas pro Claude Code"** no fim com instrucoes de implementacao.

---

## Mapeamento do site antigo → novo

| Aba antiga (15) | Aba nova (9) |
|---|---|
| 1. O que e + 15. Do Zero | **1. Comece aqui** (funde) |
| 3. Frameworks + 4. Workflow + 5. Dia Tipico | **2. O Metodo** (funde) |
| 6. Prompts + 8. Praticas | **3. Oficio** (funde) |
| 2. Ferramentas | **4. Stack** (reorganiza por objetivo + adiciona Codex) |
| 7. Skills + 12. Design | **5. Skills** (funde, reposiciona como padrao aberto) |
| 9. Tecnico | **6. Avancado** (expande com sub-abas Memoria + Plugins) |
| 11. Setup Auto | **7. Setup Personalizado** (vira o quiz central) |
| 10. Cola + 13. Dicas Pro | **8. Cola & Dicas Pro** (funde, adiciona Codex) |
| 14. Custos R$ | **9. Custos & Planos** (atualiza com Codex) |

**Resultado:** zero conteudo perdido. 4 fusoes (limpa redundancia), 5 expansoes (Codex entra), 1 reposicionamento estrutural (Skills).

---

## Decisoes de design mantidas

Do site original, NAO mexe:

- **Single HTML file** — sem build, sem framework, sem dependencias alem de Google Fonts
- **Dark theme** — bg #0e0f14, cards #1c1e28
- **Ouro como accent** — #d9a832
- **5 cores de ferramenta** — GSD roxo, GSP rosa, Spec-Kit verde, Superpowers ambar, OpenCode azul
- **Fontes** — Syne (display), DM Sans (body), JetBrains Mono (code)
- **PT-BR sem acento** — padrao dev/terminal, intencional
- **Funcionalidades** — busca global (Ctrl+K), copy-to-clipboard, hash routing, scroll reveal, navegacao por teclado, acessibilidade, responsivo, marquee/ticker

## Decisoes de design novas

A adicionar:

- **2 cores novas** — Claude Code (sugestao: laranja queimado/coral) e Codex (sugestao: teal/cyan) — **mesma hierarquia visual**, nao pode parecer que um e principal
- **Bifurcacao iniciante/avancado** logo na entrada (Aba 1)
- **Quiz interativo** na Aba 7 (estado em localStorage, geracao client-side)
- **Calculadora de custos** na Aba 9 (mesma logica)
- **Badges "NOVO"** nas sub-abas de Memoria e Plugins (Aba 6)
- **TOC sticky** na Aba 6 (navegacao entre 11 sub-abas)
- **Botao Imprimir/PDF** na Aba 8 (referencia offline)

---

## Modelo de negocio (3 camadas)

### Free — Quiz personalizado
- Quiz de 6 perguntas (5 min)
- Output: prompt + CLAUDE.md/AGENTS.md + lista de skills + 3 projetos + 3 agentes + comandos de setup

**Funcao comercial:** demonstra valor, gera lead, segmenta publico.

### Manual (one-time, ~R$ 197)
Tudo do free + manual em PDF de 40-60 paginas + setup script automatizado + pacote ZIP de skills + tema personalizado + atualizacoes 12 meses.

**Funcao comercial:** entrega completa pra quem quer comecar serio.

### Comunidade (assinatura, ~R$ 47/mes)
Tudo do manual + Discord ativo + atualizacoes do metodo + office hour mensal + repositorio privado + skills da comunidade.

**Funcao comercial:** retencao + LTV + autoridade.

### Customizado (consultoria, ~R$ 1.997+)
Tudo do anterior + sessao 1-a-1 + plugin privado opcional + AGENTS.md/CLAUDE.md sob medida + 30 dias suporte.

**Funcao comercial:** ticket alto + relacionamento enterprise.

> Precos sao referencia. Validar com mercado antes de fixar.

---

## Tech stack do site

**Imutavel:**
- HTML5 + CSS3 + Vanilla JS (sem framework)
- Google Fonts (Syne, DM Sans, JetBrains Mono)
- Single index.html, abre direto no browser
- Zero backend (tudo client-side)

**Adicoes pra Aba 7 e 9:**
- localStorage pra persistir progresso do quiz
- Estado de respostas em objeto JS
- Geracao de artefatos via template literals
- Download via Blob + URL.createObjectURL

**Pos-MVP (futuro):**
- Integracao com gateway de pagamento (Hotmart, Eduzz, ou Stripe)
- Discord da comunidade
- Sistema de entrega de PDF/ZIP pos-compra (pode usar Gumroad ou similar inicialmente)

---

## Plano de implementacao (ordem sugerida)

### Fase 1 — Estrutura (1-2 sessoes Claude Code)
1. Criar repositorio Git novo
2. Subir o index.html antigo como ponto de partida
3. Atualizar navbar/menu (15 abas → 9 abas)
4. Atualizar hero com nova tagline
5. Atualizar marquee/ticker com stats novos

### Fase 2 — Abas fundacionais (3-5 sessoes)
6. Implementar **Aba 1 (Comece aqui)** — substitui antigas 1 + 15
7. Implementar **Aba 2 (O Metodo)** — substitui antigas 3 + 4 + 5
8. Implementar **Aba 3 (Oficio)** — substitui antigas 6 + 8
9. Implementar **Aba 4 (Stack)** — substitui antiga 2, com Codex novo
10. Implementar **Aba 5 (Skills)** — substitui antigas 7 + 12

### Fase 3 — Avancado e referencia (3-4 sessoes)
11. Implementar **Aba 6 (Avancado)** — substitui antiga 9, expande com Memoria + Plugins
12. Implementar **Aba 8 (Cola & Dicas Pro)** — substitui antigas 10 + 13
13. Implementar **Aba 9 (Custos & Planos)** — substitui antiga 14

### Fase 4 — Quiz e personalizacao (2-3 sessoes — mais complexo)
14. Implementar **Aba 7 (Setup Personalizado)** — quiz interativo + geracao de artefatos
15. Testes do quiz com diferentes combinacoes
16. Refinamento de UX do quiz

### Fase 5 — Polimento (1-2 sessoes)
17. Cross-references entre abas (validar todos os links internos)
18. Acessibilidade (revisar ARIA labels, navegacao por teclado)
19. Performance (lazy load, otimizacao de imagens)
20. Mobile responsivo (testar em viewport pequeno)
21. Print/PDF da Aba 8 (CSS @media print)

### Fase 6 — Deploy
22. Subir no GitHub
23. Configurar GitHub Pages (ou Cloudflare Pages, Netlify, Vercel)
24. Conectar dominio (se houver)
25. Configurar Google Analytics ou similar (opcional)

**Total estimado:** 12-18 sessoes Claude Code. Diluido em 2-4 semanas conforme tempo disponivel.

---

## O que mostrar pro Claude Code (briefing)

Quando comecar com Claude Code, faz isso:

1. **Cria pasta limpa** com nome `get-it-easy-v2` (ou similar)
2. **Inicia git** + repositorio remoto
3. **Cria CLAUDE.md** na raiz com este resumo executivo (ou aponta pra ele)
4. **Cola as 9 abas markdown** numa pasta `/content/`
5. **Cola o index.html antigo** como referencia em `/reference/index-old.html`
6. **Primeiro prompt pro Claude Code:**

```
Le o CLAUDE.md e a pasta /content/ com as 9 abas.
Le tambem /reference/index-old.html como referencia visual.

Vamos construir o site novo (index.html) em fases.
Fase 1: estrutura base + navbar com 9 abas + hero novo.
Mantemos: dark theme, paleta dourada, single-file, vanilla JS.
Adicionamos: 2 cores novas (Claude Code laranja, Codex teal), badges "NOVO".

Comeca propondo um plano em bullets antes de codar nada.
```

7. **Aprova o plano** ou ajusta
8. **Vai por fase** — uma fase por sessao, commit no fim, volta no dia seguinte

---

## CLAUDE.md sugerido pro projeto

```markdown
# Get It Easy v2

## O que e este projeto
Site educacional single-file sobre operacao de agentes de IA em portugues.
Reposicionamento de "tutorial Claude Code" para "metodo agnostico de operar agentes."

## Stack
- HTML5 + CSS3 + Vanilla JS (sem framework)
- Google Fonts: Syne, DM Sans, JetBrains Mono
- Zero dependencias externas alem de Google Fonts
- Single index.html

## Convencoes
- Portugues brasileiro **sem acentos** (intencional)
- Dark theme, ouro como accent
- 5 cores de ferramenta + 2 novas (Claude Code, Codex)
- Codigo: indentacao 2 espacos
- Classes CSS em kebab-case
- IDs de aba: `tab-N` (ex: tab-1, tab-2)

## Arquitetura
- /index.html — site completo (single file)
- /content/ — 9 markdowns com conteudo de cada aba (referencia)
- /reference/ — index.html antigo (referencia visual)
- /assets/ — imagens, se houver (manter zero por enquanto)

## CRITICAL RULES
- NUNCA usar framework (Vue, React, etc.)
- NUNCA adicionar dependencia externa nova sem perguntar
- NUNCA quebrar single-file (tudo em index.html)
- SEMPRE manter paleta atual (nao inventa cor nova sem aprovacao)
- SEMPRE manter funcionalidades existentes (busca, copy, hash routing, etc.)

## Quick commands
- Local preview: `python -m http.server 8000` ou abrir index.html direto
- Deploy: push pro main + GitHub Pages auto-deploy

## Decisoes arquiteturais
- 9 abas (reduzido de 15 antigas) — ver pasta /content/
- Quiz interativo na Aba 7 (state em localStorage)
- Calculadora interativa na Aba 9
- TOC sticky na Aba 6 (11 sub-abas)
- Marquee/ticker mantido com stats atualizados

## O que NAO fazer
- Nao traduzir gringo — conteudo e original em PT-BR
- Nao adotar tom corporativo — voz e direta, conversacional
- Nao virar fanboy de Claude Code OU Codex — tratamento equivalente
- Nao encher de imagem decorativa — visual limpo e funcional

## Cores
- Background: #0e0f14
- Cards: #1c1e28
- Ouro accent: #d9a832
- GSD: roxo
- GSP: rosa
- Spec-Kit: verde
- Superpowers: ambar
- OpenCode: azul
- Claude Code: laranja queimado / coral (NOVO — definir hex final)
- Codex: teal / cyan (NOVO — definir hex final)

## Fontes
- Display (H1, H2): Syne
- Body: DM Sans
- Code: JetBrains Mono
```

---

## Restos importantes (nao esquece)

### Conteudo vivo
A Aba 4 (Stack) e Aba 9 (Custos) **envelhecem rapido** — releases mensais de Claude/Codex mudam features e precos. Sugiro revisar essas duas a **cada 2-3 meses**. Marcar com data de ultima revisao.

### Cross-references
Todas as 9 abas tem links pra outras abas. Quando implementar, valida que **todos os links funcionam** (sem 404 interno).

### Mobile
Aba 6 (11 sub-abas) e Aba 7 (quiz) sao as mais complexas em mobile. Investir tempo extra em testar viewport pequeno.

### Acessibilidade
Quiz e calculadora precisam ser navegaveis 100% por teclado. ARIA labels em cada elemento interativo.

### Print
Aba 8 (Cola & Dicas Pro) tem botao de imprimir/PDF. CSS @media print precisa esconder navegacao e expandir conteudo recolhido.

---

## Roadmap pos-MVP

**Mes 1:** site no ar com 9 abas implementadas
**Mes 2:** quiz funcional + entrega de artefatos free
**Mes 3:** integracao de pagamento + entrega do pacote pago
**Mes 4:** Discord da comunidade ativo + primeiros assinantes
**Mes 5:** primeiros pacotes customizados (1-a-1)
**Mes 6:** validar precos vs mercado, ajustar oferta

**Mes 12:** considerar:
- Plugin marketplace proprio (visto na Aba 6)
- Curso/serie de videos complementar
- Parceria com Anthropic/OpenAI (selo, embaixadoria)
- Versao em ingles (se mercado BR validar)

---

## Pra fechar

Voce tem agora:
- 9 markdowns com conteudo completo (24.500 palavras)
- Este resumo executivo
- Mapeamento do antigo pro novo
- Plano de implementacao em fases
- CLAUDE.md sugerido pro projeto
- Roadmap dos 12 meses

**Proximo movimento:** abre Claude Code na pasta nova, cola este documento como CLAUDE.md (ou base dele), aponta pras 9 abas, e segue Fase 1.

Boa construcao. **As ferramentas vao mudar. O metodo nao.**
