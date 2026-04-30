# Aba 3 — Oficio

## A pratica diaria de operar agentes (vale pra Claude Code, Codex, Cursor, qualquer um)

---

## INTRO (topo da aba)

### Eyebrow
> Pratica, nao teoria — aplique no proximo prompt

### Titulo principal
> # Conhecer a ferramenta nao e saber operar. Saber operar e oficio.

### Lead paragraph
A Aba 2 te deu o **metodo** (global vs local, contexto enxuto). Esta aba te da o **oficio**: como escrever prompt que funciona, quando usar qual abordagem, que erros custam dinheiro, e a rotina que separa quem entrega de quem reclama. Tudo agnostico de ferramenta. Os principios aqui sobrevivem a qualquer release de Claude Code, Codex ou o que vier depois.

---

## SECAO 1 — Os 4 pilares do bom prompt (anatomia)

Todo prompt que funciona consistentemente tem essas 4 partes. Toda vez que voce reclama "a IA nao entendeu", uma delas estava faltando.

### Pilar 1 — Contexto
**Pergunta que responde:** "O que o agente precisa saber pra fazer isso?"

Codigo do projeto, stack, convencoes, decisoes anteriores. Pode estar no CLAUDE.md/AGENTS.md (contexto persistente) ou no proprio prompt (contexto da tarefa).

**Exemplo ruim:** "Cria um endpoint pra usuario."
**Exemplo bom:** "Cria um endpoint pra usuario. Stack: FastAPI + PostgreSQL. Padrao do projeto: validacao com Pydantic, response sempre em JSON com `{data, error}`. Tabela `users` ja existe com colunas `id, email, name, created_at`."

### Pilar 2 — Objetivo
**Pergunta que responde:** "Como sei que terminou bem?"

O criterio de sucesso. Sem isso, o agente entrega "alguma coisa" e voce avalia subjetivamente.

**Exemplo ruim:** "Faz funcionar."
**Exemplo bom:** "Sucesso = endpoint POST /users que aceita `{email, name}`, valida formato de email, salva no banco, retorna `{data: {id, email, name}, error: null}` em 200 ou `{data: null, error: <msg>}` em 400."

### Pilar 3 — Restricoes
**Pergunta que responde:** "O que NAO fazer?"

Limites do que e aceitavel. Tecnologias proibidas, padroes a evitar, escopo a respeitar.

**Exemplo ruim:** (nao tem — agente pode trazer dependencia nova qualquer)
**Exemplo bom:** "Nao adicionar dependencia nova. Nao mudar schema do banco. Nao tocar em outros endpoints. Se precisar de algo que nao existe, pergunta antes."

### Pilar 4 — Formato
**Pergunta que responde:** "Como quero receber a resposta?"

Diff de codigo, explicacao em prosa, lista de passos, JSON estruturado. Sem especificar, voce recebe o formato default da IA — que pode nao ser util.

**Exemplo ruim:** (nao especifica — recebe parede de texto + codigo misturados)
**Exemplo bom:** "Entrega: (1) o codigo do endpoint pronto pra colar, (2) os testes pytest, (3) breve explicacao das decisoes que tomou. Nessa ordem. Sem comentarios obvios no codigo."

### Os 4 pilares juntos = prompt que entrega
Quando voce monta os 4 e roda, o agente sabe: o que voce sabe (contexto), o que voce quer (objetivo), o que evitar (restricoes), e como te dar (formato). E entrega.

---

## SECAO 2 — CLAUDE.md ↔ AGENTS.md: o mesmo conteudo, dois nomes

Esse e o ponto de equivalencia mais importante do toolkit. Voce escreve **uma vez** e o conteudo serve aos dois ecossistemas com adaptacao minima.

### Tabela de equivalencia

