# Introduction to GitHub

## 📚 Pesquisa e Síntese

### O que é GitHub?
GitHub é uma plataforma de hospedagem de código baseada em Git que permite colaboração em tempo real, controle de versão distribuído e uma variedade de ferramentas para desenvolvimento de software. Fundada em 2008, atualmente é a maior plataforma do mundo para desenvolvimento colaborativo, com mais de 100 milhões de desenvolvedores.

### O que é cobrado no exame GH-900 sobre GitHub?

O exame foca nos conceitos fundamentais da interface do GitHub e no fluxo de trabalho colaborativo (GitHub Flow). Os principais tópicos são:

1. **Repositórios (Repositories)**
   - Criar repositórios (públicos e privados)
   - Clonar repositórios existentes
   - Estrutura de arquivos (README, LICENSE, .gitignore)
   - Branches (ramificações)

2. **Issues (Tickets/Bug Reports)**
   - Criar issues para rastrear bugs e feature requests
   - Adicionar labels, assignees e milestones
   - Usar templates de issues
   - Fechar e referenciar issues

3. **Pull Requests (PRs)**
   - Criar PRs para propor mudanças
   - Revisar código (code review)
   - Merge strategies (merge commit, squash, rebase)
   - Resolver conflicts

4. **Fluxo Básico da UI**
   - Navegar pela interface do GitHub
   - Abas principais (Code, Issues, Pull Requests, Actions, Settings)
   - Editar arquivos na web
   - Visualizar histórico e diffs

5. **Conceitos de Colaboração**
   - Forking (copiar repositório para sua conta)
   - GitHub Flow (Branch → PR → Review → Merge)
   - Discussions e Comments
   - Notifications

### Estrutura de um Repositório

```
meu-repositorio/
├── .github/           # Configurações específicas do GitHub
│   ├── ISSUE_TEMPLATE/  # Templates para issues
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/       # GitHub Actions
├── README.md           # Documentação do projeto
├── LICENSE             # Licença do projeto
├── .gitignore          # Arquivos a ignorar
└── [seus arquivos]    # Código do projeto
```

### O GitHub Flow

O GitHub Flow é um fluxo de trabalho simplificado para desenvolvimento colaborativo:

1. **Create Branch** - Criar um branch a partir de `main`
2. **Make Changes** - Fazer alterações e commits
3. **Open Pull Request** - Abrir PR para discussão e review
4. **Discuss & Review** - Discussir e revisar as mudanças
5. **Merge** - Mergear PR para `main`
6. **Delete Branch** - Deletar o branch (opcional)

---

## 💻 Cenário Prático (Mão na Massa)

### Exercício 1: Criando um Repositório no GitHub

**Via Interface Web:**

1. Acesse https://github.com
2. No canto superior direito, clique no sinal de **+** → **New repository**
3. Preencha:
   - **Repository name:** `hello-github`
   - **Description:** `Aprendendo GitHub Flow`
   - **Visibility:** Public ou Private
   - **Add a README file:** ✅ (Marque esta opção)
   - **Choose a license:** MIT License (opcional)
4. Clique em **Create repository**

### Exercício 2: Criando um Branch e Fazendo Alterações

1. No seu repositório `hello-github`, verifique o branch atual (deve estar em `main`)
2. Abaixo do nome do repositório, clique no dropdown que diz `main`
3. Digite `meu-primeiro-branch` no campo de texto
4. Clique em **Create branch: meu-primeiro-branch from main**
5. Agora você está no novo branch `meu-primeiro-branch`

**Editando o README.md:**

1. Clique no arquivo `README.md`
2. Clique no ícone de lápis (✏️) no canto superior direito
3. Adicione o seguinte conteúdo:

```markdown
# Hello GitHub

Este é meu primeiro repositório no GitHub!

## Sobre Mim
- Aprendendo GitHub Flow
- Praticando Pull Requests
- Explorando a interface do GitHub

## Objetivos
- [ ] Criar meu primeiro branch
- [ ] Fazer commits
- [ ] Abrir um Pull Request
- [ ] Mergear no main

## Links
- [GitHub Documentation](https://docs.github.com)
- [GitHub Skills](https://skills.github.com)
```

4. No campo **Commit changes**:
   - **Add an optional extended description:** `Add README with personal info and goals`
   - **Commit directly to `meu-primeiro-branch`**
