# Introduction to GitHub

**Tags:** #github #colaboração #pull-request #issue #gh-900 #certificação #workflow

---

## 📚 Conceitos Fundamentais e Pesquisa

### O que é GitHub?

**GitHub** é a maior plataforma de hospedagem de código e colaboração de desenvolvimento do mundo. Fundado em **2008** por Chris Wanstrath, PJ Hyett e Tom Preston-Werner, foi adquirido pela **Microsoft** em **2018** por **$7.5 bilhões**.

**Características principais:**
- **Hospedagem de repositórios Git** - Mais de 100 milhões de repositórios
- **Colaboração em tempo real** - Múltiplos desenvolvedores trabalham simultaneamente
- **Code review** - Pull requests com discussões e aprovações
- **Issues e Project Management** - Rastreamento de bugs, feature requests e tarefas
- **CI/CD com GitHub Actions** - Automação de build, test e deploy
- **Segurança avançada** - Dependabot, code scanning, secret scanning

### GitHub vs Git

| Aspecto | Git | GitHub |
|---------|-----|--------|
| **O que é** | Sistema de controle de versão (software) | Plataforma de hospedagem (serviço web) |
| **Onde roda** | Localmente no seu computador | Em nuvem (github.com) |
| **Função** | Rastreia e gerencia mudanças | Permite colaboração e hospedagem |
| **Relação** | GitHub usa Git por baixo | GitHub é uma interface para Git |

### Fluxo de Trabalho no GitHub (GitHub Flow)

O **GitHub Flow** é um fluxo simplificado para desenvolvimento colaborativo:

```
┌─────────────────────────────────────────────────────────────┐
│                  main (PRODUCTION)                   │
│                 ✓ Código estável                          │
└──────────────────────┬──────────────────────────────────┘
                       │ git checkout -b feature
                       ▼
┌─────────────────────────────────────────────────────────────┐
│               feature-branch (DEVELOPMENT)              │
│              ✗ Código em desenvolvimento                    │
│              - Você trabalha aqui                          │
│              - Faz commits                                 │
│              - Testa mudanças                              │
└──────────────────────┬──────────────────────────────────┘
                       │ git push
                       ▼
┌─────────────────────────────────────────────────────────────┐
│              GitHub (REMOTE REPOSITORY)                 │
│              - Pull Request aberto                        │
│              - Code review em andamento                    │
│              - Discussão da equipe                        │
└──────────────────────┬──────────────────────────────────┘
                       │ merge após review aprovado
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                  main (PRODUCTION)                   │
│                 ✓ Novas mudanças integradas               │
│              - feature-branch deletado                     │
└─────────────────────────────────────────────────────────────┘
```

### Estrutura de um Repositório no GitHub

```
meu-repositorio/
├── .github/                    # Configurações específicas do GitHub
│   ├── ISSUE_TEMPLATE/          # Templates para issues
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   ├── PULL_REQUEST_TEMPLATE.md # Template para PRs
│   ├── workflows/              # GitHub Actions (CI/CD)
│   │   ├── ci.yml
│   │   └── deploy.yml
│   └── dependabot.yml         # Automação de dependências
├── docs/                      # Documentação
├── src/                       # Código fonte
├── tests/                     # Testes
├── README.md                  # Documentação principal do projeto
├── LICENSE                    # Licença do projeto
├── .gitignore                 # Arquivos a ignorar
└── .git/                      # Diretório Git (não no GitHub)
```

### Repositório vs Organization

| Repositório Pessoal | Organization |
|---------------------|-------------|
| **Proprietário:** Um usuário | **Proprietário:** Múltiplos membros |
| **Permissões:** Simples (leitura/escrita) | **Permissões:** Granulares (admin, maintain, member, guest) |
| **Uso:** Projetos pessoais, portfolio | **Uso:** Empresas, projetos open-source grandes |
| **Limites:** Limitado por plano pessoal | **Limites:** Limitado por plano enterprise |

---