| | **CLAUDE.md** (Claude Code) | **AGENTS.md** (Codex, Cursor, Aider) |
|---|---|---|
| **Localizacao** | `<projeto>/CLAUDE.md` | `<projeto>/AGENTS.md` |
| **Sintaxe** | Markdown | Markdown |
| **Quem le** | Claude Code | Codex, Cursor, Aider |
| **Conteudo tipico** | Mesmo | Mesmo |
| **Tamanho ideal** | 100-300 linhas | 100-300 linhas |
| **Hierarquia** | 5 camadas (system → user → project → directory → flag) | Profiles explicitos via `--profile` |
| **Adocao** | Anthropic only | Padrao aberto da industria |

### O que vai dentro (igual nos dois)

```markdown
# Nome do Projeto

## Stack
- Backend: <linguagem + framework>
- Banco: <tipo + versao>
- Frontend: <framework>
- Deploy: <onde>

## Convencoes
- Padrao de commit: <formato>
- Branch principal: <nome>
- Estilo de codigo: <linter/formatter>
- Padroes de PR: <descricao>

## Decisoes arquiteturais
- <decisao 1 com racional>
- <decisao 2 com racional>

## O que NAO fazer
- Nao instalar dependencia sem perguntar
- Nao modificar <arquivo critico>
- Nao tocar em <area sensivel>

## Comandos uteis
- Rodar: <comando>
- Testar: <comando>
- Build: <comando>
- Deploy: <comando>

## Contexto adicional
- <links pra docs>
- <pessoas responsaveis>
- <historico relevante>
```

### A regra
Voce escreve **uma vez** o conteudo. Se o time usa Claude Code, salva como `CLAUDE.md`. Se usa Codex/Cursor, salva como `AGENTS.md`. Se usa os dois, salva ambos (ou faz symlink). **Nao precisa reescrever pra cada ferramenta.**

---

## SECAO 3 — Templates de prompt (por tarefa, agnosticos)

> 6 templates que funcionam em Claude Code, Codex, Cursor, qualquer agente.
> Cada um seguindo os 4 pilares.
> Mantem botao "Copiar template" em cada bloco.

### Template 1 — Criar feature nova (greenfield)
```
Contexto: [descricao do projeto + stack + arquivo CLAUDE.md/AGENTS.md ja deve estar lido]
Objetivo: criar [feature X] que [comportamento esperado]. 
  Sucesso = [criterio mensuravel].
Restricoes:
  - Nao adicionar dependencia nova
  - Seguir convencao do projeto
  - [outras restricoes especificas]
Formato: 
  1. Plano em bullets do que vai fazer (antes de codar)
  2. Codigo dos arquivos novos/modificados
  3. Testes
  4. Resumo final em 3 linhas
```

### Template 2 — Consertar bug
```
Contexto: arquivo [X] tem um bug. Comportamento esperado: [Y]. Comportamento atual: [Z]. 
  Reproducao: [passos]. Stack trace: [se tiver].
Objetivo: identificar a causa raiz e corrigir, sem efeito colateral em outras areas.
Restricoes:
  - Nao trocar logica que nao esta diretamente relacionada
  - Adicionar teste que pega esse bug
  - Se a causa raiz revelar problema mais profundo, sinaliza mas nao corrige sozinho
Formato:
  1. Diagnostico (1 paragrafo: por que esta acontecendo)
  2. Diff da correcao
  3. Teste novo
  4. Risco residual (se houver)
```

### Template 3 — Revisar codigo
```
Contexto: PR/diff a seguir. Padroes do projeto em CLAUDE.md/AGENTS.md.
Objetivo: revisar como senior reviewer faria. 
  Sucesso = nao deixa passar nada que afete corretude, seguranca, performance ou clareza.
Restricoes:
  - Nao reescrever o codigo (so apontar)
  - Priorizar issues por severidade
  - Aceitar trade-offs explicitos do autor
Formato:
  1. Veredito: APPROVE / REQUEST_CHANGES / COMMENT
  2. Issues por severidade: BLOCKING / HIGH / MEDIUM / NIT
  3. Pontos positivos (1-2)
```

