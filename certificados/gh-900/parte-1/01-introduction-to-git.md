# Introduction to Git

**Tags:** #git #version-control #vcs #distributed #gh-900 #certificação #comandos

---

## 📚 Conceitos Fundamentais e Pesquisa

### O que é Version Control System (VCS)?

Um **Sistema de Controle de Versão** é uma ferramenta que rastreia e gerencia mudanças em arquivos ao longo do tempo. Ele permite:

- **Histórico Completo:** Ver todas as alterações feitas
- **Colaboração:** Múltiplas pessoas trabalham simultaneamente
- **Reversão:** Voltar a versões anteriores se necessário
- **Comparações:** Ver diferenças entre versões
- **Conflitos:** Resolver mudanças conflitantes

### Tipos de VCS

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Local** | Rastreja mudanças em um único computador | RCS (Revision Control System) |
| **Centralizado** | Servidor central armazena histórico; clientes baixam cópias | SVN, CVS, Perforce |
| **Distribuído (DVCS)** | Cada cliente tem cópia completa do histórico | **Git**, Mercurial, Bazaar |

### O que é Git?

Git é um **Sistema de Controle de Versão Distribuído** criado por **Linus Torvalds** em **2005** para gerenciar o desenvolvimento do **kernel Linux**.

**Características principais:**
- **Distribuído:** Cada desenvolvedor tem cópia completa do projeto
- **Performance:** Extremamente rápido mesmo com projetos grandes
- **Snapshots:** Salva estado completo dos arquivos (não apenas diferenças)
- **Branching:** Criação de branches é rápida e barata
- **Integridade:** Verificação de integridade criptográfica em cada operação

### Como o Git Funciona Internamente

Git funciona diferente da maioria dos sistemas de controle de versão. Entenda os conceitos fundamentais:

#### 1. Estrutura de Dados

Git armazena dados de forma diferente da maioria dos sistemas de controle de versão:

**Sistemas tradicionais (SVN, CVS):**
- Armazenam **diferenças** entre versões
- Lista de mudanças: delta v1 → v2 → v3 → v4

**Git:**
- Armazena **snapshots** completos do sistema de arquivos
- Cada commit é um snapshot inteiro do projeto
- Git é como um **mini sistema de arquivos**

#### 2. Os 3 Estados Principais

Git tem 3 estados principais onde seus arquivos podem residir:

```
┌─────────────────────────────────────────────────────────┐
│                    WORKING DIRECTORY                    │
│  (Onde você faz alterações nos arquivos atuais)        │
└────────────────────┬────────────────────────────────┘
                     │ git add
                     ▼
┌─────────────────────────────────────────────────────────┐
│                   STAGING AREA (INDEX)                  │
│         (Prepara arquivos para o próximo commit)          │
└────────────────────┬────────────────────────────────┘
                     │ git commit
                     ▼
┌─────────────────────────────────────────────────────────┐
│                    REPOSITORY (.git)                    │
│      (Snapshot permanente de todos os commits)             │
└─────────────────────────────────────────────────────────┘
```

**Detalhes:**

1. **Working Directory**
   - É onde você edita arquivos
   - Arquivos podem ser: untracked, modified ou staged
   - Não afeta o histórico até serem commitados

2. **Staging Area (Index)**
   - Área intermediária entre working directory e repositório
   - Você seleciona quais alterações irão no próximo commit
   - Permite commits granulares e bem definidos
   - Também chamada de **cache**, **index** ou **staged files**

3. **Repository (.git)**
   - Diretório `.git` contém tudo: metadados, objetos, referências
   - **Objects:** Blobs (arquivos), Trees (diretório), Commits (snapshot)
   - **Refs:** Branches, tags, HEAD
   - **HEAD:** Ponteiro para o branch/commit atual

#### 3. Ciclo de Vida de um Arquivo

```
┌──────────┐  git add  ┌───────────┐  git commit  ┌──────────┐
│ UNTRACKED │──────────▶│  STAGED   │─────────────▶│ COMMITED │
└──────────┘           └───────────┘              └──────────┘
                          │                              │
                          │ git reset                    │ modificado
                          ▼                              ▼
                     ┌──────────┐                   ┌──────────┐
                     │ MODIFIED │                   │ MODIFIED │
                     └──────────┘                   └──────────┘
```

**Estados dos arquivos:**

- **Untracked:** Novo arquivo, ainda não rastreado por Git
- **Tracked:** Arquivo conhecido pelo Git
  - **Unmodified:** Não houveram mudanças desde último commit
  - **Modified:** Houve mudanças no working directory
  - **Staged:** Mudanças preparadas para commit