## 📋 O que é Cobrado no Exame GH-900

### Tópicos Principais

1. **Repositórios (Repositories)**
   - Criar repositórios (públicos e privados)
   - Clonar repositórios existentes (HTTPS, SSH)
   - Estrutura de arquivos (README, LICENSE, .gitignore)
   - Branches (ramificações) na interface web
   - Repository settings (visibilidade, features, proteção)

2. **Issues**
   - Criar issues para rastrear bugs e feature requests
   - Adicionar labels, assignees, milestones, projects
   - Usar templates de issues
   - Fechar e referenciar issues em commits/PRs
   - Issue comments e discussions

3. **Pull Requests (PRs)**
   - Criar PRs para propor mudanças
   - Revisar código (code review)
   - Merge strategies (merge commit, squash, rebase)
   - Resolver conflicts de merge
   - PR comments, reviews, e approvals

4. **Fluxo Básico da Interface**
   - Navegar pela interface do GitHub (tabs, menus)
   - Editar arquivos na web
   - Visualizar histórico e diffs
   - Usar keyboard shortcuts
   - Gerenciar colaboradores (collaborators)

5. **Conceitos de Colaboração**
   - Forking (copiar repositório para sua conta)
   - GitHub Flow (Branch → Commit → PR → Review → Merge)
   - Discussions e Comments em Issues/PRs
   - Notifications e subscrições
   - Wiki para documentação

---

## 💻 Cenários Práticos (Mão na Massa)

### Exercício 1: Criar Repositório no GitHub

**Via Interface Web:**

1. **Acesse** https://github.com
2. **Clique** no sinal de **+** (canto superior direito) → **New repository**
3. **Preencha:**
   ```
   Repository name:     hello-github
   Description:         Aprendendo GitHub Flow e colaboração
   Visibility:           [x] Public  |  ( ) Private
   Add a README file:  [x] Checked
   Add .gitignore:      [None] ▼ (ou selecione sua linguagem)
   Choose a license:    [MIT License] ▼ (opcional)
   ```
4. **Clique** em **Create repository**

**Via GitHub CLI (gh):**

```bash
# Instale o GitHub CLI primeiro
# Ubuntu/Debian:
sudo apt install gh

# macOS:
brew install gh

# Autentique
gh auth login

# Crie repositório
gh repo create hello-github --public --source=. --remote=origin --description="Aprendendo GitHub Flow" --clone=false
```

### Exercício 2: Criar Branch e Editar Arquivos

**Criar Branch:**

1. **Navegue** até seu repositório `hello-github`
2. **Verifique** o branch atual (deve estar em `main`)
3. **Abra** o dropdown do branch (abaixo do nome do repositório)
4. **Digite** `feature/update-readme` no campo de texto
5. **Clique** em **Create branch: feature/update-readme from main**

**Editar README.md:**

1. **Clique** no arquivo `README.md`
2. **Clique** no ícone de lápis (✏️ Edit file) no canto superior direito
3. **Substitua** o conteúdo:

```markdown
# Hello GitHub

Bem-vindo ao meu repositório de exemplo! Este projeto foi criado para praticar o **GitHub Flow**.

## 🎯 Objetivos

Aprender e dominar os conceitos fundamentais do GitHub:

- [x] Criar repositório
- [ ] Criar e gerenciar branches
- [ ] Fazer commits na interface web
- [ ] Abrir Pull Request
- [ ] Revisar e mergear PR
- [ ] Trabalhar com Issues

## 📚 Recursos Aprendidos

### Git
- Comandos básicos: `init`, `add`, `commit`, `push`, `pull`
- Branches: `branch`, `checkout`, `merge`
- Histórico: `log`, `diff`, `show`

### GitHub
- Repositórios e branches
- Issues e Pull Requests
- Markdown para documentação
- GitHub Actions (básico)

## 🔗 Links Úteis

- [Documentação do GitHub](https://docs.github.com)
- [GitHub Skills](https://skills.github.com/)
- [Git Handbook](https://guides.github.com/introduction/git-handbook/)

---

_Licenciado sob MIT License_
```

