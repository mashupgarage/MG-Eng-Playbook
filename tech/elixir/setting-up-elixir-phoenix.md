# Set Phoenix project up and running

This topic tackles on phoenix framework installation thru <a href="https://asdf-vm.com/guide/introduction.html" target="_blank">asdf</a> version manager.

## Prerequisites

- Asdf tool version manager
- Erlang
- Elixir

## Asdf setup

1. Install Dependencies

asdf primarily requires git & curl. Here is a non-exhaustive list of commands to run for your package manager (some might automatically install these tools in later steps).

| OS    | Package manager | Command                         |
|-------|-----------------|---------------------------------|
| Linux | Aptitude        | sudo apt install curl git       |
| Linux | Pacman          | sudo pacman -S curl git         |
| MacOS | Homebrew        | brew install coreutils curl git |


> Note - Windows OS have curl installed for windows 10 and later. While git have exe installer in here https://git-scm.com/download/win`

2. Download asdf

Official Download
```
git clone https://github.com/asdf-vm/asdf.git ~/.asdf
```
We highly recommend using the official git method.

<b> Community Supported Download Methods </b>

| Method   | Command                                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------------------|
| Homebrew | brew install asdf                                                                                                             |
| Pacman   | git clone https://aur.archlinux.org/asdf-vm.git &amp;&amp; cd asdf-vm &amp;&amp; makepkg -si or use your preferred AUR helper |

3. Install asdf

<b>Bash</b>

Add the following to ~/.bashrc:
```
. "$HOME/.asdf/asdf.sh"
```

Completions must be configured by adding the following to your .bashrc:
```
. "$HOME/.asdf/completions/asdf.bash"
```

<b>Homebrew & ZSH (MacOS)</b>

Add asdf.sh to your ~/.zshrc with:
```
echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ${ZDOTDIR:-~}/.zshrc
```

> Completions are configured by either a ZSH Framework asdf or will need to be configured as per Homebrew's instructions. If you are using a ZSH Framework the associated plugin for asdf may need to be updated to use the new ZSH completions properly via fpath. The Oh-My-ZSH asdf plugin is yet to be updated, see ohmyzsh/ohmyzsh#8837.

## Project setup

1. Install plugins

```
asdf plugin-add erlang
asdf plugin-add elixir
```