#### 4. Como o Git Rastreia Mudanças

Git usa um sistema de **hashes criptográficos** para rastrear tudo:

1. **SHA-1 (Secure Hash Algorithm):**
   - Cada objeto tem um hash único de 40 caractares hexadecimais
   - Exemplo: `a94a8fe5ccb19ba61c4c0873d69189847f9796ba`
   - Hash baseado no conteúdo, não no nome do arquivo

2. **Tipos de Objetos Git:**

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Blob** | Contúdo de um arquivo | `blob: arquivo.txt` |
| **Tree** | Diretório com blobs e trees | `tree: src/` |
| **Commit** | Ponteiro para tree + metadados | `commit: mensagem` |
| **Tag** | Referência permanente a um commit | `tag: v1.0.0` |

3. **Estrutura de um Commit:**

```
commit <hash-sha1>
tree <hash-da-tree>
parent <hash-do-commit-pai>
author <nome> <email> <timestamp>
committer <nome> <email> <timestamp>

mensagem do commit
```

#### 5. Branching no Git

Branches no Git são **extremamente leves**:

- **Custo:** Criar um branch é criar um arquivo de 41 bytes
- **Velocidade:** Trocar branches é quase instantâneo
- **Mesclagem:** Merge é apenas 3 commits que apontam para o mesmo objeto tree

**Como funciona:**

```
     master (HEAD)
        │
        ▼
    ┌─────┐
    │ C1  │ ← Commit inicial
    └─────┘
```

```
     master
        │
        ▼
    ┌─────┐
    │ C1  │
    └──┬──┘
       │
       ▼
    ┌─────┐
    │ C2  │ ← Novo branch "feature"
    └─────┘
```

**HEAD aponta sempre para o branch ou commit atual:**

```
HEAD → master → C3
      feature → C2
```

---

## 📋 O que é Cobrado no Exame GH-900

### Tópicos Principais

1. **Configuração (git config)**
   - Definir identidade do usuário (nome e email) - **MUITO IMPORTANTE**
   - Configurar branch padrão (`init.defaultBranch`)
   - Níveis de configuração (local, global, system)

2. **Criação de Repositórios**
   - `git init` - Inicializar novo repositório local
   - `git clone` - Clonar repositórios existentes (HTTPS, SSH)
   - Estrutura do diretório `.git`

3. **Fluxo Básico de Trabalho**
   - `git status` - Verificar estado dos arquivos
   - `git add` - Adicionar arquivos ao staging area
   - `git commit` - Salvar alterações no histórico
   - Diferença entre working directory, staging area e repository

4. **Gerenciamento de Arquivos Ignorados (.gitignore)**
   - Criar arquivo `.gitignore`
   - Padrões de exclusão (glob patterns)
   - Tipos comuns de arquivos para ignorar

5. **Comandos de Visualização**
   - `git log` - Ver histórico de commits
   - `git diff` - Ver diferenças entre versões
   - `git show` - Ver detalhes de um commit específico

---

## 💻 Cenários Práticos (Mão na Massa)

### Exercício 1: Configurar Git e Criar Repositório

```bash
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# PARTE 1: CONFIGURAÇÃO INICIAL
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 1. Configure sua identidade (NECESSÁRIO antes de qualquer commit)
git config --global user.name "Seu Nome Completo"
git config --global user.email "seu.email@exemplo.com"

# 2. Verifique a configuração
git config --list | grep user
git config user.name
git config user.email

# 3. Configure o branch padrão como "main"
git config --global init.defaultBranch main

# 4. Configure o editor padrão para mensagens de commit
git config --global core.editor "code --wait"  # Para VS Code

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# PARTE 2: CRIAR REPOSITÓRIO LOCAL
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 5. Crie diretório para o projeto
mkdir meu-projeto-git
cd meu-projeto-git

# 6. Inicialize o repositório Git
git init
# Output: Initialized empty Git repository in /path/to/meu-projeto-git/.git/

# 7. Verifique a estrutura do diretório .git
ls -la .git/
# Você verá: HEAD, config, objects/, refs/, hooks/, info/

# 8. Verifique o estado inicial
git status
# Output: On branch main
#         nothing to commit, create/copy files and use "git add"

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# PARTE 3: PRIMEIRO COMMIT
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 9. Crie um arquivo README.md
cat > README.md << 'EOF'
# Meu Primeiro Projeto Git

Este é um projeto de exemplo para aprender Git.

## Sobre
- Aprendendo sistema de controle de versão
- Praticando comandos básicos

## Objetivos
- [ ] Compreender estrutura do Git
- [ ] Dominar fluxo de trabalho básico
- [ ] Aprender sobre branches
EOF

# 10. Verifique o estado (deve mostrar "untracked")
git status

# 11. Adicione o arquivo ao staging area
git add README.md

# 12. Verifique novamente (o arquivo deve estar "staged")
git status

# 13. Faça o primeiro commit
git commit -m "Initial commit: Add README with project description"

# 14. Verifique o histórico de commits
git log
git log --oneline
git log --graph --oneline --all

# 15. Verifique o conteúdo do último commit
git show HEAD
git show HEAD:README.md
```