4. **No campo "Commit changes":**
   - **Commit message:** `Update README with learning goals and resources`
   - **Extended description:** `Added checklist of learning objectives, resources section, and useful links.`
   - **Commit directly to:** `feature/update-readme` ← MUITO IMPORTANTE!
5. **Clique** em **Commit changes**

### Exercício 3: Abrir Pull Request

1. **Clique** na aba **Pull requests** no topo do repositório
2. **Clique** em **New pull request**
3. **Verifique as informações:**
   - **base repository:** `seu-usuario/hello-github`
   - **base:** `main` ← onde as mudanças serão aplicadas
   - **compare repository:** `seu-usuario/hello-github`
   - **compare:** `feature/update-readme` ← seu branch com as mudanças
4. **Clique** em **Compare & pull request** (ou similar)
5. **Verifique o diff** (diferenças entre os branches) na aba **Files changed**
6. **Se estiver tudo certo, clique** em **Create pull request**
7. **Preencha:**
   
   ```markdown
   ## 📋 Título
   
   Update README with comprehensive learning resources
   
   ## 📝 Descrição
   
   ### O que foi alterado
   - Atualizado o README com objetivos de aprendizado
   - Adicionado checklist progresso
   - Criado seção de recursos (Git + GitHub)
   - Adicionado links úteis para documentação
   
   ### Por que fazer estas mudanças?
   O README serve como ponto de partida para quem está aprendendo GitHub. Documentar claramente os objetivos e recursos ajuda a manter o foco.
   
   ### Mudanças
   - 📝 150 linhas adicionadas ao README
   - ✅ Checklists de progresso
   - 🔗 Links para documentação oficial
   
   ### Screenshots
   *(Se houver, adicione capturas de tela)*
   
   ### Checklist
   - [x] Código segue padrões do projeto
   - [x] Testes executados e passando
   - [x] Documentação atualizada
   - [x] Mensagens de commit claras
   
   ### Issue Relacionada
   Closes #1 (se houver issue)
   
   ---
   
   _Mergear depois da revisão_
   ```

8. **Clique** em **Create pull request**

### Exercício 4: Revisar e Mergear Pull Request

**Code Review (Simulado):**

1. **No seu PR**, clique na aba **Files changed**
2. **Visualize** as alterações (adicões em verde, remoções em vermelho)
3. **Clique** em qualquer linha para adicionar comentário de revisão
4. **Digite:** `Ótima estrutura! Que tal adicionar uma seção sobre como resolver conflitos de merge?`
5. **Clique** em **Start a review** → **Submit review**
6. **Selecione** a opção: **Approve** (requer permissões)
7. **Adicione** um comentário geral: `Aprovação das mudanças do README. Excelente documentação!`
8. **Clique** em **Submit review**

**Merge:**

1. **Volte** para a aba **Conversation** do PR
2. **No final da página**, verifique se há conflitos (aviso em vermelho)
3. **Se não houver conflitos**, clique em **Merge pull request**
4. **Escolha** uma estratégia de merge:
   
   | Estratégia | Quando Usar | O que Faz |
   |-----------|-------------|------------|
   | **Merge commit** | Preservar histórico completo | Cria commit de merge, preserva todos os commits |
   | **Squash and merge** | Histórico limpo | Combina todos em UM único commit |
   | **Rebase and merge** | Histórico linear | Rebase commits, depois mergear |
   
5. **Para este exercício**, selecione **Merge commit**
6. **Clique** em **Confirm merge**
7. **Após o merge**, você verá uma mensagem verde: `Pull request successfully merged and closed`
8. **Clique** em **Delete branch** para limpar o branch `feature/update-readme`
9. **Clique** em **View pull request** para ver os detalhes

### Exercício 5: Trabalhar com Issues

**Criar Issue:**

