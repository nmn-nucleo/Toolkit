# Get It Easy — Design Spec

## Visao geral

Site educacional single-file (index.html) sobre operacao de agentes de IA em portugues brasileiro. Reposicionamento de "Claude Code Toolkit" para metodo agnostico. 9 abas, dark theme, zero dependencias alem de Google Fonts.

**Tagline:** "Desenvolva como uma Big Tech estando solo"

**Entregavel:** index.html unico, abre direto no browser.

---

## Decisoes de design

### Direcao visual
Evolucao do site original. Mesma base dark/ouro, mesmas fontes, componentes atualizados. Quem viu o antigo reconhece.

### Paleta de cores

**Mantidas do original:**
```css
:root {
  /* Backgrounds */
  --bg0: #09090d;
  --bg1: #0e0f14;
  --bg2: #141620;
  --bg3: #1c1e28;
  --bg4: #24263280;

  /* Texto */
  --t1: #f0ede6;
  --t2: #b0ada6;
  --t3: #969390;
  --t4: #454340;

  /* Ouro accent */
  --au: #d9a832;
  --au1: #f5cf6a;
  --au3: #b88420;
  --aubg: rgba(217,168,50,.07);

  /* Ferramentas auxiliares */
  --gsd: #7c6aff;       /* GSD roxo */
  --gsp: #e8527a;       /* GSP rosa */
  --spc: #2dbf8a;       /* Spec-Kit verde */
  --sup: #e8a84b;       /* Superpowers ambar */
  --opc: #4ba8e8;       /* OpenCode azul */

  /* Semantico */
  --err: #e24b4a;
  --ok: #2dbf8a;
  --warn: #e8a84b;

  /* Bordas */
  --b1: rgba(255,255,255,.05);
  --b2: rgba(255,255,255,.09);
  --b3: rgba(255,255,255,.15);
}
```

**Novas (harnesses):**
```css
:root {
  /* Claude Code — terracota */
  --cc: #d4775c;
  --cc-bg: rgba(212,119,92,.07);
  --cc-b: rgba(212,119,92,.22);

  /* Codex — cyan suave */
  --cdx: #46b5c9;
  --cdx-bg: rgba(70,181,201,.07);
  --cdx-b: rgba(70,181,201,.22);
}
```

Ambos harnesses tem mesma hierarquia visual. Nenhum "grita" mais que o outro.

### Tipografia (mantida)
```css
--f-display: 'Syne', sans-serif;     /* Headings, logo */
--f-body: 'DM Sans', sans-serif;     /* Paragrafos, UI */
--f-mono: 'JetBrains Mono', monospace; /* Codigo, eyebrows */
```

Escala tipografica, espacamento (grid 8pt), raios de borda, animacoes — tudo mantido do original.

---

## Estrutura: 9 abas

| # | ID | Label | Icone | Camada | Wrapper |
|---|---|---|---|---|---|
| 1 | comece | Comece aqui | ▶ | Fundacao | .W |
| 2 | metodo | O Metodo | ◇ | Fundacao | .W2 |
| 3 | oficio | Oficio | ✦ | Fundacao | .W |
| 4 | stack | Stack | ⚡ | Stack | .W |
| 5 | skills | Skills | ⚙ | Stack | .W |
| 6 | avancado | Avancado | ◆ | Stack | .W |
| 7 | setup | Setup | ☰ | Personalizacao | .W2 |
| 8 | cola | Cola & Dicas | ⌘ | Personalizacao | .W |
| 9 | custos | Custos & Planos | $ | Personalizacao | .W |

### Navegacao
- Tabs no header, agrupadas por camada com separadores visuais sutis
- Cada tab com icone pequeno ao lado do nome
- 3 grupos: Fundacao (1-3) | Stack (4-6) | Personalizacao (7-9)
- Separador: linha vertical fina `rgba(255,255,255,0.06)` entre grupos
- Header sticky, 50px, blur backdrop, z-index 100
- Mobile: tabs scrollaveis horizontalmente
- Icones em unicode/SVG inline (sem dependencia de icon library)

