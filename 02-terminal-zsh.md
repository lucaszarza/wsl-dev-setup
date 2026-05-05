# Setup Terminal WSL — oh-my-zsh + zoxide + fzf

Guia completo para replicar a configuração do terminal em um novo WSL.

---

## 1. Pré-requisitos

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl wget unzip zsh
```

Definir zsh como shell padrão:

```bash
chsh -s $(which zsh)
```

Feche e reabra o terminal. Na primeira execução do zsh, pressione `q` para sair do wizard.

---

## 2. Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Plugins extras

**zsh-autosuggestions** (sugestões enquanto digita):
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

**zsh-syntax-highlighting** (coloriza comandos válidos/inválidos):
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Tema: Spaceship

```bash
git clone https://github.com/spaceship-prompt/spaceship-prompt.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship-prompt --depth=1

ln -s ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship-prompt/spaceship.zsh-theme \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship.zsh-theme
```

---

## 3. fzf (fuzzy finder)

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install --all
```

Responda `y` para todas as perguntas. O instalador adiciona `[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh` no `.zshrc` automaticamente.

**Atalhos úteis após instalação:**
- `Ctrl+R` — busca no histórico de comandos com fuzzy
- `Ctrl+T` — insere arquivo/diretório selecionado no prompt
- `Alt+C` — navega para diretório com fuzzy

---

## 4. zoxide (substituição inteligente do `cd`)

```bash
sudo apt install -y zoxide
```

A inicialização é feita no `.zshrc` (já incluída na config abaixo).

**Como usar:**
```bash
z workspace        # vai para o diretório que contém "workspace" que você mais visitou
z claude work      # filtra por múltiplos termos
zi                 # abre seletor interativo com fzf
```

---

## 5. Arquivo `.zshrc`

Substitua o conteúdo de `~/.zshrc` pelo seguinte:

```zsh
# Performance optimizations
DISABLE_AUTO_UPDATE="true"
DISABLE_MAGIC_FUNCTIONS="true"
DISABLE_COMPFIX="true"

# Cache completions (recarrega só uma vez por dia)
autoload -Uz compinit
if [ "$(date +'%j')" != "$(stat -c '%j' ~/.zcompdump 2>/dev/null)" ]; then
    compinit
else
    compinit -C
fi

# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="spaceship"

# Spaceship
SPACESHIP_PROMPT_ASYNC=true
SPACESHIP_PROMPT_ADD_NEWLINE=true
SPACESHIP_CHAR_SYMBOL="⚡"
SPACESHIP_PROMPT_ORDER=(
  time
  user
  dir
  git
  line_sep
  char
)

# Plugins (syntax-highlighting deve ser sempre o último)
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)

source $ZSH/oh-my-zsh.sh

# Autosuggestions
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#663399,standout"
ZSH_AUTOSUGGEST_BUFFER_MAX_SIZE="20"
ZSH_AUTOSUGGEST_USE_ASYNC=1

# Expansão de alias com espaço
globalias() {
   if [[ $LBUFFER =~ '[a-zA-Z0-9]+$' ]]; then
       zle _expand_alias
       zle expand-word
   fi
   zle self-insert
}
zle -N globalias
bindkey " " globalias
bindkey "^[[Z" magic-space
bindkey -M isearch " " magic-space

# SSH agent (lazy load)
function _load_ssh_agent() {
    if [ -z "$SSH_AUTH_SOCK" ]; then
        eval "$(ssh-agent -s)" > /dev/null
        ssh-add ~/.ssh/id_github_sign_and_auth 2>/dev/null
    fi
}
autoload -U add-zsh-hook
add-zsh-hook precmd _load_ssh_agent

# PATH
export VOLTA_HOME="$HOME/.volta"
PATH="$VOLTA_HOME/bin:$PATH"
export PATH

# zoxide
eval "$(zoxide init zsh)"

# Aliases
[ -f ~/.zsh_aliases ] && source ~/.zsh_aliases

# fzf
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
```

> **Nota:** blocos do conda, bun, deno são adicionados automaticamente pelos instaladores — não é necessário copiar manualmente.

---

## 6. Arquivo `~/.zsh_aliases`

Crie o arquivo:

```bash
touch ~/.zsh_aliases
```

Conteúdo:

```zsh
# Claude Code
alias cl="claude"
alias clc="claude --continue"
alias clp="claude --print"

# Navegação
alias ..="cd .."
alias ...="cd ../.."

# Git
alias gs="git status"
alias gd="git diff"
alias gl="git log --oneline -15"
alias gb="git branch"

# Python
alias py="python3"

# WSL utils
alias exp="explorer.exe ."    # abre diretório atual no Windows Explorer
alias clip="clip.exe"         # copia para clipboard Windows: cat file | clip
```

---

## 7. Aplicar as configurações

```bash
source ~/.zshrc
```

---

## 8. Verificar instalação

```bash
fzf --version      # deve retornar versão (ex: 0.61.1)
zoxide --version   # deve retornar versão (ex: 0.9.3)
z --help           # deve mostrar ajuda do zoxide
echo $ZSH_THEME    # deve retornar "spaceship"
```

---

## Referências

- [Oh My Zsh](https://ohmyz.sh)
- [Spaceship Prompt](https://spaceship-prompt.sh)
- [fzf](https://github.com/junegunn/fzf)
- [zoxide](https://github.com/ajeetdsouza/zoxide)