1. **Clique** na aba **Issues** no topo do repositório
2. **Se for a primeira issue**, clique em **Get started** para configurar templates
3. **Clique** em **New issue**
4. **Preencha:**
   
   ```
   Title: Adicionar seção de conflitos de merge ao README
   
   Type: [x] Bug report | ( ) Feature request | ( ) Documentation
   
   Priority:
   - (x) High
   - ( ) Medium
   - ( ) Low
   
   Labels:
   - [x] documentation
   - [ ] enhancement
   - [ ] good first issue
   
   Assignees: @seu-usuario
   
   Projects: Learning Path
   
   Milestone: Milestone 1
   ```
   
   **Descrição:**
   
   ```markdown
   ## 📋 Issue Title
   Adicionar seção de conflitos de merge ao README
   
   ## 🎯 Objetivo
   Adicionar uma seção ao README explicando como resolver conflitos de merge comuns no GitHub.
   
   ## 📝 Detalhes
   
   ### O que precisa ser feito
   - [ ] Criar nova seção "Resolvendo Conflitos de Merge"
   - [ ] Explicar o que causa conflitos
   - [ ] Fornecer passos para resolver
   - [ ] Adicionar exemplos visuais
   - [ ] Incluir links para documentação oficial
   
   ### Onde deve ser alterado
   Arquivo: `README.md`
   Seção: Após "Recursos Aprendidos"
   
   ### Critérios de Aceitação
   - [ ] Seção criada com título claro
   - [ ] Explicação técnica precisa
   - [ ] Exemplos práticos incluídos
   - [ ] Links funcionando
   - [ ] Markdown formatado corretamente
   
   ### Contexto Adicional
   Conflitos de merge são comuns ao colaborar em equipes. Documentar como resolvê-los ajuda novos contribuidores.
   
   ### Referências
   - [Resolving a merge conflict on GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)
   - [About merge conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)
   
   ---
   
   _Assignee: @seu-usuario_
   ```

5. **Clique** em **Submit new issue**

**Referenciar Issue em Commits e PRs:**

1. **Anote** o número da issue (ex: `#1`)
2. **Crie** um novo branch: `feature/merge-conflicts-section`
3. **Edite** o README.md e adicione:

```markdown
## 🔧 Resolvendo Conflitos de Merge

Conflitos de merge ocorrem quando duas pessoas alteram a mesma linha de código em branches diferentes. O GitHub não pode automaticamente resolver quais mudanças devem prevalecer.

### O que Causa Conflitos?

Conflitos acontecem quando:
- Dois branches modificam a mesma linha de código
- Um branch deleta um arquivo que outro branch modificou
- As mudanças não podem ser automaticamente combinadas

### Como Resolver no GitHub

1. **Identifique** o conflito: PR mostrará aviso "This branch has conflicts that must be resolved"
2. **Abra** o PR para ver quais arquivos estão em conflito
3. **Resolva** manualmente:
   - Clique em **Resolve conflicts**
   - Veja as duas versões lado a lado (your changes vs incoming changes)
   - Edite para combinar ou escolher as mudanças corretas
   - Marque os conflitos como resolvidos
4. **Commit** as mudanças resolvidas
5. **Merge** o PR normalmente

### Dicas para Evitar Conflitos

- Mantenha branches curtos (merge frequentemente)
- Comunique-se com a equipe sobre quem está trabalhando no quê
- Atualize seu branch regularmente: `git pull origin main`
- Use branches de feature bem definidos

### Exemplo Visual

```
Main:     console.log('Hello, World!')        │
Feature:  console.log('Hello, Universe!')       │
           ↑                                        │
          CONFLITO                                  │
```

**Resolução:** Escolha uma das versões ou combine:

```
Main:     console.log('Hello, Universe!')       ✓
```

### Recursos

- [Resolving merge conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)
- [Git: Basic merge conflicts](https://git-scm.com/book/en/v2/Git-Branching-Merge-Conflicts.html)
```

4. **Faça** commit com mensagem:

