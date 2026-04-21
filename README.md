# claude-plugins — marketplace do giordanorec

Marketplace de plugins Claude Code mantido por
[@giordanorec](https://github.com/giordanorec).

## Como usar

```bash
claude plugin marketplace add giordanorec/claude-plugins
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

---

## Instalação completa em uma máquina nova

Guia passo a passo pra levar o `multiagentes-giordano` (e qualquer outro
plugin deste marketplace) pra uma máquina do zero.

### 1. Dependências do sistema

**Ubuntu/Debian**:
```bash
sudo apt update
sudo apt install -y tmux jq gh util-linux python3 tilix
```

**macOS** (via Homebrew):
```bash
brew install tmux jq gh python3 util-linux
# macOS não tem Tilix — use iTerm2 ou outro emulator favorito.
# O script do dashboard detecta a ausência e avisa.
```

**Arch**:
```bash
sudo pacman -S tmux jq github-cli util-linux python tilix
```

### 2. Instalar o Claude Code

Caso ainda não tenha:

```bash
npm install -g @anthropic-ai/claude-code
claude login
```

Ver instruções oficiais: https://docs.claude.com/en/docs/claude-code/quickstart

### 3. Autenticar o `gh` (pro Arquiteto conseguir criar repo GitHub)

```bash
gh auth login
# escolha: GitHub.com → SSH → autorize no browser
```

### 4. Adicionar o marketplace + instalar o plugin

```bash
claude plugin marketplace add giordanorec/claude-plugins
claude plugin install multiagentes-giordano@giordanorec
```

Confirma:

```bash
claude plugin list | grep multiagentes
# esperado: multiagentes-giordano@giordanorec  v0.1.0  enabled
```

### 5. Usar num projeto novo

```bash
mkdir ~/projetos/meu-projeto
cd ~/projetos/meu-projeto
claude
```

Dentro do Claude Code, invocar o comando:

```
/multiagente-init meu-projeto
```

O Arquiteto assume, faz Discovery (perguntas de escopo/stack/time),
preenche os `docs/` numerados, escolhe os especialistas, cria o repo
GitHub privado, spawna todo mundo, abre o dashboard tmux.

Depois, ao longo do projeto:

- `/multiagente-spawn <nome>` — adicionar especialista novo.
- `/multiagente-dashboard` — reabrir dashboard se fechou.

### 6. Atualizar

Quando uma nova versão for publicada:

```bash
claude plugin marketplace update giordanorec
claude plugin update multiagentes-giordano
```

### 7. Desinstalar

```bash
claude plugin uninstall multiagentes-giordano@giordanorec
claude plugin marketplace remove giordanorec   # opcional
```

## Licença

Cada plugin tem sua própria licença (ver `LICENSE` no repo respectivo).