### Exercício 2: Trabalhando com Múltiplos Arquivos

```bash
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# TRABALHANDO COM ARQUIVOS: ADICIONAR, MODIFICAR, REMOVER
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 1. Crie arquivos de projeto
mkdir src tests

cat > src/app.js << 'EOF'
console.log('Aplicação iniciada!');

function greet(name) {
    return `Olá, ${name}!`;
}

module.exports = { greet };
EOF

cat > tests/app.test.js << 'EOF'
const { greet } = require('../src/app');

console.log('Teste greet:', greet('Mundo'));
EOF

# 2. Crie arquivo .gitignore
cat > .gitignore << 'EOF'
# Dependências
node_modules/
vendor/
__pycache__/

# Logs
*.log
logs/
npm-debug.log*

# Ambiente
.env
.env.local
.env.*.local

# Build
dist/
build/
*.min.js

# IDE
.vscode/
.idea/
*.swp
*.swo

# SO
.DS_Store
Thumbs.db
EOF

# 3. Verifique o estado (deve mostrar arquivos "untracked")
git status

# 4. Adicione arquivos específicos
git add src/app.js

# 5. Adicione todo o restante exceto node_modules (que ainda não existe)
git add .

# 6. Verifique (todos devem estar "staged")
git status

# 7. Faça o commit
git commit -m "Add application code and test files"

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CENÁRIO: MODIFICAR ARQUIVOS
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 8. Modifique src/app.js
cat >> src/app.js << 'EOF'

function calculateSum(a, b) {
    return a + b;
}

module.exports = { greet, calculateSum };
EOF

# 9. Verifique o estado (app.js deve estar "modified")
git status

# 10. Veja as diferenças (working directory vs staging)
git diff

# 11. Adicione a modificação ao staging
git add src/app.js

# 12. Faça mais uma modificação no mesmo arquivo
cat >> src/app.js << 'EOF'

function calculateProduct(a, b) {
    return a * b;
}

module.exports = { greet, calculateSum, calculateProduct };
EOF

# 13. Verifique novamente (agora há alterações "modified" não staged)
git status

# 14. Veja diferenças em staging
git diff --staged

# 15. Veja diferenças não staged
git diff

# 16. Descarte as alterações não staged
git restore src/app.js

# 17. Faça o commit das alterações staged
git commit -m "Add calculateSum function"
```

### Exercício 3: Clonando Repositório

```bash
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CLONANDO REPOSITÓRIOS EXISTENTES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 1. Clone via HTTPS
git clone https://github.com/microsoft/vscode.git vscode-https
# Isso baixa todo o histórico do projeto

# 2. Clone via SSH (requer chave SSH configurada)
# git clone git@github.com:microsoft/vscode.git vscode-ssh

# 3. Clone para diretório específico com nome customizado
git clone https://github.com/microsoft/vscode.git meu-editor-favorito

# 4. Entre no repositório clonado
cd vscode-https

# 5. Verifique o remote configurado
git remote -v
# Output:
# origin	https://github.com/microsoft/vscode.git (fetch)
# origin	https://github.com/microsoft/vscode.git (push)

# 6. Verifique branches locais
git branch

# 7. Verifique todos os branches (locais e remotos)
git branch -a

# 8. Verifique o histórico de commits
git log --oneline -10

# 9. Verifique o último commit
git show HEAD --stat

# 10. Clone específico de branch
git clone --branch stable https://github.com/nodejs/node.git node-stable

# 11. Clone raso (apenas commits recentes)
git clone --depth 1 https://github.com/microsoft/vscode.git vscode-shallow
```

### Exercício 4: Visualização e Comparação