```markdown
Add merge conflicts resolution section

Closes #1
```

5. **Crie** um PR normalmente

**Fechar Issue Manualmente:**

Se você fechou a issue sem usar uma das palavras-chave, pode fechar manualmente:

1. **Abra** a issue
2. **No menu lateral direito**, clique em **Close issue**
3. **Adicione** um comentário explicando por que está fechando

### Exercício 6: Fork e Contribuição

**Forkar um Repositório:**

1. **Navegue** até um repositório open-source (ex: https://github.com/facebook/react)
2. **Clique** no botão **Fork** (canto superior direito)
3. **Selecione** sua conta como owner do fork
4. **Clique** em **Create fork**
5. **Clone** seu fork: `git clone https://github.com/seu-usuario/react.git`

**Workflow de Contribuição:**

```
┌─────────────────────────────────────────────────────────┐
│  REPOSITÓRIO ORIGINAL (upstream)                 │
│  facebook/react                                    │
└────────────────────┬────────────────────────────────┘
                     │ Fork
                     ▼
┌─────────────────────────────────────────────────────────┐
│  SEU FORK (origin)                              │
│  seu-usuario/react                                │
└────────────────────┬────────────────────────────────┘
                     │ git clone
                     ▼
┌─────────────────────────────────────────────────────────┐
│  SEU COMPUTADOR (local)                          │
│  git checkout -b fix-bug                           │
│  ...faz mudanças...                               │
│  git commit -m "Fix bug..."                        │
│  git push origin fix-bug                            │
└────────────────────┬────────────────────────────────┘
                     │ Abre PR no GitHub
                     ▼
┌─────────────────────────────────────────────────────────┐
│  REPOSITÓRIO ORIGINAL (upstream)                 │
│  PR: seu-usuario/react:fix-bug → main             │
│  Mantenedores do upstream revisam e mergear        │
└─────────────────────────────────────────────────────────┘
```

**Comandos para Contribuição:**

```bash
# 1. Adicionar remote upstream
git remote add upstream https://github.com/facebook/react.git

# 2. Verificar remotos
git remote -v
# origin    https://github.com/seu-usuario/react.git (fetch/push)
# upstream  https://github.com/facebook/react.git (fetch)

# 3. Sincronizar com upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# 4. Criar branch para contribuição
git checkout -b fix-documentation-bug

# 5. Fazer mudanças, commitar, pushar para seu fork
git push origin fix-documentation-bug

# 6. Abrir PR no GitHub (de seu fork → upstream)
```

---

## 📝 Simulado de Exame (Com Solução)

### Questão 1
Qual é o propósito principal de uma Pull Request no GitHub?

A) Copiar um repositório para sua conta pessoal
B) Propor mudanças para review e discussão antes de mergear no branch principal
C) Relatar um bug ou solicitar uma nova funcionalidade
D) Enviar notificações para outros membros do time

<details>
<summary>✅ Resposta Correta</summary>

**B) Propor mudanças para review e discussão antes de mergear no branch principal**

**Explicação:**
- Pull Requests servem para propor mudanças e iniciar discussões
- Permitem revisão de código antes de integrar mudanças
- São o coração da colaboração no GitHub
- Facilitam code review, discussão e aprovação de mudanças

**Por que as outras estão incorretas:**
- A) Isso é o que um **Fork** faz, não uma Pull Request
- C) Isso é o que uma **Issue** faz, não uma Pull Request
- D) Notificações são enviadas automaticamente pelo GitHub, não via PR
</details>

---

### Questão 2
Ao criar um novo repositório no GitHub, quais opções podem ser selecionadas automaticamente?

A) README.md, LICENSE e .gitignore
B) README.md, LICENSE e branch protection rules
C) README.md, .gitignore e GitHub Actions workflow
D) LICENSE, .gitignore e Issues templates

<details>
<summary>✅ Resposta Correta</summary>

**A) README.md, LICENSE e .gitignore**

