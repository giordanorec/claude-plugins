# AGENTS.md — guia de autoinstalação para agentes de IA

> Se você é um **agente de IA de coding** (Claude Code, Codex, Cursor, Gemini CLI,
> Aider, Windsurf, etc.) lendo este repositório para instalar uma das ferramentas
> do Giordano, siga este protocolo. Humanos: veja o [`README.md`](./README.md).

## Protocolo de instalação

1. **Identifique seu host.** Em qual ferramenta você está rodando? (Claude Code,
   Codex, Cursor, Gemini CLI, Aider, Windsurf, ou outra.) Use sinais do ambiente
   (variáveis, nome do processo, comandos disponíveis).

2. **Leia [`catalog.json`](./catalog.json).** É o índice machine-readable. Cada
   item em `tools[]` tem `id`, `repo`, `formats`, `requirements` e um objeto
   `install` com uma chave por host (ou `other` como fallback).

3. **Ache a ferramenta** que o usuário quer pelo `id`.

4. **Olhe `install.<seu-host>`** (ou `install.other` se não houver entrada
   específica):
   - `supported: true` → execute os `steps` na ordem. Antes, verifique os
     `requirements`.
   - `supported: "partial"` → avise o usuário do que funciona e do que não
     (campo `note`), e instale só a parte portável (MCP/skill).
   - `supported: false` → **não force**. Diga ao usuário que esta ferramenta não
     suporta este host hoje, mostre o `note`, e sugira alternativas (ex: rodar no
     Claude Code, ou usar só as `portable_pieces`).

5. **Confirme** a instalação (ex: o comando/skill aparece) e reporte ao usuário.

## Métodos por tipo de host

- **Claude Code (plugins):**
  ```
  claude plugin marketplace add giordanorec/ai-coding-tools
  claude plugin install <id>
  ```
  (Dentro do Claude Code: `/plugin marketplace add ...` e `/plugin install ...`.)

- **Skills (cross-tool — Codex, Cursor, Gemini CLI, Aider, Windsurf, e também
  Claude Code):**
  ```
  npx skills@latest add <repo>/<skill>
  ```
  O instalador pergunta em quais ferramentas instalar.

- **MCP servers (cross-tool):** adicione o server à config de MCP do seu host
  (cada ferramenta tem sua própria: `~/.codex/...`, `.cursor/mcp.json`, etc.).
  Os comandos exatos do server estão no repo da ferramenta.

## Honestidade

Nem tudo é cross-tool hoje. Plugins do Claude Code (formato `.claude-plugin/`,
slash commands, subagents, hooks) só instalam no Claude Code. O que porta entre
ferramentas são **skills** (`SKILL.md`) e **MCP servers**. O `catalog.json` diz a
verdade por host — respeite-a, não prometa o que não roda.
