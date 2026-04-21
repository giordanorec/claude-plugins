# claude-plugins — marketplace do giordanorec

Marketplace de plugins Claude Code mantido por
[@giordanorec](https://github.com/giordanorec).

## Como adicionar este marketplace

No Claude Code:

```bash
claude plugin marketplace add giordanorec/claude-plugins
```

Depois de adicionar, os plugins ficam disponíveis pra instalação:

```bash
claude plugin install <nome>@giordanorec
```

## Plugins disponíveis

### [`multiagentes-giordano`](https://github.com/giordanorec/multiagentes-giordano)

Fluxo multi-agente com sessões persistentes. Arquiteto coordena um time
de especialistas, cada um é uma sessão Claude Code separada, comunicação
via arquivos (`specs/`, `reports/`, `memory/`). Dashboard tmux ao vivo
mostra todos os agentes trabalhando em paralelo, com texto formatado
semanticamente (tool calls com emoji + cor, diff visual, badges).

**Instala**:

```bash
claude plugin install multiagentes-giordano@giordanorec
```

**Comandos**:
- `/multiagente-init [nome]` — Discovery + setup inteiro + spawn + dashboard.
- `/multiagente-spawn <agente>` — spawna especialista num projeto já iniciado.
- `/multiagente-dashboard` — abre (ou reabre) o dashboard tmux.

## Licença

Cada plugin tem sua própria licença (ver `LICENSE` no repo respectivo).
