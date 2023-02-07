# 支給マシン初期構築（Ruby on WSL）

## vscode 設定

### プラグイン類

```bash
# vs code extensions
 $ code --list-extensions | xargs -L 1 echo code --install-extension
 code --install-extension aki77.rails-db-schema
 code --install-extension bung87.rails
 code --install-extension bung87.vscode-gemfile
 code --install-extension castwide.solargraph
 code --install-extension eamodio.gitlens
 code --install-extension gencay.vscode-chatgpt
 code --install-extension GrapeCity.gc-excelviewer
 code --install-extension mechatroner.rainbow-csv
 code --install-extension mhutchie.git-graph
 code --install-extension misogi.ruby-rubocop
 code --install-extension mosapride.zenkaku
 code --install-extension mtxr.sqltools
 code --install-extension oderwat.indent-rainbow
 code --install-extension rebornix.ruby
 code --install-extension ryu1kn.partial-diff
 code --install-extension shardulm94.trailing-spaces
 code --install-extension sianglim.slim
 code --install-extension sporto.rails-go-to-spec
 code --install-extension TabNine.tabnine-vscode
 code --install-extension wingrunr21.vscode-ruby
```

### solargraph

```json
// .vscode/settings.json
{
  "solargraph.externalServer": {
    "host": "localhost",
    "port": 7658
  },
  "solargraph.transport": "external"
}
```

```yml
# docker-compose.yml

solargraph:
  build: .
  command: solargraph socket --host=0.0.0.0 --port=7658
  restart: always
  volumes:
    - .:/app
  ports:
    - "7658:7658"
```

```dockerfile
# Dockerfile

FROM ruby:latest
WORKDIR /app
RUN gem install solargraph
EXPOSE 7658
```

## .bashrc

### Git

```bash
# on command line
cd ~
curl -o .git-completion.sh \
    https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
curl -o .git-prompt.sh \
    https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh

git config --local commit.template .commit_template
```

```bash
# git bash settings

if [ -f ~/.git-completion.sh ]; then
  source ~/.git-completion.sh
fi

if [ -f ~/.git-prompt.sh ]; then
  source ~/.git-prompt.sh
fi

#GIT_PS1_SHOWDIRTYSTATE=true
#GIT_PS1_SHOWUNTRACKEDFILES=true
#GIT_PS1_SHOWSTASHSTATE=true
#GIT_PS1_SHOWUPSTREAM=auto

PS1='[\[\033[32m\]\u@\h\[\033[00m\] \[\033[33m\]\w\[\033[1;36m\]$(\_\_git_ps1 " (%s)")\[\033[00m\]]\n\$ '
```
