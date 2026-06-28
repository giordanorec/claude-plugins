# Giordano's AI Coding Tools

Ponto central das ferramentas de **AI coding** do Giordano — plugins, skills e MCP
servers. Cada ferramenta vive no seu próprio repositório; este hub **indexa tudo** e
documenta **como instalar em cada ambiente de IA** (Claude Code, Codex, Cursor, ...).

- **Humano?** Use as tabelas abaixo.
- **Agente de IA?** Leia [`AGENTS.md`](./AGENTS.md) + [`catalog.json`](./catalog.json)
  e siga o protocolo de autoinstalação.

## Catálogo

| Ferramenta | O que faz | Repo |
|---|---|---|
| **mad** | Orquestração multi-agente em modo *decanting* (Arquiteto + especialistas via Agent tool, memória em arquivo, trust ladder, dashboard, discovery profundo) | [multiagents-decanting](https://github.com/giordanorec/multiagents-decanting) |
| **brainstorm** | Ideação multi-agente com Quality-Diversity (MAP-Elites, decomposição morfológica, críticos adversariais, dashboard force-graph) | [claude-brainstorm-multiagent](https://github.com/giordanorec/claude-brainstorm-multiagent) |
| **discovery** | Entrevistador de intent antes da spec (postura + rigor) — skill pura, cross-tool | [skills](https://github.com/giordanorec/skills) |
| **multiagentes-giordano** | Fluxo multi-agente legado (tmux + claude -p), Linux-first | [multiagentes-giordano](https://github.com/giordanorec/multiagentes-giordano) |

## Portabilidade (estado real — sem prometer o que não roda)

| Ferramenta | Claude Code | Codex / Cursor / Gemini CLI / Aider / ... |
|---|---|---|
| mad | ✅ plugin | ❌ hoje (só as skills `mad-discovery`/`mad-workflow` portam — roadmap) |
| brainstorm | ✅ plugin | ⚠️ parcial (MCP `brainstorm-tools` + skill portam; agentes/hooks não) |
| discovery | ✅ skill | ✅ skill (cross-tool via `npx skills`) |
| multiagentes-giordano | ✅ plugin | ❌ (tmux + claude -p) |

## Instalação

### No Claude Code (plugins)

Adicione o catálogo **uma vez** e instale o que quiser:

```
/plugin marketplace add giordanorec/ai-coding-tools
/plugin install mad
/plugin install claude-brainstorm-multiagent
/plugin install multiagentes-giordano
```

(Pela CLI: troque `/plugin` por `claude plugin`.) Abra uma sessão nova para carregar.

### Skills cross-tool (Codex, Cursor, Gemini CLI, Aider, Windsurf, ...)

As **skills** funcionam em ~13 ferramentas via o instalador universal:

```
npx skills@latest add giordanorec/skills/discovery
```

Ele pergunta em quais ferramentas instalar.

### MCP servers (cross-tool)

Partes baseadas em **MCP** (ex: `brainstorm-tools`) seguem o padrão aberto MCP —
adicione à config de MCP da sua ferramenta. Detalhes no repo de cada ferramenta.

## Requisitos por ferramenta

- **mad:** Python 3.9+ e `pip install websockets`.
- **brainstorm:** Python 3.10+ e `uv`/`uvx`.
- **discovery:** nenhum (skill pura).
- **multiagentes-giordano:** Linux + tmux + Python.

## Como isto se mantém

`catalog.json` é a fonte da verdade machine-readable; `README.md` e `AGENTS.md`
derivam dele. Plugins novos entram como uma nova entrada em `catalog.json` (e em
`.claude-plugin/marketplace.json` para o install nativo do Claude Code) apontando
para o repo da ferramenta. A pessoa nunca precisa adicionar o marketplace de novo.

## Licença

Cada ferramenta carrega sua própria licença (MIT). © 2026 Giordano Cabral.
