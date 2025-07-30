# Mac App Quick Install Guide

## Manual Downloads (not in install script)

• **Claude Desktop** - https://claude.ai/download
• **Shottr** - https://shottr.cc

## One-Line Installation Script

```bash
/bin/bash -c "
failed_commands=()
echo '🚀 Starting Mac setup...'

# Install Homebrew
if ! /bin/bash -c \"\$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)\"; then
  failed_commands+=('Homebrew installation')
fi

# Setup PATH based on architecture
if [[ \$(uname -m) == 'arm64' ]]; then
  if ! (echo 'eval \"\$(/opt/homebrew/bin/brew shellenv)\"' >> ~/.$(basename $SHELL)rc && eval \"\$(/opt/homebrew/bin/brew shellenv)\"); then
    failed_commands+=('Homebrew PATH setup (Apple Silicon)')
  fi
else
  if ! (echo 'eval \"\$(/usr/local/bin/brew shellenv)\"' >> ~/.$(basename $SHELL)rc && eval \"\$(/usr/local/bin/brew shellenv)\"); then
    failed_commands+=('Homebrew PATH setup (Intel)')
  fi
fi

# Install Node.js
if ! brew install node; then
  failed_commands+=('Node.js installation')
fi

# Install GUI applications
if ! brew install --cask google-chrome warp rectangle alfred slack whatsapp signal telegram sublime-text intellij-idea-ce flux 1password toggl-track todoist handbrake linear-linear losslesscut; then
  failed_commands+=('GUI applications installation')
fi

# Install CLI tools
if ! brew install 1password-cli jq openjdk@17 scrcpy handbrake; then
  failed_commands+=('CLI tools installation')
fi

# Install FVM
if ! (brew tap leoafarias/fvm && brew install fvm); then
  failed_commands+=('FVM installation')
fi

# Install asdf version management tool
if ! brew install asdf; then
  failed_commands+=('asdf installation')
fi

# Install Claude Code
if ! npm install -g @anthropic-ai/claude-code; then
  failed_commands+=('Claude Code installation')
fi

# Install FlutterFire CLI
if ! dart pub global activate flutterfire_cli; then
  failed_commands+=('FlutterFire CLI installation')
fi

# Report results
echo
echo '=================================='
if [ \${#failed_commands[@]} -eq 0 ]; then
  echo '🎉 All installations completed successfully!'
  echo
  echo 'Remember to set JAVA_HOME:'
  echo 'export JAVA_HOME=\"\$(brew --prefix)/opt/openjdk@17\"'
  echo
  echo 'Setup FVM with:'
  echo 'fvm install stable && fvm global stable'
  echo
  echo 'Setup asdf with:'
  echo 'echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ~/.zshrc && source ~/.zshrc'
  echo
  echo 'Note: FlutterFire CLI requires Flutter/Dart to be installed first via FVM'
else
  echo '⚠️  Installation completed with some failures:'
  for cmd in \"\${failed_commands[@]}\"; do
    echo \"  ❌ \$cmd\"
  done
  echo
  echo 'You can retry failed installations manually.'
fi
echo '=================================='
"
```

## Detailed Installation Script

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Add Homebrew to PATH
# For Apple Silicon Macs (M1/M2/M3):
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# For Intel Macs, use this instead:
# echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
# eval "$(/usr/local/bin/brew shellenv)"

# Install Node.js and npm
brew install node

# Install GUI applications
brew install --cask google-chrome
brew install --cask warp
brew install --cask rectangle
brew install --cask alfred
brew install --cask slack
brew install --cask whatsapp
brew install --cask signal
brew install --cask telegram
brew install --cask sublime-text
brew install --cask intellij-idea-ce
brew install --cask flux
brew install --cask 1password
brew install --cask toggl-track
brew install --cask todoist
brew install --cask handbrake
brew install --cask linear-linear
brew install --cask losslesscut

# Install command-line tools
brew install 1password-cli
brew install jq
brew install openjdk@17
# export JAVA_HOME="/opt/homebrew/opt/openjdk@17"
brew install scrcpy
brew install handbrake
brew install cocoapods
brew install gh
brew install firebase-cli

# Install FVM (Flutter Version Management)
brew tap leoafarias/fvm
brew install fvm

# Install asdf version management tool
brew install asdf

# Setup FVM with stable Flutter
# fvm install stable
# fvm global stable
# echo 'export PATH="$HOME/fvm/default/bin:$PATH"' >> ~/.zshrc
# source ~/.zshrc

# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Install FlutterFire CLI
dart pub global activate flutterfire_cli

# Setup asdf (add to shell)
# echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ~/.zshrc
# source ~/.zshrc
```

## Setup Notes

- Restart terminal after Homebrew installation
- Claude Code requires Anthropic API key (set up at console.anthropic.com)
- Run `claude` in your project directory to start Claude Code
- asdf requires shell configuration (see setup command in installation output)