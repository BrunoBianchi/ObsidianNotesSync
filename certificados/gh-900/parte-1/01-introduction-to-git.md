# Introduction to Git

## 📚 Pesquisa e Síntese

### O que é Git?
Git é um sistema de controle de versão distribuído (Distributed Version Control System - DVCS) criado por Linus Torvalds em 2005 para gerenciar o desenvolvimento do kernel Linux. Ele permite rastrear alterações em arquivos, coordenar trabalho entre desenvolvedores e manter o histórico completo de um projeto.

### O que é cobrado no exame GH-900 sobre Git?

O exame GH-900 foca nos comandos básicos e fluxos fundamentais de trabalho com Git. Os principais tópicos são:

1. **Configuração (git config)**
   - Definir identidade do usuário (nome e email)
   - Configurar branch padrão
   - Níveis de configuração (local, global, system)

2. **Criação de Repositórios (git init, git clone)**
   - Inicializar novo repositório local
   - Clonar repositórios existentes
   - Estrutura do diretório .git

3. **Fluxo Básico de Trabalho**
   - `git status` - Verificar estado dos arquivos
   - `git add` - Adicionar arquivos ao staging area
   - `git commit` - Salvar alterações no histórico
   - Diferença entre working directory, staging area e repository

4. **Gerenciamento de Arquivos Ignorados (.gitignore)**
   - Criar arquivo .gitignore
   - Padrões de exclusão
   - Tipos comuns de arquivos para ignorar

5. **Comandos de Visualização**
   - `git log` - Ver histórico de commits
   - `git diff` - Ver diferenças entre versões

### Conceitos Fundamentais

| Termo | Descrição |
|--------|-----------|
| **Working Directory** | O diretório onde você faz suas alterações nos arquivos |
| **Staging Area (Index)** | Área onde os arquivos são preparados antes do commit |
| **Repository (.git)** | O banco de dados onde Git armazena todos os metadados e histórico |
| **Commit** | Um snapshot do estado do projeto em um determinado momento |
| **Branch** | Uma linha independente de desenvolvimento |
| **HEAD** | Um ponteiro para o branch/commit atual |

---

## 💻 Cenário Prático (Mão na Massa)

### Exercício 1: Configurar Git e Criar um Repositório Local

```bash
# 1. Configure sua identidade (necessário antes de qualquer commit)
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"

# 2. Verifique a configuração
git config --list
git config user.name
git config user.email

# 3. Crie um novo diretório para o projeto
mkdir meu-projeto-git
cd meu-projeto-git

# 4. Inicialize o repositório Git
git init
# Output: Initialized empty Git repository in /path/to/meu-projeto-git/.git/

# 5. Crie um arquivo README.md
echo "# Meu Primeiro Projeto Git" > README.md

# 6. Verifique o estado dos arquivos
git status
# Output: Untracked files: README.md

# 7. Adicione o arquivo ao staging area
git add README.md

# 8. Verifique novamente (o arquivo deve estar em verde/staged)
git status

# 9. Faça o primeiro commit
git commit -m "Initial commit: Add README.md"

# 10. Verifique o histórico de commits
git log
git log --oneline
```

### Exercício 2: Trabalhando com Múltiplos Arquivos

```bash
# 1. Crie mais arquivos
echo "console.log('Hello, Git!');" > app.js
echo "node_modules/" > .gitignore
echo "*.log" >> .gitignore

# 2. Verifique o status (deve mostrar os novos arquivos)
git status

# 3. Adicione todos os arquivos ao staging area
git add .

# 4. Crie um arquivo temporário que NÃO deve ser commitado
echo "segredo" > temp.txt

# 5. Verifique o status (temp.txt deve estar untracked)
git status

# 6. Faça o commit dos arquivos staged
git commit -m "Add app.js and .gitignore"

# 7. Adicione o .gitignore novamente (para incluir a nova regra)
git add .gitignore
git commit -m "Update .gitignore with temp.txt rule"

# 8. Tente adicionar o arquivo temp.txt (não funcionará devido ao .gitignore)
git add temp.txt
# Git deve informar que o arquivo está sendo ignorado

# 9. Forçar adição de arquivo ignorado (caso seja realmente necessário)
git add -f temp.txt

# 10. Remova o arquivo do staging area
git reset temp.txt
```

