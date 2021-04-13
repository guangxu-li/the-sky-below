#software-development #python #development-environment

# Setup [[Python]] Environment

## Introduction

Things could be complicated for Apple ecosystem since macos has built-in [[Python]] environment. The built-in Python 2.7 locating in `/usr/bin/` should never be touched. It's has been deprecated, but Apple still include it for compatibility purpose.

For some situation, xcode `CommandLineTools` is required to be installed, which comes along with a Python 3.x also locating at `/usr/bin`.

To not make things confused, installing Python run time to other paths is recommended. To make it easier to maintain multiple version Python and environments,  [pyenv](https://github.com/pyenv/pyenv) and [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) is helpful to achieve the goal.

## Installation for MacOS: pyenv

### Prerequisites:

For `pyenv` to install python correctly, install the **Python build dependencies**:


1. Install Xcode Command Line Tools (`xcode-select --install`) and [Homebrew](https://brew.sh)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Install build dependencies:

```bash
brew install openssl readline sqlite3 xz zlib
```

### pyenv
1. Install pyenv using homebrew:
```bash
brew update
brew install pyenv
```

2. Add `pyenv init` to shell to enable shims and autocompletion. Make sure `eval "$(pyenv init-)"` is placed toward the end of the shell configuration file since it manipulates `PATH` during the initialization.
	- For **bash**:
		```bash
		echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\\n  eval "$(pyenv init -)"\\nfi' \>> ~/.bash\_profile
		```
	- For **zsh**:
		```bash
		echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\\n  eval "$(pyenv init -)"\\nfi' \>> ~/.zshrc
		```
	- For **Fish Shell**:
			```bash
			echo \-e '\\n\\n# pyenv init\\nif command -v pyenv 1>/dev/null 2>&1\\n  pyenv init - | source\\nend' \>> ~/.config/fish/config.fish
			```
3. Restart the shell so the path changes take effect.
	```bash
	exec "$SHELL"
	```
4. Install Python versions into `$(pyenv root)/versions`. For example, to download and install `Python 3.9.1`, run:
	```bash
	pyenv install 3.9.1
	```

### Upgrading

Use brew to upgrade:
```bash
brew upgrade pyenv
```

### Uninstalling

1. Remove the `pyenv init` line from shell startup configuration. This will remove pyenv shims directory from PATH, and future invocations like `python` will execute the system Python version, as before pyenv.
2. To completely **uninstall** pyenv, perform step 1 and then remove its root directory. This will **delete all Python versions** that were installed under `$(pyenv root)/versions/` directory:
	```bash
	rm -rf $(pyenv root)	
	brew uninstall pyenv
	```
	
## Installation for MacOS: pyenv-virtualenv

1. Install `pyenv-virtualenv` using homebrew:
	```bash
	brew install pyenv-virtualenv	
	```
2. Add `pyenv virtualenv-init` to shell to enable auto-activation of virtualenvs. This is entirely optional but pretty useful.
	```bash
	echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc	
	```
	
3. Restart shell to enable:
	```bash
	exec "$SHELL"	
	```