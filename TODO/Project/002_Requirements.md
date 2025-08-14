


### Orchestratror



### Front-End ()
Machine that supports the front end:
- NodeJs
```
# install nvm which manages verions of nodejs and 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# After running the installer, add this to your `~/.bashrc` (or `~/.zshrc` if you're using zsh): NOTE. THE INSTALLER ALREADY ADDED THE LINES, just refres

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
source ~/.bashrc


#after:
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# later
nvm install --lts  # latest
nvm use --lts
nvm alias default lts/*


```
		- Tailwind
```
# In frontend directory
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
npm install react-router-dom

```

React dev tools
https://addons.mozilla.org/en-US/firefox/addon/react-devtools/

- Nmp

- **Vite** (to set up react)

### Back-End (auth-login, api-logic, data access)

ensurepip (to create or load python3 venv)

```
apt install python3.10-venv
pip install fastapi uvicorn python-dotenv
```