### Exercício 3: Clonando um Repositório Existente

```bash
# 1. Clone um repositório de exemplo
git clone https://github.com/microsoft/vscode.git vscode-exemplo
# Isso cria um diretório vscode-exemplo e copia todo o código

# 2. Entre no repositório clonado
cd vscode-exemplo

# 3. Verifique o remote (origin)
git remote -v

# 4. Verifique o branch atual
git branch
git branch -a  # Mostra todos os branches (locais e remotos)

# 5. Verifique o histórico de commits
git log --oneline -10

# 6. Clone para um diretório específico com um nome diferente
git clone https://github.com/microsoft/vscode.git meu-editor
```

### Exercício 4: Visualizando Alterações

```bash
# 1. Crie um arquivo e faça commit
echo "versao 1" > arquivo.txt
git add arquivo.txt
git commit -m "Add arquivo.txt v1"

# 2. Faça alterações no arquivo
echo "versao 2" >> arquivo.txt

# 3. Veja as diferenças (working directory vs staging area)
git diff

# 4. Adicione ao staging area
git add arquivo.txt

# 5. Faça mais alterações
echo "versao 3" >> arquivo.txt

# 6. Veja as diferenças em staging
git diff --staged

# 7. Veja as diferenças não staged
git diff

# 8. Descarte as alterações não staged
git restore arquivo.txt

# 9. Verifique o status
git status

# 10. Verifique o conteúdo de um commit específico
git show HEAD
```

### Exercício 5: Padrões Avançados de .gitignore

```bash
# Crie um .gitignore completo
cat > .gitignore << 'EOF'
# Ignorar dependências
node_modules/
vendor/
__pycache__/

# Ignorar arquivos de log
*.log
logs/

# Ignorar arquivos de sistema
.DS_Store
Thumbs.db

# Ignorar arquivos de build
dist/
build/
*.min.js

# Ignorar arquivos de configuração local
.env
.env.local
config.local.js

# Ignorar arquivos temporários
*.tmp
*.temp
*.swp
*~

# Mas NÃO ignorar arquivo específico
!keep-this.log
EOF

# Adicione o .gitignore
git add .gitignore
git commit -m "Add comprehensive .gitignore"
```

---

## 📝 Simulado de Exame (Com Solução)

### Questão 1
Qual comando Git é usado para configurar o email do usuário globalmente?

A) `git config --email "email@exemplo.com"`
B) `git config --global user.email "email@exemplo.com"`
C) `git config user.email "email@exemplo.com"`
D) `git config set email "email@exemplo.com"`

<details>
<summary>✅ Resposta Correta</summary>

**B) `git config --global user.email "email@exemplo.com"`**

**Explicação:**
- A opção `--global` define a configuração para todos os repositórios do usuário
- A chave correta é `user.email`, não apenas `email`
- O comando correto é `git config --global <chave> <valor>`, não `git config set`

**Por que as outras estão incorretas:**
- A) Falta a palavra-chave `user` antes de `email` e não usa o flag `--global`
- C) Falta o flag `--global`, então a configuração seria apenas local (repositório atual)
- D) Não existe o comando `git config set`, a sintaxe correta é `git config --global <chave> <valor>`
</details>

---

### Questão 2
Após executar `git init`, o que acontece com os arquivos existentes no diretório?

A) Eles são automaticamente adicionados ao repositório Git
B) Eles são adicionados ao staging area (index)
C) Eles permanecem no working directory e precisam ser explicitamente adicionados
D) Eles são removidos e substituídos pelo diretório .git

<details>
<summary>✅ Resposta Correta</summary>

**C) Eles permanecem no working directory e precisam ser explicitamente adicionados**

**Explicação:**
- `git init` apenas cria a estrutura do repositório (.git)
- Arquivos existentes continuam no working directory como "untracked"
- É necessário usar `git add` para movê-los ao staging area
- Em seguida, usar `git commit` para salvá-los no histórico

**Por que as outras estão incorretas:**
- A) Git nunca adiciona arquivos automaticamente sem comando explícito
- B) Arquivos são adicionados ao staging area apenas com `git add`, não com `git init`
- D) `git init` não remove arquivos existentes, apenas adiciona o diretório .git
</details>