**Explicação:**
- Ao criar um repositório, GitHub oferece adicionar automaticamente:
  - **README.md** - Documentação inicial
  - **LICENSE** - Licença de código aberto
  - **.gitignore** - Arquivos para ignorar do versionamento
- Estes são os três padrões disponíveis na criação de repositório

**Por que as outras estão incorretas:**
- B) Branch protection rules são configuradas APÓS criar o repositório (em Settings)
- C) GitHub Actions workflows são criados manualmente, não na criação
- D) Issues templates são criados manualmente em `.github/ISSUE_TEMPLATE/`
</details>

---

### Questão 3
Qual comando Git é necessário para enviar commits locais para o GitHub após fazer alterações localmente?

A) `git upload`
B) `git push origin main`
C) `git send origin`
D) `git sync`

<details>
<summary>✅ Resposta Correta</summary>

**B) `git push origin main`**

**Explicação:**
- `git push` envia commits locais para um repositório remoto
- `origin` é o nome padrão do remoto (pode ser alterado)
- `main` é o branch que está sendo enviado
- Sintaxe: `git push <remote> <branch>`

**Por que as outras estão incorretas:**
- A) `git upload` não existe como comando Git
- C) `git send` não existe como comando Git
- D) `git sync` não existe (existe `git pull` para receber, mas não `git sync`)
</details>

---

### Questão 4
Qual destas estratégias de merge em Pull Request PRESERVA todos os commits individuais?

A) Squash and merge
B) Merge commit
C) Rebase and merge
D) Tanto B quanto C

<details>
<summary>✅ Resposta Correta</summary>

**D) Tanto B quanto C**

**Explicação:**
- **Merge commit**: Cria um commit de merge, mas preserva todos os commits individuais
- **Rebase and merge**: Rebase os commits no topo de main e depois mergear (preserva commits)
- **Squash and merge**: Combina todos os commits em UM único commit (NÃO preserva)

**Por que as outras estão incorretas:**
- A) `Squash and merge` NÃO preserva commits individuais - eles são combinados
- B e C estão corretas, então a resposta é D

**Observação para o exame:**
- `Squash and merge` é útil para limpar histórico
- `Merge commit` mantém histórico completo
- `Rebase and merge` mantém commits mas com histórico mais limpo (linear)
</details>

---

### Questão 5
O que acontece quando você referencia uma issue em um commit com a mensagem como "Closes #123"?

A) A issue é automaticamente fechada
B) A issue é marcada como "in progress"
C) Um comentário é adicionado à issue, mas ela não é fechada
D) A issue é deletada

<details>
<summary>✅ Resposta Correta</summary>

**A) A issue é automaticamente fechada**

**Explicação:**
- Palavras-chave como `Closes`, `Fixes`, `Resolves`, ou `Closes #123` fecham automaticamente a issue referenciada
- Isso acontece quando o commit (ou PR) é mergado no branch principal
- A issue recebe um comentário automático indicando que foi fechada
- Outras palavras-chave: `closes`, `fixes`, `resolves`, `closed`, `fixed`, `resolved`

**Por que as outras estão incorretas:**
- B) Não existe status "in progress" automático
- C) Se não usar as palavras-chave corretas, a issue permanece aberta
- D) Issues nunca são deletadas automaticamente
</details>

---

### Questão 6
Qual aba do GitHub você deve usar para ver e gerenciar todos os Pull Requests de um repositório?

A) Code
B) Issues
C) Pull requests
D) Settings

<details>
<summary>✅ Resposta Correta</summary>

**C) Pull requests**

**Explicação:**
- A aba **Pull requests** lista todos os PRs do repositório
- Permite criar novos PRs, revisar, mergear e comentar
- É onde você vê o status e histórico dos PRs

**Por que as outras estão incorretas:**
- A) **Code** mostra os arquivos do repositório, branches e tags
- B) **Issues** mostra tickets e bug reports, não PRs
- D) **Settings** é para configurações do repositório
</details>

---

