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

### Atalho (Ubuntu/Debian) — 1 linha

```bash
curl -sSL https://gist.githubusercontent.com/giordanorec/16999a7f1c24c62de46e491191d7c29e/raw/install-multiagentes-giordano.sh | bash
```

O script instala deps, adiciona o marketplace e o plugin. Você só roda
`gh auth login` depois se ainda não rodou nunca. Pra outras distros ou
controle fino, siga o passo a passo abaixo.

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

## Troubleshooting

### `Host key verification failed` ao instalar

Máquina nova sem a chave do github.com em `~/.ssh/known_hosts`:

```bash
mkdir -p ~/.ssh
ssh-keyscan -H github.com >> ~/.ssh/known_hosts
```

### `git@github.com: Permission denied (publickey)` ao instalar

Máquina sem chave SSH pessoal configurada no GitHub. Como o repo é
**público**, dá pra forçar HTTPS (sem precisar de autenticação):

```bash
git config --global url."https://github.com/".insteadOf "git@github.com:"
git config --global url."https://github.com/".insteadOf "ssh://git@github.com/"
```

Depois retente `claude plugin install multiagentes-giordano@giordanorec`.
O script de instalação 1-linha já detecta e aplica esse fix
automaticamente se SSH não estiver funcionando.

### `gh` não autenticado

Se o Arquiteto falhar ao criar repo GitHub:

```bash
gh auth login
# escolha GitHub.com → SSH → autorize no browser
```

## Licença

Cada plugin tem sua própria licença (ver `LICENSE` no repo respectivo).