### Template 4 — Refactor de modulo
```
Contexto: modulo [X] em [caminho]. Tamanho atual: [linhas]. 
  Problema: [duplicacao / acoplamento / complexidade / testabilidade].
Objetivo: refatorar para [criterio: ex. reduzir duplicacao, isolar responsabilidades, melhorar testabilidade].
  Sucesso = comportamento publico identico, mas estrutura interna [criterio].
Restricoes:
  - Mudancas em pequenos commits, nao um commit gigante
  - Manter compatibilidade de API publica
  - Cada commit roda os testes existentes
Formato:
  1. Plano de refactor (passos numerados)
  2. Para cada passo: diff + explicacao
  3. Validacao final (testes passam? perf nao regrediu?)
```

### Template 5 — Documentar codigo
```
Contexto: arquivo/modulo [X]. Publico-alvo: [dev novo no time / usuario externo / voce daqui 6 meses].
Objetivo: criar documentacao que faz [persona] entender [aspecto] em [tempo].
Restricoes:
  - Nao documentar o obvio
  - Inclui exemplos rodaveis
  - Foco em "por que", nao "o que" (o codigo ja diz o que)
Formato:
  - Markdown com secoes: Visao geral / Quando usar / Como usar (com exemplo) / Pegadinhas
```

### Template 6 — Analise de dataset / planilha
```
Contexto: dataset em [caminho]. Linhas: [N]. Colunas relevantes: [lista]. 
  Origem dos dados: [fonte]. Nivel de confianca: [alta/baixa/incerta].
Objetivo: responder [pergunta especifica] OU [encontrar padrao em area X].
Restricoes:
  - Nao alucinar numero (sempre derivar dos dados)
  - Sinalizar dados sujos / faltantes
  - Mostrar metodologia (como chegou no resultado)
Formato:
  1. Resposta direta (1-2 linhas)
  2. Metodo (queries SQL ou codigo Python que rodou)
  3. Caveats e qualidade dos dados
  4. Sugestoes de proxima analise (opcional)
```

---

## SECAO 4 — Tabela de decisao: que abordagem usar?

> Bloco visual claro. Quando voce tem uma tarefa, consulta isso pra saber como atacar.

| Tipo de tarefa | Abordagem | Por que |
|---|---|---|
| Pequena e simples (< 30min) | Prompt direto, sem spec formal | Overhead nao compensa |
| Media (30min - 2h) | Prompt completo com 4 pilares | Estrutura ajuda |
| Grande (> 2h) | SDD (Spec-Driven Dev) primeiro, codigo depois | Sem spec voce retrabalha |
| Critica (producao, financeiro, saude) | Spec + revisao cruzada (2 agentes) + testes | Erro caro |
| Repetitiva (faz sempre igual) | Vira **skill** | Codifica o padrao |
| Colaborativa (time/cliente) | CLAUDE.md/AGENTS.md robusto | Padroniza |
| Exploratoria (nao sabe como comecar) | Pede plano primeiro, codigo depois | Forca pensar antes |
| Bug em producao urgente | Diagnostico curto + fix minimo + teste regressao | Evitar fix piorar |

---

## SECAO 5 — 6 cenarios reais (com prompt errado vs prompt certo)

> Cards interativos. Cada um expande pra mostrar o cenario completo.
> "Ouro" do toolkit — mantem do site original e expande.

### Cenario 1: Bug em producao, urgencia alta
**Situacao:** sao 16h de uma sexta. Cliente reclama que o checkout esta retornando 500. Voce precisa achar e corrigir antes do final do expediente.

**Prompt errado:** "O checkout esta com 500. Conserta."