---

## Hero (Aba 1 — acima do fold)

### Layout
- Centralizado, full viewport height
- Fundo: 3 orbs de luz difusa (terracota top-right, cyan bottom-left, ouro center) sobre #0e0f14
- Orbs com opacity baixa (0.08-0.12), radial-gradient, sem animacao pesada

### Conteudo
```
[eyebrow] Metodo + comunidade + personalizacao em portugues
[H1] Desenvolva como uma Big Tech estando solo
[lead] Em 2026 o problema nao e escolher entre Claude Code, Codex ou Cursor.
       O problema e que ninguem te ensinou a pensar com agentes de IA.
[CTA unico] Faco o quiz → (link pra Aba 7)
[stats] 107+ skills | 5 ferramentas | 2 padroes abertos | 9 abas
```

- Stats com numeros animados (contagem ao entrar na viewport via IntersectionObserver)
- Eyebrow: JetBrains Mono, uppercase, letter-spacing .14em, cor ouro
- H1: Syne 800, fluid clamp(38px, 6.5vw, 70px), "Big Tech" em ouro
- Lead: DM Sans, 15px, cor --t2
- CTA: botao dourado (#d9a832 bg, #0e0f14 text), border-radius 8px
- Prova social abaixo: "Construido em portugues, testado com clientes reais, agnostico de ferramenta."

### Abaixo do fold
- Bifurcacao iniciante/avancado: 2 cards lado a lado
- Card "Iniciante curioso" + Card "Dev experiente"
- Hover destaca, click navega

---

## Componentes (evolucao do original)

### Cards
Mesma base (.card com bg3, border b1, border-radius r-lg), adicionando:
- Cards de harness: stripe lateral na cor do harness (terracota ou cyan)
- Cards de ferramenta: stripe no topo (mantido do original)

### Tool Cards
Mantidos exatamente como original: stripe colorido, badge tipo/importancia, problema/solucao, install command, barra de importancia visual.

### Code blocks
Mantidos: bg0, border b1, monospace 12px, line-height 1.9, botao copiar em todos. Cores de sintaxe mantidas (.cm, .cc, .ch, .cg, .cp, .cr).

### FAQ accordion
Mantido: click toggle, icone + rotaciona 45deg.

### Tabela de decisao
Mantida: .ck check verde, .cx opacity 20%, .co ambar.

### Comparacao (prompt ruim/bom)
Mantida: .cmp-bad vermelho, .cmp-good verde.

### Cenarios interativos
Mantidos: botoes de cenario que mostram steps no painel abaixo.

### Badges
Mantidos: .b-req verde, .b-opt azul, .b-ui ambar, .b-danger vermelho.
Novo: .b-new com fundo ouro suave, texto ouro, para badges "NOVO" nas sub-abas Memoria e Plugins.

---

## Funcionalidades interativas

### Mantidas do original
1. Busca global (Ctrl+K) — pesquisa em todas as abas
2. Copy-to-clipboard — todos os code blocks e prompt boxes
3. Hash routing — deep links (#aba), back button
4. Scroll reveal — IntersectionObserver, fade-up
5. Navegacao por teclado — setas, Tab, Enter, Esc
6. Acessibilidade — skip link, focus rings, ARIA roles/tablist, reduced-motion
7. Responsivo — breakpoints 480/768/1024/1440
8. Ticker/marquee — stats e versoes

### Novas
9. **Quiz interativo (Aba 7)** — stepper vertical, 1 pergunta por vez, barra de progresso no topo, transicao suave. Estado em localStorage. Gera artefatos client-side via template literals.
10. **Calculadora de custos (Aba 9)** — sliders, presets (estudante/freelancer/time/critico), resultado em R$. Mesma logica do site original, expandida com Codex.
11. **Sub-tabs sticky (Aba 6)** — barra horizontal de sub-tabs que gruda abaixo do header ao scrollar. Badges "NOVO" em Memoria e Plugins.
12. **Botao imprimir/PDF (Aba 8)** — CSS @media print que esconde navegacao e expande conteudo recolhido.
13. **Stats animados (hero)** — contagem de numeros ao entrar na viewport.
14. **Checklist com persistencia (Aba 3)** — checkboxes clicaveis em localStorage.

---

## Aba 6 — Avancado (TOC especial)

11 sub-abas com navegacao horizontal sticky:

| # | Sub-aba | Badge |
|---|---|---|
| 1 | CLAUDE.md / AGENTS.md | — |
| 2 | settings / config | — |
| 3 | MCP | — |
| 4 | Subagents | — |
| 5 | Hooks | — |
| 6 | Custom skills | — |
| 7 | Performance | — |
| 8 | CI/CD | — |
| 9 | Troubleshooting | — |
| 10 | Memoria | NOVO |
| 11 | Plugins & Marketplace | NOVO |

Sub-tabs: barra horizontal scrollavel, sticky abaixo do header principal. Mesmo estilo visual das sub-tabs do site original (Aba Tecnico).

---

## Aba 7 — Quiz (stepper)

### UX
- 6 perguntas, 1 por vez
- Barra de progresso no topo (step N de 6)
- Transicao fade entre perguntas
- Botoes anterior/proximo
- Pergunta 7 (bonus) opcional com campo livre

### Artefatos gerados
- Prompt personalizado (copiavel)
- CLAUDE.md ou AGENTS.md (copiavel + download)
- Lista de skills recomendadas
- 3 ideias de agentes
- 3 ideias de projetos
- Comandos de setup (bash/powershell conforme OS)

### Persistencia
- localStorage para estado do quiz (respostas, step atual)
- Download via Blob + URL.createObjectURL

### Layout resultado
- 2 tabs: "Prompt para o agente" | "CLAUDE.md / AGENTS.md gerado"
- Botao "Copiar tudo" + "Baixar como arquivo"

---

## Restricoes tecnicas

- Single HTML file — sem build, sem framework
- Google Fonts unica dependencia externa
- Portugues brasileiro sem acentos no conteudo (intencional)
- Dark theme imutavel
- Zero backend — tudo client-side
- Responsivo mobile-first (480/768/1024/1440)
- Acessibilidade WCAG AA baseline
- Performance: lazy load, IntersectionObserver, event delegation

---

## Plano de implementacao

### Fase 1 — Esqueleto
- index.html com head, tokens CSS, reset, header/nav com 9 abas agrupadas + icones
- Sistema de paginas (show/hide por tab)
- Hash routing
- Hero completo (orbs, titulo, CTA, stats)
- Ticker/marquee
- Busca global (Ctrl+K)

### Fase 2 — Abas fundacionais (1-3)
- Aba 1: Comece aqui (hero ja pronto, bifurcacao, FAQ, pre-requisitos, stats, mapa)
- Aba 2: O Metodo (global vs local, cozinha/mochila, anti-padrao Globalzao)
- Aba 3: Oficio (4 pilares, templates, tabela decisao, cenarios, regras, anti-patterns, checklist, ciclo do dia)

### Fase 3 — Abas stack (4-6)
- Aba 4: Stack (cards Claude Code vs Codex em paridade, comparativo, stack por objetivo, ferramentas auxiliares, guia decisao)
- Aba 5: Skills (padrao aberto, anatomia SKILL.md, 4 ferramentas, GSP showcase, workflows, distribuicao)
- Aba 6: Avancado (11 sub-abas com TOC sticky + badges NOVO)

### Fase 4 — Quiz e referencia (7-9)
- Aba 7: Setup Personalizado (quiz stepper, geracao de artefatos, free vs premium)
- Aba 8: Cola & Dicas Pro (grid Claude/Codex, fluxos, 18 dicas, botao imprimir)
- Aba 9: Custos & Planos (calculadora, cenarios em R$, comparativo planos)

### Fase 5 — Polimento
- Cross-references entre abas
- Acessibilidade (ARIA, teclado, reduced-motion)
- Mobile (viewport pequeno, Aba 6 e 7 especialmente)
- Print CSS (Aba 8)
- Performance (lazy load, otimizacao)