### Questão 7
O que é necessário fazer para contribuir em um projeto open-source que você não possui permissões diretas?

A) Clonar o repositório e fazer push para main
B) Fazer um fork do repositório, criar branch, fazer PR para o projeto original
C) Pedir permissões de admin ao owner do repositório
D) Criar uma issue pedindo para que alguém faça as mudanças

<details>
<summary>✅ Resposta Correta</summary>

**B) Fazer um fork do repositório, criar branch, fazer PR para o projeto original**

**Explicação:**
- **Fork**: Cria uma cópia do repositório em sua conta GitHub
- Você trabalha no seu fork (tem permissões totais)
- Abre um Pull Request do seu fork para o repositório original
- Mantenedores do projeto original revisam e mergear seu PR

**Workflow correto:**
1. Fork do repositório original
2. Clone seu fork
3. Criar branch para sua contribuição
4. Fazer mudanças e commits
5. Push para seu fork
6. Abrir PR para o repositório original

**Por que as outras estão incorretas:**
- A) Você não tem permissões para push direto no repositório original
- C) Você não precisa de permissões de admin - fork permite contribuição
- D) Embora você possa criar issues, a maneira correta é contribuir via PR
</details>

---

## 🔥 Dicas de Ouro para o Exame

1. **Memorize o GitHub Flow:**
   ```
   Branch → Commit → PR → Review → Merge → Delete Branch
   ```

2. **Conheça os tipos de merge:**
   - **Merge commit**: Preserva todos os commits (histórico completo)
   - **Squash and merge**: Um único commit (histórico limpo)
   - **Rebase and merge**: Commits linearizados (histórico limpo + preservação)

3. **Saiba referenciar Issues:**
   - `Closes #123` - Fecha a issue ao mergear
   - `Fixes #123` - Fecha a issue ao mergear
   - `Related to #123` - Adiciona link mas não fecha

4. **Entenda a estrutura de abas:**
   - **Code**: Arquivos, branches, releases
   - **Issues**: Tickets, bugs, feature requests
   - **Pull requests**: Propostas de mudanças
   - **Actions**: Workflows de CI/CD
   - **Settings**: Configurações do repositório

5. **Pratique o fluxo completo:**
   - Crie repositório
   - Crie branch
   - Faça commits
   - Abra PR
   - Revisar e mergear

## 📚 Recursos de Estudo

### Documentação Oficial
- [GitHub Documentation](https://docs.github.com) - Documentação completa
- [Hello World Tutorial](https://docs.github.com/en/get-started/start-your-journey/hello-world) - Tutorial inicial
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow) - Fluxo de trabalho

### Cursos
- [GitHub Skills](https://skills.github.com/) - Cursos interativos gratuitos
- [GitHub Learning Lab](https://lab.github.com/) - Laboratórios de aprendizado

### Códigos e Templates
- [Awesome README](https://github.com/matiassingers/awesome-readme) - Templates de README
- [GitHub .gitignore Templates](https://github.com/github/gitignore) - Templates de .gitignore

### Vídeos
- [GitHub Getting Started](https://www.youtube.com/playlist?list=PLg7s6r-TTFndRqM5JuMPMYD3pJY0R) - Playlist oficial
- [Git & GitHub Crash Course](https://www.youtube.com/watch?v=RGOj5yH7evk) - FreeCodeCamp

### Links Úteis
- [GitHub Glossary](https://docs.github.com/en/get-started/quickstart/github-glossary) - Glossário de termos
- [Keyboard Shortcuts](https://docs.github.com/en/get-started/using-github/keyboard-shortcuts) - Atalhos de teclado

---

**Resumo Final:** GitHub é a plataforma líder para colaboração em desenvolvimento. Para o exame GH-900, domine o fluxo GitHub Flow (Branch → Commit → PR → Review → Merge), entenda Pull Requests, Issues, merge strategies, e como contribuir em projetos open-source via fork. O sucesso vem da prática! 🚀🔗