**Prompt certo:**
```
Contexto: erro 500 no endpoint POST /checkout, intermitente. 
Comecou ~30min atras (logs em [caminho]). Stack trace anexado. 
Cliente em producao, urgencia alta.
Objetivo: identificar causa raiz e propor fix minimo, sem rodar deploy ainda.
Restricoes: nao mudar nada que nao seja diretamente relacionado ao bug. 
Se causa raiz exigir mudanca grande, sinaliza e propoe workaround temporario.
Formato: 
  1. Hipotese mais provavel (1 linha)
  2. Como confirmar (comando/query)
  3. Fix minimo proposto (diff)
  4. Plano de deploy seguro
```

**Por que funciona:** o agente nao tem licenca pra "consertar" — tem licenca pra **diagnosticar** primeiro. Voce mantem controle, fix e cirurgico, nao introduz novo bug em panico.

### Cenario 2: Feature nova em projeto existente
**Situacao:** PM pediu "tela de configuracoes do usuario". Projeto ja tem 8 meses, 50 arquivos, convencoes definidas.

**Prompt errado:** "Cria a tela de configuracoes do usuario com salvar perfil, mudar senha, e preferencias de notificacao."

**Prompt certo:**
```
Contexto: projeto [X], stack [Y]. Padroes em CLAUDE.md/AGENTS.md. 
Componentes existentes que devo reusar: [lista de componentes na pasta /components]. 
API atual de usuario em [arquivo].
Objetivo: tela /settings com 3 secoes: Perfil (nome, email, foto), Senha (atual + nova), Notificacoes (toggles).
Restricoes: 
  - Reusar componentes existentes (nao criar Button novo)
  - Validacao consistente com resto do app
  - Nao adicionar dep nova
Formato:
  1. Plano (que arquivos vai criar/editar)
  2. Codigo
  3. Testes basicos
  4. Pontos que precisam decisao do PM (se houver)
```

**Por que funciona:** voce explicita "reusar o que existe". Sem isso, agente cria componentes novos paralelos aos antigos, gerando inconsistencia visual e codigo duplicado.

### Cenario 3: Refactor grande de codigo legado
**Situacao:** modulo de pagamentos com 1.500 linhas, sem testes, todo mundo tem medo de tocar.

**Prompt errado:** "Refatora o modulo de pagamentos."

**Prompt certo:**
```
Contexto: arquivo /src/payments/handler.py com 1.500 linhas. 
Sem testes atualmente. Comportamento publico: [3 funcoes principais e suas assinaturas].
Objetivo: refatorar em modulos coesos, ADICIONANDO testes ANTES de mudar codigo.
Restricoes:
  - Comportamento publico identico (nenhum teste de integracao deve quebrar)
  - Mudancas em commits pequenos
  - Cada commit deixa o codigo rodavel
  - Se descobrir bug existente, sinaliza mas nao corrige sozinho
Formato:
  1. Plano em fases (test coverage primeiro, depois refactor)
  2. Para cada fase: lista de commits
  3. Validacao apos cada fase
```

**Por que funciona:** "testes antes de refactor" e regra de ouro de codigo legado. Sem teste, voce esta refatorando no escuro. Sub-agentes podem ajudar aqui — um escreve teste, outro refatora baseado nos testes.

### Cenario 4: Onboarding em projeto desconhecido
**Situacao:** voce assumiu codigo de um cliente novo. 200 arquivos, zero documentacao.

**Prompt errado:** "Me explica o projeto."

**Prompt certo:**
```
Contexto: acabei de assumir esse repositorio. Nao conheco o codigo.
Objetivo: gerar mapa mental do projeto pra eu entender em 30min.
Especificamente:
  - Pontos de entrada (main, server, etc.)
  - Modulos principais e suas responsabilidades
  - Fluxos principais (request -> resposta)
  - Deps externas criticas
  - Pontos sensiveis ou complexos
Formato:
  - Markdown estruturado por sessoes
  - Diagrama em ASCII se ajudar
  - Lista de "perguntas que voce faria pro autor original" no final
  - Lista de arquivos top-10 que devo ler primeiro, em ordem
```

