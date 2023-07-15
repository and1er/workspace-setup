# macOS setup

## Install brew

See [Install Homebrew](https://brew.sh/)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Brew packages installation

See [Homebrew Formulae](https://formulae.brew.sh/).

```bash
brew install --cask iterm2
brew install --cask flycut
brew install zsh-autosuggestions
brew install --cask visual-studio-code
brew install --cask libreoffice
brew install --cask zoom
brew install gnupg
brew install bat
```

## Docker setup

### Installation

```bash
brew install docker
brew install colima
```

Also add to `~/.zshrc`

```bash
export DOCKER_HOST="unix://${HOME}/.colima/default/docker.sock"
```

### Run

```bash
colima start --cpu 4 --memory 2
```