```bash
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# COMPARANDO VERSÕES E HISTÓRICO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 1. Crie arquivo inicial
cat > changelog.md << 'EOF'
# Changelog

## v1.0.0 (2026-01-27)
- Lançamento inicial
EOF

# 2. Faça commit
git add changelog.md
git commit -m "Add initial changelog v1.0.0"

# 3. Modifique o arquivo
cat >> changelog.md << 'EOF'

## v1.1.0 (2026-01-28)
- Correção de bugs
- Melhoria de performance
EOF

# 4. Veja diferenças (working vs last commit)
git diff

# 5. Veja diferenças em formato colorido
git diff --color-words

# 6. Veja diferenças de um arquivo específico
git diff changelog.md

# 7. Veja quantas linhas mudaram
git diff --stat

# 8. Veja histórico de commits
git log --oneline --all --graph
git log --pretty=format:"%h - %an, %ar : %s" --graph

# 9. Veja commits de um autor específico
git log --author="Seu Nome"

# 10. Pesquise commits por mensagem
git log --grep="Add"

# 11. Veja quem modificou cada linha de um arquivo
git blame changelog.md
```

### Exercício 5: .gitignore Avançado

```bash
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# PADRÕES AVANÇADOS DE .GITIGNORE
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# Crie um .gitignore profissional
cat > .gitignore << 'EOF'
# =====================
# DEPENDÊNCIAS
# =====================
node_modules/
jspm_packages/
bower_components/

# =====================
# BUILD & DIST
# =====================
dist/
build/
out/
.next/
.nuxt/
.cache/

# =====================
# LOGS
# =====================
logs/
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# =====================
# ARQUIVOS TEMPORÁRIOS
# =====================
*.tmp
*.temp
*.swp
*.swo
*~
.DS_Store
Thumbs.db

# =====================
# VARIÁVEIS DE AMBIENTE
# =====================
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# =====================
# IDE & EDITOR
# =====================
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# =====================
# ARQUIVOS TESTE
# =====================
coverage/
*.lcov
.nyc_output/

# =====================
# EXCEÇÕES (NÃO IGNORAR)
# =====================
!.gitkeep
!README.md
!LICENSE
EOF

# Verifique quais arquivos seriam ignorados
git check-ignore -v node_modules/
git check-ignore -v *.log

# Teste padrões específicos
echo "teste.log" > teste.log
git status  # teste.log não deve aparecer

echo "node_modules/teste.txt" > node_modules/teste.txt
git status  # Não deve aparecer

# Forçar adicionar arquivo ignorado (se necessário)
git add -f teste.log
git status  # Agora teste.log aparece

# Remover do staging
git reset teste.log
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

## 🔥 Dicas de Ouro para o Exame

1. **Memorize o fluxo padrão:**
   ```bash
   git init              # Inicializar
   git add .             # Preparar
   git commit -m "msg"    # Commitar
   ```

2. **Conheça as diferenças entre comandos:**
   - `git diff` vs `git diff --staged` (working vs staging)
   - `git add .` vs `git add --all` (recursivo vs tudo)
   - `git config` (global vs local vs system)

3. **Entenda o ciclo de vida dos arquivos:**
   ```
   Untracked → Staged → Committed → Modified
        ↑___________|
   ```

4. **Saiba quando usar cada comando:**
   - `git status` - Verificar estado
   - `git log` - Ver histórico
   - `git diff` - Ver alterações
   - `git show` - Ver detalhes de um commit

5. **Pratique com repositórios reais:**
   - Clone repositórios do GitHub
   - Crie branches, faça commits
   - Trabalhe com .gitignore

## 📚 Recursos de Estudo

### Documentação Oficial
- [Git Documentation](https://git-scm.com/doc) - Documentação completa do Git
- [Pro Git Book](https://git-scm.com/book/en/v2) - Livro gratuito sobre Git
- [Git Reference Manual](https://git-scm.com/docs) - Referência de comandos

### Cursos Interativos
- [Learn Git Branching](https://learngitbranching.js.org/) - Tutorial visual e interativo
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) - Resumo em PDF

### Microsoft Learn
- [Introduction to Git](https://learn.microsoft.com/en-us/training/modules/intro-to-git/) - Curso oficial Microsoft

### Vídeos
- [Git & GitHub Crash Course](https://www.youtube.com/watch?v=RGOj5yH7evk) - FreeCodeCamp (1h+)

### Links Úteis
- [Git Ignore Templates](https://github.com/github/gitignore) - Templates de .gitignore para diversas linguagens
- [Visualizing Git Concepts](https://marklodato.github.io/visual-git-guide/) - Guia visual do Git

---

**Resumo Final:** Git é um sistema de controle de versão distribuído poderoso que usa snapshots, hashes e branches para rastrear alterações. Para o exame GH-900, domine os comandos básicos (`init`, `add`, `commit`, `status`, `diff`, `log`) e entenda os três estados: Working Directory, Staging Area e Repository. 🚀