**Por que funciona:** voce direciona o que quer aprender, nao deixa o agente despejar tudo. Resultado e leitura focada de 30min em vez de 4 horas de exploracao caotica.

### Cenario 5: Migracao de stack/lib
**Situacao:** time decidiu trocar de Express pra Fastify. 30 endpoints existentes.

**Prompt errado:** "Migra de Express pra Fastify."

**Prompt certo:**
```
Contexto: aplicacao Node.js com 30 endpoints em Express 4. 
Vamos migrar pra Fastify 4. Razao: performance + tipos.
Objetivo: plano de migracao incremental (nao big-bang).
Restricoes:
  - App deve continuar rodando durante migracao (sem down)
  - Endpoints migrados conviver com Express (boundary clara)
  - Testes existentes devem continuar passando
Formato:
  1. Estrategia (rota a rota? feature por feature? camada por camada?)
  2. Plano em fases com criterios de "go/no-go" entre fases
  3. Codigo de exemplo: 1 endpoint migrado completo + comentarios
  4. Lista de pegadinhas (middlewares Express incompativeis, etc.)
```

**Por que funciona:** migracao e projeto, nao tarefa. Plano em fases com go/no-go evita ficar 3 semanas sem aplicacao funcional.

### Cenario 6: Tarefa que voce nao sabe como comecar
**Situacao:** boss te pediu "um sistema de notificacoes que entenda preferencias do usuario e nao faca spam." Voce nem sabe por onde comeca.

**Prompt errado:** "Cria um sistema de notificacoes inteligente."

**Prompt certo:**
```
Contexto: precisamos de sistema de notificacoes do projeto [X]. 
Tipos de notificacoes possiveis: [lista]. Canais: email, push, in-app. 
Stack do projeto: [...].
Objetivo: nao escrever codigo ainda. Quero um plano de design.
Especificamente, me ajude a pensar em:
  - Modelagem de "preferencia do usuario"
  - Politicas anti-spam (rate limit, cooldown, agrupamento)
  - Trade-offs de implementacao (in-house vs servico externo)
  - MVP vs versao final
Formato:
  - 3 opcoes de arquitetura, cada uma com pros/contras
  - Modelo de dados sugerido
  - Recomendacao final + razao
  - Pergunte 5 perguntas de stakeholder que voce precisa antes de codar
```

**Por que funciona:** voce admite que nao sabe e usa o agente como **parceiro de pensamento**, nao como executor. Resultado e clareza antes de gastar token escrevendo codigo errado.

---

## SECAO 6 — As 6 regras de ouro

> Bloco em destaque. Numeros grandes. Cada regra em 1 linha + 1 paragrafo de explicacao.

### 1. Contexto primeiro, prompt depois
Sempre ofereca contexto **antes** de pedir acao. Agente sem contexto preenche lacunas com suposicao — e voce paga em retrabalho.

### 2. Pequeno antes de grande
Quebre tarefa grande em pequenas. Tarefa pequena = prompt focado = resultado certo. Tarefa grande = prompt vago = resultado generico.

### 3. Local sobrescreve global (sempre)
Regras do projeto sempre vencem regras pessoais. Documente isso explicitamente no CLAUDE.md/AGENTS.md do projeto.

### 4. Testar antes de confiar
Nunca aceitar mudanca sem rodar. Mesmo se "parece certo." Especialmente quando "parece certo." Maior parte dos bugs introduzidos por IA passa em revisao de codigo mas falha em runtime.

### 5. Commit atomico (uma mudanca, um commit)
Cada commit faz **uma coisa**. Refactor + feature nova + bug fix tudo junto vira commit impossivel de revisar e pesadelo pra reverter.

### 6. Re-spec antes de re-codar
Se voce mudou de ideia no meio do trabalho, **atualize a spec antes de mexer no codigo**. Senao voce vira detetive da propria mudanca em 2 semanas.

