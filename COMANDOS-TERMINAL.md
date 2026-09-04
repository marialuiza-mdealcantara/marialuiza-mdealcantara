# 🖥️ Cola de Comandos do Terminal

> Referência pessoal de comandos usados em projetos de desenvolvimento, Git/GitHub, Python, FastAPI, Node.js, n8n, Docker e tarefas comuns no terminal.
>
> **Objetivo:** poder consultar rapidamente um comando sem precisar perguntar novamente o que ele faz.

---

## 📌 Índice

- [1. Navegação e arquivos](#1--navegação-e-arquivos)
- [2. Git e GitHub](#2--git-e-github)
- [3. Python](#3--python)
- [4. Ambiente virtual](#4--ambiente-virtual)
- [5. pip](#5--pip)
- [6. Pytest](#6--pytest)
- [7. FastAPI e Uvicorn](#7--fastapi-e-uvicorn)
- [8. Node.js e npm](#8--nodejs-e-npm)
- [9. NVM](#9--nvm)
- [10. n8n](#10--n8n)
- [11. PM2](#11--pm2)
- [12. Docker](#12--docker)
- [13. PowerShell e comandos úteis](#13--powershell-e-comandos-úteis)
- [14. Fluxos prontos](#14--fluxos-prontos)
- [15. Comandos perigosos](#15--comandos-perigosos)
- [16. Mini cola](#16--mini-cola)

---

# 1. 📁 Navegação e arquivos

Comandos básicos para se movimentar pelo computador usando o terminal.

| Comando | O que faz |
|---|---|
| `pwd` | Mostra o caminho da pasta atual. |
| `ls` | Lista arquivos e pastas. |
| `ls -la` | Lista arquivos, inclusive ocultos. |
| `cd nome-da-pasta` | Entra em uma pasta. |
| `cd ..` | Volta uma pasta. |
| `cd ~` | Vai para a pasta inicial do usuário. |
| `cd caminho/para/projeto` | Vai diretamente para uma pasta. |
| `mkdir nome-da-pasta` | Cria uma pasta. |
| `touch arquivo.txt` | Cria um arquivo vazio. |
| `clear` | Limpa a tela do terminal. |
| `exit` | Encerra a sessão atual do terminal. |

### Exemplos

```bash
cd projeto
```

```bash
cd ..
```

```bash
mkdir meu-projeto
```

```bash
ls
```

> **Windows / PowerShell:** alguns comandos têm equivalentes próprios. `dir` também lista arquivos, e `Get-Location` mostra a pasta atual.

---

# 2. 🐙 Git e GitHub

Git é o controle de versão. GitHub é o serviço remoto onde o repositório pode ser hospedado e compartilhado.

## 2.1 Configuração inicial

| Comando | O que faz |
|---|---|
| `git --version` | Mostra a versão do Git. |
| `git config --global user.name "Seu Nome"` | Define o nome usado nos commits. |
| `git config --global user.email "seu@email.com"` | Define o e-mail usado nos commits. |
| `git init` | Inicializa um repositório Git na pasta atual. |
| `git remote -v` | Mostra os repositórios remotos configurados. |
| `git remote add origin URL` | Conecta o repositório local ao remoto. |

### Exemplo

```bash
git init
```

```bash
git remote add origin https://github.com/usuario/repositorio.git
```

---

## 2.2 Ver o que está acontecendo

| Comando | O que faz |
|---|---|
| `git status` | Mostra o estado dos arquivos e da área de staging. |
| `git diff` | Mostra alterações ainda não adicionadas ao staging. |
| `git diff --staged` | Mostra alterações que já estão no staging. |
| `git log` | Mostra o histórico de commits. |
| `git log --oneline` | Mostra o histórico resumido. |
| `git log --oneline --graph --all` | Mostra um histórico visual de branches e commits. |

### O comando mais importante no dia a dia

```bash
git status
```

Use quando pensar:

> **“O que eu alterei? O que já está preparado? O que falta fazer?”**

---

## 2.3 Adicionar e criar commits

| Comando | O que faz |
|---|---|
| `git add .` | Adiciona todas as alterações ao staging. |
| `git add arquivo.py` | Adiciona somente um arquivo. |
| `git commit -m "mensagem"` | Cria um commit. |

### Exemplo

```bash
git add .
git commit -m "Adiciona cadastro de produtos"
```

---

## 2.4 Enviar para o GitHub

| Comando | O que faz |
|---|---|
| `git push` | Envia commits para o remoto configurado. |
| `git push -u origin main` | Envia a `main` pela primeira vez e define o upstream. |
| `git push origin nome-da-branch` | Envia uma branch específica. |

### Primeiro push de um projeto

```bash
git branch -M main
git push -u origin main
```

Depois do upstream configurado, normalmente basta:

```bash
git push
```

> **Importante:** `git commit` salva localmente. `git push` envia para o GitHub. O push **não acontece automaticamente** a cada novo commit.

---

## 2.5 Baixar e atualizar um projeto

| Comando | O que faz |
|---|---|
| `git clone URL` | Baixa um repositório remoto para o computador. |
| `git pull` | Busca alterações remotas e integra no trabalho local. |
| `git fetch` | Busca informações do remoto sem alterar o código de trabalho. |

### Clonar

```bash
git clone https://github.com/usuario/repositorio.git
```

### Atualizar

```bash
git pull
```

---

## 2.6 Branches

| Comando | O que faz |
|---|---|
| `git branch` | Lista branches locais. |
| `git branch nome` | Cria uma branch. |
| `git switch nome` | Muda para uma branch existente. |
| `git switch -c nome` | Cria e muda para a branch. |
| `git checkout -b nome` | Forma tradicional de criar e mudar para uma branch. |
| `git merge nome` | Mescla uma branch na branch atual. |
| `git branch -d nome` | Exclui uma branch local já integrada. |

### Exemplo de feature

```bash
git switch -c feature-cadastro-produto
```

ou:

```bash
git checkout -b feature-cadastro-produto
```

Depois:

```bash
git add .
git commit -m "Adiciona cadastro de produto"
git push -u origin feature-cadastro-produto
```

---

## 2.7 Desfazer alterações

| Comando | O que faz |
|---|---|
| `git restore arquivo.py` | Descarta alterações locais do arquivo que ainda não foram commitadas. |
| `git restore --staged arquivo.py` | Retira o arquivo do staging sem apagar as alterações. |
| `git reset --soft HEAD~1` | Desfaz o último commit, mantendo as alterações no staging. |
| `git reset --mixed HEAD~1` | Desfaz o último commit e tira as alterações do staging. |
| `git reset --hard HEAD~1` | Desfaz o commit e descarta alterações. ⚠️ |
| `git revert ID_DO_COMMIT` | Cria um novo commit que desfaz outro commit. |

### Regra prática

- **Errei antes do commit?** → `git restore`
- **Quero refazer o último commit local?** → `git reset`
- **Preciso desfazer algo que já foi compartilhado?** → normalmente `git revert`

> ⚠️ `git reset --hard` pode causar perda de alterações. Use com cuidado.

---

## 2.8 Resolver conflito de merge

Fluxo básico:

```bash
git status
```

1. Abra os arquivos indicados pelo Git.
2. Resolva os trechos marcados como conflito.
3. Salve os arquivos.
4. Adicione os arquivos resolvidos:

```bash
git add .
```

5. Finalize o merge:

```bash
git commit -m "Resolve conflitos de merge"
```

---

# 3. 🐍 Python

## 3.1 Verificar instalação

| Comando | O que faz |
|---|---|
| `python --version` | Mostra a versão do Python. |
| `python3 --version` | Verifica o Python 3 em sistemas que usam esse comando. |
| `where python` | Mostra onde o Python está no Windows. |
| `where.exe python` | Outra forma de localizar o Python no Windows. |
| `which python` | Mostra o caminho do Python em Linux/macOS. |

### Exemplo

```bash
python --version
```

---

## 3.2 Executar Python

| Comando | O que faz |
|---|---|
| `python main.py` | Executa um arquivo Python. |
| `python -m modulo` | Executa um módulo usando o Python atual. |
| `python -c "print('Olá')"` | Executa um pequeno trecho de código diretamente no terminal. |

### Exemplo

```bash
python main.py
```

---

# 4. 🧪 Ambiente virtual

O ambiente virtual (`venv`) isola as dependências do projeto das dependências do computador.

## Criar

```bash
python -m venv .venv
```

## Ativar no Windows PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

ou, em alguns terminais Windows:

```powershell
.\.venv\Scripts\activate
```

## Ativar no Linux/macOS

```bash
source .venv/bin/activate
```

## Sair do ambiente virtual

```bash
deactivate
```

### Como saber se está ativado?

Normalmente o terminal mostra algo parecido com:

```text
(.venv) PS C:\Users\Malu\projeto>
```

---

# 5. 📦 pip

`pip` é o gerenciador de pacotes Python.

| Comando | O que faz |
|---|---|
| `pip install pacote` | Instala uma biblioteca. |
| `python -m pip install pacote` | Instala uma biblioteca usando o Python atual. |
| `pip install -r requirements.txt` | Instala todas as dependências listadas no arquivo. |
| `pip freeze` | Lista os pacotes instalados. |
| `pip freeze > requirements.txt` | Gera/atualiza o arquivo de dependências. |
| `pip uninstall pacote` | Remove uma biblioteca. |
| `pip show pacote` | Mostra informações do pacote. |
| `python -m pip install --upgrade pip` | Atualiza o pip. |

### Instalar dependências de um projeto

```bash
pip install -r requirements.txt
```

### Gerar `requirements.txt`

```bash
pip freeze > requirements.txt
```

---

# 6. 🧪 Pytest

Usado para executar testes automatizados em Python.

| Comando | O que faz |
|---|---|
| `pytest` | Executa os testes. |
| `pytest -v` | Executa com mais detalhes. |
| `pytest arquivo.py` | Executa um arquivo específico de testes. |
| `pytest -k nome` | Executa testes que correspondem ao termo informado. |
| `pytest --cov` | Executa testes com cobertura, se o plugin estiver instalado. |

### Exemplo

```bash
pytest -v
```

---

# 7. 🚀 FastAPI e Uvicorn

Para executar uma API FastAPI localmente.

| Comando | O que faz |
|---|---|
| `uvicorn main:app --reload` | Inicia a API e recarrega quando o código muda. |
| `python -m uvicorn main:app --reload` | Faz a mesma execução usando o Python atual. |
| `uvicorn main:app --host 0.0.0.0 --port 8000` | Define host e porta manualmente. |

### Desenvolvimento

```bash
uvicorn main:app --reload
```

### URLs comuns

```text
http://127.0.0.1:8000
```

Documentação Swagger:

```text
http://127.0.0.1:8000/docs
```

Documentação alternativa:

```text
http://127.0.0.1:8000/redoc
```

---

# 8. 🌐 Node.js e npm

## Verificar instalação

| Comando | O que faz |
|---|---|
| `node -v` | Mostra a versão do Node.js. |
| `npm -v` | Mostra a versão do npm. |

## Pacotes

| Comando | O que faz |
|---|---|
| `npm install` | Instala as dependências descritas no projeto. |
| `npm install pacote` | Instala um pacote. |
| `npm install -g pacote` | Instala um pacote globalmente. |
| `npm uninstall pacote` | Remove um pacote. |
| `npm list -g --depth=0` | Lista pacotes globais de forma resumida. |

### Exemplos

```bash
node -v
npm -v
```

```bash
npm install
```

```bash
npm install express
```

---

# 9. 🔄 NVM

NVM permite instalar e alternar entre versões do Node.js.

| Comando | O que faz |
|---|---|
| `nvm install 18` | Instala o Node.js 18. |
| `nvm use 18` | Passa a usar a versão 18. |
| `nvm list` | Lista as versões disponíveis/instaladas, dependendo da implementação. |
| `nvm alias default 18` | Define a versão padrão no NVM compatível com esse comando. |
| `source ~/.bashrc` | Recarrega configurações do shell em Linux. |

### Exemplo

```bash
nvm install 18
nvm use 18
```

> ⚠️ **Atenção:** existem implementações diferentes de NVM para Windows e Unix. Os comandos podem variar conforme a versão instalada.

---

# 10. ⚙️ n8n

Comandos comuns para executar e verificar o n8n via terminal.

| Comando | O que faz |
|---|---|
| `n8n --version` | Mostra a versão instalada. |
| `n8n` | Inicia o n8n. |
| `n8n start` | Inicia o n8n. |

### Iniciar

```bash
n8n
```

### Ver versão

```bash
n8n --version
```

### Logs em segundo plano (Linux)

```bash
nohup n8n > n8n.log 2>&1 &
```

Acompanhar o log:

```bash
tail -f n8n.log
```

Parar um processo em primeiro plano:

```text
Ctrl + C
```

---

# 11. 🔧 PM2

PM2 pode manter processos Node.js em execução e gerenciá-los.

| Comando | O que faz |
|---|---|
| `npm install -g pm2` | Instala o PM2 globalmente. |
| `pm2 start n8n` | Inicia o n8n pelo PM2. |
| `pm2 list` | Lista os processos gerenciados. |
| `pm2 logs` | Mostra os logs. |
| `pm2 restart n8n` | Reinicia o processo. |
| `pm2 stop n8n` | Para o processo. |
| `pm2 save` | Salva os processos configurados. |

### Exemplo

```bash
pm2 start n8n
pm2 save
```

---

# 12. 🐳 Docker

## Verificar instalação

```bash
docker --version
```

## Containers

| Comando | O que faz |
|---|---|
| `docker ps` | Lista containers em execução. |
| `docker ps -a` | Lista todos os containers, inclusive parados. |
| `docker start nome` | Inicia um container existente. |
| `docker stop nome` | Para um container. |
| `docker restart nome` | Reinicia um container. |
| `docker logs nome` | Mostra os logs do container. |
| `docker exec -it nome bash` | Abre um terminal dentro do container. |

## Imagens

| Comando | O que faz |
|---|---|
| `docker images` | Lista imagens locais. |
| `docker pull imagem` | Baixa uma imagem. |
| `docker build -t nome:tag .` | Cria uma imagem a partir do Dockerfile. |

## Criar e executar

```bash
docker run nome-da-imagem
```

## Docker Compose

| Comando | O que faz |
|---|---|
| `docker compose up` | Inicia os serviços definidos no Compose. |
| `docker compose up -d` | Inicia em segundo plano. |
| `docker compose down` | Para e remove os serviços. |
| `docker compose ps` | Mostra o estado dos serviços. |
| `docker compose logs` | Mostra os logs dos serviços. |
| `docker compose logs -f` | Acompanha os logs em tempo real. |

### Exemplo

```bash
docker compose up -d
```

---

# 13. 🪟 PowerShell e comandos úteis

| Comando | O que faz |
|---|---|
| `Get-Location` | Mostra o diretório atual. |
| `Get-ChildItem` | Lista arquivos e pastas. |
| `Get-History` | Mostra o histórico de comandos do PowerShell. |
| `Clear-Host` | Limpa a tela. |
| `Get-Process` | Lista processos em execução. |
| `Get-Command python` | Mostra qual comando Python está sendo encontrado. |
| `where.exe python` | Mostra caminhos encontrados para o Python. |

### Teclas úteis

| Atalho | O que faz |
|---|---|
| `Ctrl + C` | Interrompe um comando/processo em execução. |
| `Ctrl + L` | Limpa a tela em vários terminais. |
| `Tab` | Autocompleta nomes de arquivos, pastas e comandos. |
| `↑` / `↓` | Navega pelo histórico de comandos. |

---

# 14. 📋 Fluxos prontos

## 14.1 Criar um projeto Python do zero

```bash
mkdir meu-projeto
cd meu-projeto
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Depois:

```bash
pip install -r requirements.txt
```

ou, se ainda não existir:

```bash
pip install fastapi uvicorn pytest
```

---

## 14.2 Criar projeto e subir para o GitHub

```bash
mkdir meu-projeto
cd meu-projeto
```

```bash
git init
git add .
git commit -m "Primeiro commit"
git branch -M main
git remote add origin URL_DO_REPOSITORIO
git push -u origin main
```

### Fluxo depois que o projeto já está conectado

```bash
git status
git add .
git commit -m "Descreve a alteração"
git push
```

---

## 14.3 Baixar um projeto do GitHub

```bash
git clone URL_DO_REPOSITORIO
cd nome-do-projeto
```

Depois:

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

---

## 14.4 Criar uma branch para uma nova funcionalidade

```bash
git switch -c feature-nova-funcionalidade
```

Fazer alterações:

```bash
git status
git add .
git commit -m "Adiciona nova funcionalidade"
git push -u origin feature-nova-funcionalidade
```

Depois, abrir o Pull Request no GitHub.

---

## 14.5 Atualizar a `main` antes de começar uma tarefa

```bash
git switch main
git pull
```

Criar sua branch:

```bash
git switch -c feature-minha-tarefa
```

---

## 14.6 Rodar uma API FastAPI

```bash
.\.venv\Scripts\Activate.ps1
```

```bash
uvicorn main:app --reload
```

Abrir:

```text
http://127.0.0.1:8000/docs
```

---

## 14.7 Rodar os testes

```bash
.\.venv\Scripts\Activate.ps1
pytest -v
```

---

## 14.8 Atualizar dependências do projeto

```bash
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Depois de instalar algo novo:

```bash
pip freeze > requirements.txt
```

---

# 15. ⚠️ Comandos perigosos

Alguns comandos podem apagar arquivos, alterar histórico ou causar perda de dados.

## Git

```bash
git reset --hard
```

Pode descartar alterações.

```bash
git clean -fd
```

Remove arquivos e diretórios não rastreados.

## Docker

```bash
docker system prune
```

Pode remover recursos Docker não utilizados.

## Terminal

Comandos de exclusão como `rm -rf` devem ser usados com extremo cuidado.

> **Regra:** antes de executar um comando destrutivo, pare e confirme exatamente o que ele vai apagar ou alterar.

---

# 16. ⭐ Mini cola

Quando você esquecer, pense no que quer fazer:

| Quero... | Comando |
|---|---|
| 📁 Ver onde estou | `pwd` |
| 📂 Ver arquivos | `ls` |
| 📂 Entrar em pasta | `cd pasta` |
| 🔙 Voltar pasta | `cd ..` |
| 🐙 Ver situação do Git | `git status` |
| ➕ Preparar alterações | `git add .` |
| 💾 Criar commit | `git commit -m "mensagem"` |
| ☁️ Enviar ao GitHub | `git push` |
| ⬇️ Atualizar do GitHub | `git pull` |
| 🌿 Criar branch | `git switch -c nome` |
| 📥 Clonar projeto | `git clone URL` |
| 🐍 Ver Python | `python --version` |
| 🧪 Criar ambiente | `python -m venv .venv` |
| ✅ Ativar ambiente (Windows) | `.\.venv\Scripts\Activate.ps1` |
| 📦 Instalar dependências | `pip install -r requirements.txt` |
| 🧪 Rodar testes | `pytest -v` |
| 🚀 Rodar FastAPI | `uvicorn main:app --reload` |
| 🌐 Ver Node | `node -v` |
| 📦 Ver npm | `npm -v` |
| ⚙️ Ver n8n | `n8n --version` |
| 🐳 Ver Docker | `docker --version` |
| 🛑 Parar processo | `Ctrl + C` |

---

## 🧠 Ordem mental para Git

Quando terminar uma alteração, pense:

```text
1. git status
       ↓
2. git add .
       ↓
3. git commit -m "..."
       ↓
4. git push
```

Quando for começar a trabalhar:

```text
1. git switch main
       ↓
2. git pull
       ↓
3. git switch -c feature-minha-tarefa
```

---

## 📚 Regra de ouro

> **`status` → `add` → `commit` → `push`**
>
> **`pull` antes de começar a trabalhar em algo novo.**
>
> **`revert` para desfazer alterações já compartilhadas, quando apropriado.**
>
> **Cuidado com comandos que apagam ou reescrevem histórico.**

---

## 🔄 Manutenção desta cola

Quando um comando novo aparecer em um projeto, adicione aqui usando este formato:

```markdown
| `comando` | Explicação curta do que ele faz. |
```

Assim este arquivo pode evoluir junto com seus estudos e projetos.

---

**Arquivo:** `COMANDOS-TERMINAL.md`  
**Uso:** referência pessoal de terminal para estudos e projetos.