---

### Questão 3
Qual comando mostra a diferença entre o working directory e o último commit?

A) `git diff --staged`
B) `git log --oneline`
C) `git diff`
D) `git status`

<details>
<summary>✅ Resposta Correta</summary>

**C) `git diff`**

**Explicação:**
- `git diff` mostra diferenças entre o working directory e o staging area
- Se o staging area estiver vazio, mostra diferenças em relação ao último commit
- É o comando padrão para ver alterações não commitadas

**Por que as outras estão incorretas:**
- A) `git diff --staged` mostra diferenças entre o staging area e o último commit (alterações preparadas)
- B) `git log --oneline` mostra o histórico de commits, não diferenças
- D) `git status` mostra apenas quais arquivos foram modificados, não as diferenças reais
</details>

---

### Questão 4
Qual destas linhas em .gitignore está corretamente formatada?

A) `*.js` (exclui todos os arquivos JavaScript)
B) `node_modules` (exclui o diretório node_modules)
C) `*.log` (exclui todos os arquivos terminados em .log)
D) Todas as alternativas estão corretas

<details>
<summary>✅ Resposta Correta</summary>

**D) Todas as alternativas estão corretas**

**Explicação:**
- `*.js` é um padrão glob que exclui todos os arquivos .js em qualquer diretório
- `node_modules` exclui o diretório node_modules (e todo o seu conteúdo)
- `*.log` exclui todos os arquivos terminados em .log
- Todas são formas válidas e corretas de especificar padrões no .gitignore

**Detalhes adicionais:**
- Padrões com `*` são wildcards que correspondem a qualquer caractere
- Padrões sem `/` no início podem corresponder em qualquer diretório
- Para excluir apenas no raiz, usar `/*.js`
- Para excluir recursivamente, usar `**/*.js`
</details>

---

### Questão 5
Qual comando adiciona todos os arquivos modificados e novos ao staging area?

A) `git add all`
B) `git add --all`
C) `git add .`
D) Tanto B quanto C estão corretos

<details>
<summary>✅ Resposta Correta</summary>

**D) Tanto B quanto C estão corretos**

**Explicação:**
- `git add --all` ou `git add -A` adiciona todos os arquivos (modificados, novos e deletados)
- `git add .` adiciona todos os arquivos no diretório atual e subdiretórios
- Ambos são equivalentes em muitos casos, mas `--all` é mais explícito
- Para o exame GH-900, ambos são considerados corretos

**Diferenças sutis:**
- `git add .` não adiciona arquivos deletados (depende da versão do Git)
- `git add --all` sempre adiciona todos os tipos de alterações
- No exame, ambos são aceitos como resposta correta para "adicionar todos os arquivos"
</details>

---

## 🔥 Dicas para o Exame

1. **Memorize o fluxo padrão:**
   ```bash
   git init
   git add .
   git commit -m "mensagem"
   ```

2. **Conheça as diferenças entre comandos:**
   - `git diff` vs `git diff --staged`
   - `git add .` vs `git add --all`
   - `git config` (global vs local vs system)

3. **Entenda o ciclo de vida dos arquivos:**
   - Untracked → Staged → Committed → Modified

4. **Saiba quando usar cada comando:**
   - `git status` - Verificar estado
   - `git log` - Ver histórico
   - `git diff` - Ver alterações
   - `git show` - Ver detalhes de um commit

5. **Pratique com repositórios reais:**
   - Clone repositórios do GitHub
   - Crie branches, faça commits
   - Trabalhe com .gitignore

## 📚 Recursos Adicionais

- [Documentação Oficial do Git](https://git-scm.com/doc)
- [Git Cheat Sheet Oficial](https://education.github.com/git-cheat-sheet-education.pdf)
- [Learn Git Branching](https://learngitbranching.js.org/) - Tutorial interativo
- [Microsoft Learn: Introduction to Git](https://learn.microsoft.com/en-us/training/modules/intro-to-git/)

---

Pratique bastante estes exercícios e você estará bem preparado para o tópico "Introduction to Git" do GH-900! 🚀