---

## SECAO 7 — Os 5 anti-patterns que custam dinheiro

> Bloco em destaque com cor de alerta sutil (vermelho suave / laranja). Cada um e um erro caro.

### Anti-pattern 1: O Mega-Prompt
Prompt de 500 linhas com tudo: contexto + 5 tarefas + 10 restricoes + 3 formatos diferentes. Resultado: agente perde foco, entrega tudo medio, voce gasta token em re-prompt.

**Sintoma:** voce escreve por 10 minutos antes de mandar o prompt.

**Cura:** divide em 3-5 prompts pequenos, encadeados.

### Anti-pattern 2: A Adivinhacao
Esperar que o agente "saiba" coisas que voce nao disse. "Ele deveria entender que isso e um projeto Django, ne?"

**Sintoma:** voce reclama "a IA nao entendeu" mais que 1x por semana.

**Cura:** CLAUDE.md/AGENTS.md robusto. Contexto sempre explicito.

### Anti-pattern 3: A Aceitacao Cega
Aceitar diff sem ler. Aceitar resposta sem testar. "Parece OK."

**Sintoma:** voce comita codigo do agente direto e descobre o bug em producao.

**Cura:** revisar o diff. Rodar os testes. Sempre.

### Anti-pattern 4: A Confianca em Alucinacao
Usar API/funcao/biblioteca que o agente sugeriu sem verificar se existe. Agente sugere `lodash.deepClone` (existe? como assina?), voce usa, quebra.

**Sintoma:** "tinha certeza que existia."

**Cura:** quando agente sugere API que voce nao conhece, peca pra ele rodar/verificar antes de assumir.

### Anti-pattern 5: O Globalzao
(Visto na Aba 2 mas vale repetir.) Tudo no global, nada no local. 30 skills carregadas em todo projeto.

**Sintoma:** agente lento, contexto inchado, "ele se perde."

**Cura:** ver Aba 2 — Metodo. Global enxuto, local especifico.

---

## SECAO 8 — Checklist: novo projeto em 8 passos

> Lista numerada com checkboxes. Cada passo com codigo/comando concreto.

Quando voce comeca um projeto novo (ou reorganiza um existente), passa por isso. **Nao pula passo.**

### ✓ 1. Cria a pasta
```bash
mkdir meu-projeto && cd meu-projeto
```

### ✓ 2. Inicializa Git
```bash
git init
git remote add origin git@github.com:voce/meu-projeto.git
```

### ✓ 3. Abre o agente nessa pasta
```bash
claude   # ou: codex
```

### ✓ 4. Cria estrutura local
```bash
mkdir -p .claude/skills    # ou .agents/skills pra Codex
touch CLAUDE.md            # ou AGENTS.md
```

### ✓ 5. Preenche o CLAUDE.md/AGENTS.md
Use o template da Secao 2. **Nao deixa em branco.** Mesmo que basico, melhor que vazio.

### ✓ 6. Adiciona skills relevantes
Escolha 2-4 skills locais alinhadas com o projeto. Ver Aba 5 — Skills.

### ✓ 7. Primeiro commit
```bash
git add .
git commit -m "feat: estrutura inicial + setup do agente"
git push -u origin main
```

### ✓ 8. Valida com prompt simples
Antes de comecar trabalho real, testa o setup com prompt simples:
```
Le o CLAUDE.md/AGENTS.md e me responde:
1. Qual o stack desse projeto?
2. Quais convencoes o time segue?
3. O que NAO fazer?
```

Se o agente responder bem, setup esta valido. Se nao, ajusta o CLAUDE.md/AGENTS.md.

**Agora sim, comeca o trabalho.**

---

## SECAO 9 — O ciclo do dia bem feito

> Bloco final. Sintese pratica de tudo da aba.
> Pode ser visualizado como timeline horizontal (manha → meio → tarde → fim) em desktop, vertical em mobile.