5. Clique em **Commit changes**

### Exercício 3: Abrindo um Pull Request

1. Clique na aba **Pull requests** no topo do repositório
2. Clique em **New pull request**
3. Verifique as informações:
   - **base:** `main` ← este é onde as mudanças serão aplicadas
   - **compare:** `meu-primeiro-branch` ← este é seu branch com as mudanças
4. Verifique o diff (diferenças entre os branches)
5. Clique em **Create pull request**
6. Preencha:
   - **Title:** `Add personal README with goals`
   - **Description:**
     ```markdown
     ## Descrição
     Este PR adiciona informações pessoais e objetivos ao README.
     
     ## Alterações
     - Adicionado seção "Sobre Mim"
     - Adicionado checklist de objetivos
     - Adicionado links úteis
     
     ## Testes
     - [ ] Verificado no navegador
     - [ ] Links funcionando
     
     Closes #0 (se houver uma issue relacionada)
     ```
7. Clique em **Create pull request**

### Exercício 4: Revisando e Mergendo um Pull Request

1. No seu PR, clique na aba **Files changed** para ver as alterações
2. Clique em qualquer linha para adicionar um comentário de revisão (simule uma review)
3. Adicione um comentário: `Ótima adição! Os links estão funcionando?`
4. Clique em **Start a review** → **Submit review**
5. Selecione **Approve** e adicione um comentário geral
6. Volte para a aba **Conversation** do PR
7. No final da página, clique em **Merge pull request**
8. Escolha uma estratégia de merge:
   - **Merge commit** - Preserva todo o histórico
   - **Squash and merge** - Combina todos os commits em um
   - **Rebase and merge** - Rebase os commits e mergear
9. Para este exercício, selecione **Merge commit**
10. Clique em **Confirm merge**
11. Após o merge, clique em **Delete branch** para limpar

### Exercício 5: Trabalhando com Issues

**Criando uma Issue:**

1. Clique na aba **Issues** no topo do repositório
2. Clique em **New issue**
3. Preencha:
   - **Title:** `Adicionar seção de recursos aprendidos`
   - **Descrição:**
     ```markdown
     ## Descrição
     Seria legal adicionar uma seção no README listando todos os recursos do GitHub que aprendi.
     
     ## O que deve ser incluído
     - Repositórios
     - Issues
     - Pull Requests
     - Markdown
     - GitHub Actions (básico)
     
     ## Prioridade
     - Baixa
     
     ## Labels
     - enhancement
     - documentation
     ```
4. Adicione labels (selecione no menu lateral direito):
   - `enhancement`
   - `documentation`
5. Adicione assignees (opcional): Selecione você mesmo
6. Clique em **Submit new issue**

**Referenciando Issues em Commits e PRs:**

1. Anote o número da issue que você acabou de criar (ex: #1)
2. Crie um novo branch: `add-resources-section`
3. Edite o README.md e adicione:

```markdown
## Recursos do GitHub Aprendidos

### Repositórios
- Criar e gerenciar repositórios
- Branches e commits
- README e documentação

### Issues
- Criar e gerenciar issues
- Labels e assignees
- Templates de issues

### Pull Requests
- Abrir e revisar PRs
- Merge strategies
- Resolvendo conflicts

### Markdown
- Headers e formatação
- Listas e links
- Imagens e código
```

4. Faça commit com mensagem: `Add resources section to README`

```markdown
Closes #1
```

A palavra-chave `Closes` (ou `Fixes`, `Resolves`) automaticamente fecha a issue #1 quando o PR for mergado.

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

## 🔥 Dicas para o Exame

1. **Memorize o GitHub Flow:**
   ```
   Branch → Changes → Commit → PR → Review → Merge → Delete Branch
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

## 📚 Recursos Adicionais

- [GitHub Hello World Tutorial](https://docs.github.com/en/get-started/start-your-journey/hello-world)
- [GitHub Flow Documentation](https://docs.github.com/en/get-started/quickstart/github-flow)
- [About Pull Requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests)
- [Managing Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue)
- [GitHub Skills: Introduction to GitHub](https://skills.github.com/)

---

Pratique estes exercícios na interface web do GitHub e você estará bem preparado para o tópico "Introduction to GitHub" do GH-900! 🚀