### Manha (15-30min): Planning
- Revisa CLAUDE.md/AGENTS.md (esta atualizado?)
- Define 1-3 tarefas do dia (use a tabela de decisao)
- Pra cada tarefa, escreve 4 pilares no caderno (mental ou papel)

### Meio (foco): Execucao
- Roda o agente pra primeira tarefa
- Aceita ou rejeita diff (com leitura, nao cega)
- Commit atomico
- Proxima tarefa

### Tarde (review): Validacao
- Roda os testes (manualmente ou agente)
- Revisa o que foi feito
- Atualiza CLAUDE.md/AGENTS.md se decisao importante mudou
- Se algo merece virar skill (padrao repetido), anota

### Fim (handoff, 5min): Encerra
- Push final
- Comentario claro no PR / issue tracker
- Limpa contexto da sessao (se vai voltar amanha, ela nao reaproveita)

**Resultado de 1 mes nessa rotina:** 20 dias de trabalho organizado vencem 4 semanas de execucao caotica. Toda vez.

---

## CTA FINAL DA ABA

Voce viu o oficio. Agora aplica:
- **Quer setup pronto?** → Aba 7 (Quiz personalizado)
- **Quer ver as ferramentas em detalhe?** → Aba 4 (Stack)
- **Quer skills pra economizar tempo?** → Aba 5 (Skills)
- **Quer ir mais fundo?** → Aba 6 (Avancado)

---

# Notas pro Claude Code (instrucoes de implementacao)

### Estrutura geral
- Aba mais longa, organizada em 9 secoes claras
- Cada secao com header forte (H2), subsecoes em H3
- Fluxo de leitura: anatomia → templates → decisao → cenarios → regras → erros → checklist → ciclo

### Os 4 pilares (Secao 1)
- 4 cards verticalmente empilhados ou em grid 2x2 em desktop
- Cada card com pergunta-titulo, exemplo ruim, exemplo bom
- Code blocks pros exemplos com botao copy

### Tabela de equivalencia CLAUDE.md/AGENTS.md (Secao 2)
- Tabela limpa, primeira coluna em destaque
- Code block do template generico com botao copy
- Texto "A regra" em destaque visual

### Templates de prompt (Secao 3)
- 6 templates em accordion ou tabs
- Cada um com botao "Copiar template"
- Visual codeblock-like (monospace, fundo escuro)
- **Em mobile:** tabs viram lista vertical com expand

### Tabela de decisao (Secao 4)
- Tabela responsiva
- Em mobile: vira lista de cards (Tipo / Abordagem / Por que)

### Cenarios (Secao 5) — manter UX existente
- Esses sao "cenarios interativos" que ja existem no site
- Cada cenario expande pra mostrar prompt errado/certo lado a lado
- Em mobile: prompts empilhados verticalmente
- Code blocks com syntax highlight

### Regras de ouro (Secao 6)
- 6 cards numerados (numero gigante em ouro)
- 1 linha de regra + 1 paragrafo
- Layout: grid 2x3 em desktop, vertical em mobile

### Anti-patterns (Secao 7)
- Cards com fundo levemente avermelhado (sem agressividade)
- Cada um com nome, sintoma, cura
- 5 cards verticalmente empilhados

### Checklist (Secao 8)
- Lista numerada com checkboxes funcionais (clicavel pra marcar)
- Cada item com code block do comando
- Persistencia em localStorage (usuario marca, salva)

### Ciclo do dia (Secao 9)
- Timeline horizontal em desktop (4 estagios)
- Timeline vertical em mobile
- Visual: linha conectando os estagios, icone pra cada um

### Acessibilidade
- Cenarios e templates: shortcuts de teclado pra expandir/colapsar
- Code blocks: aria-label dizendo que e copiavel
- Checklist: marcacao acessivel por teclado

### Performance
- Lazy load dos cenarios (pesado em conteudo)
- Templates com defer load se nao estiver visivel
