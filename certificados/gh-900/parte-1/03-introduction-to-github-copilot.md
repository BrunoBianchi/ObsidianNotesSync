# Introduction to GitHub Copilot

## 📚 Pesquisa e Síntese

### O que é GitHub Copilot?
GitHub Copilot é um assistente de programação com IA (Artificial Intelligence) que fornece sugestões de código em tempo real enquanto você digita. Desenvolvido pela GitHub em parceira com a OpenAI, utiliza o modelo de linguagem Codex para entender o contexto do seu código e gerar sugestões relevantes.

### O que é cobrado no exame GH-900 sobre GitHub Copilot?

O exame foca nos fundamentos do Copilot, sua integração com ambientes de desenvolvimento e os planos de subscrição. Os principais tópicos são:

1. **Integração com VS Code e IDEs**
   - Instalar a extensão do GitHub Copilot
   - Configurar autenticação no VS Code
   - Ativar/desativar Copilot no editor
   - Atalhos de teclado padrão

2. **Sugestões de Código (Inline Suggestions)**
   - Sugestões automáticas ao digitar
   - Aceitar/Rejeitar sugestões (Tab, Esc)
   - Ver múltiplas sugestões (Ctrl/Cmd + Enter)
   - Context-aware completions

3. **Chat do Copilot (Copilot Chat)**
   - Fazer perguntas sobre código
   - Explicar funções e arquivos
   - Sugerir melhorias de código
   - Gerar código a partir de descrições

4. **Planos de Subscrição**
   - Copilot Free (grátis, limitado)
   - Copilot Pro (individual, recursos avançados)
   - Copilot Business/Enterprise (empresarial, recursos corporativos)
   - Diferenças de recursos e limites

5. **Funcionalidades Adicionais**
   - Copilot Workspace (contexto do repositório)
   - Copilot CLI (interface de linha de comando)
   - Copilot no GitHub Mobile
   - Copilot em Codespaces

### Tecnologias por Trás do Copilot

| Tecnologia | Descrição |
|------------|-----------|
| **OpenAI Codex** | Modelo de linguagem baseado em GPT-4, fine-tuned para código |
| **Context Awareness** | Copilot analisa seu código, comentários e arquivos relacionados |
| **Multi-language Support** | Suporta Python, JavaScript, TypeScript, Ruby, Go, C#, C++, e mais |
| **Framework Support** | Funciona com React, Vue, Angular, Django, Flask, etc. |

---

## 💻 Cenário Prático (Mão na Massa)

### Exercício 1: Instalando e Configurando Copilot no VS Code

**Via VS Code:**

1. Abra o **Visual Studio Code**
2. Vá para a aba de **Extensions** (ícone de quadrados no sidebar esquerdo)
3. Digite `GitHub Copilot` na barra de busca
4. Encontre a extensão oficial "GitHub Copilot" (pela GitHub)
5. Clique em **Install**
6. Após a instalação, clique no ícone do Copilot na barra de status (canto inferior direito)
7. Selecione **Sign in to GitHub**
8. Copilot abrirá uma janela de autenticação em seu navegador
9. Acesse sua conta do GitHub
10. Copile um plano (Free, Pro, ou Business)
11. Retorne ao VS Code - Copilot deve estar ativo

### Exercício 2: Usando Sugestões Inline (Inline Suggestions)

**Em JavaScript:**

1. Crie um novo arquivo `calculator.js`
2. Digite o seguinte código:

```javascript
function add(a, b) {
    // O Copilot sugerirá automaticamente:
    return a + b;
}
```

3. Quando o Copilot sugerir código em cinza, pressione **Tab** para aceitar
4. Continue digitando mais funções:

```javascript
function subtract(a, b) {
    return a - b;
}

function multiply(a, b) {
    return a * b;
}

function divide(a, b) {
    if (b === 0) {
        return "Cannot divide by zero";
    }
    return a / b;
}
```

**Em Python:**

```python
def calculate_factorial(n):
    # Copilot sugerirá:
    if n == 0 or n == 1:
        return 1
    else:
        return n * calculate_factorial(n - 1)
```

### Exercício 3: Ver Múltiplas Sugestões

1. Comece a digitar uma função:

```javascript
function formatName(firstName, lastName) {
```

2. Em vez de aceitar a primeira sugestão, pressione **Ctrl/Cmd + Enter**
3. Copilot mostrará múltiplas sugestões (geralmente 3 opções)
4. Use as setas **↑ ↓** (ou Ctrl/N) para navegar entre sugestões
5. Pressione **Tab** para aceitar a sugestão desejada

### Exercício 4: Usando o Copilot Chat

**No VS Code:**

1. Abra a aba **Copilot Chat** no sidebar esquerdo (ícone de robô)
2. Clique no campo de texto na parte inferior do painel de chat
3. Digite perguntas e pressione Enter:

```text
// Exemplo de perguntas:

"Explicar este arquivo"
"Como posso melhorar esta função?"
"Gere uma função que valide emails"
"Escreva testes unitários para este código"
"Qual é a complexidade deste algoritmo?"
```

**Com Contexto de Código:**

1. Selecione algumas linhas de código no editor
2. Abra o Copilot Chat
3. Digite:

```text
"Explicar as linhas selecionadas"
"Adicionar comentários a estas linhas"
"Refatorar este código para ser mais legível"
"Encontrar bugs neste código"
```

4. Copilot fornecerá respostas específicas sobre o código selecionado

### Exercício 5: Gerando Código com Prompt Descritivo

**Gerar Função:**

1. Abra o Copilot Chat
2. Digite:

```text
"Gere uma função em Python que calcule a distância entre dois pontos em 3D"
```

3. Copilot gerará:

```python
import math

def calculate_distance_3d(point1, point2):
    """
    Calcula a distância euclidiana entre dois pontos em 3D.
    
    Args:
        point1: Tuple (x, y, z) para o primeiro ponto
        point2: Tuple (x, y, z) para o segundo ponto
    
    Returns:
        float: Distância entre os dois pontos
    """
    x1, y1, z1 = point1
    x2, y2, z2 = point2
    
    distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2 + (z2 - z1)**2)
    return distance
```

4. Clique em **Insert at Cursor** para adicionar ao seu arquivo

**Gerar API Endpoint:**

```text
"Gere um endpoint REST em Express.js que cria um usuário"
```

Copilot gerará:

```javascript
const express = require('express');
const router = express.Router();

// POST /api/users - Criar um novo usuário
router.post('/users', (req, res) => {
    const { name, email, password } = req.body;
    
    // Validação básica
    if (!name || !email || !password) {
        return res.status(400).json({ 
            error: 'Todos os campos são obrigatórios' 
        });
    }
    
    // Criar usuário (exemplo com banco de dados)
    const newUser = {
        id: Date.now(),
        name,
        email,
        password: hash(password), // Sempre hashear senhas!
        createdAt: new Date()
    };
    
    // Salvar no banco de dados
    // ...
    
    res.status(201).json({
        message: 'Usuário criado com sucesso',
        user: { id: newUser.id, name: newUser.name, email: newUser.email }
    });
});

module.exports = router;
```

### Exercício 6: Desativando e Configurando Copilot

**Desativar Temporariamente:**

1. No VS Code, pressione **Ctrl/Cmd + Shift + P** para abrir a Command Palette
2. Digite `GitHub Copilot: Disable`
3. Selecione a opção para desativar Copilot
4. Para reativar, use `GitHub Copilot: Enable`

**Atalhos de Teclado Personalizados:**

1. Abra **File** → **Preferences** → **Keyboard Shortcuts**
2. Busque por "copilot"
3. Você pode personalizar atalhos como:
   - `GitHub Copilot: Trigger Copilot` (geralmente Ctrl/Cmd + Enter)
   - `GitHub Copilot: Accept Suggestion` (Tab)
   - `GitHub Copilot: Reject Suggestion` (Esc)

---

## 📝 Simulado de Exame (Com Solução)

### Questão 1
Qual atalho é usado para aceitar uma sugestão de código do GitHub Copilot no VS Code?

A) Ctrl/Cmd + S
B) Tab
C) Enter
D) Ctrl/Cmd + V

<details>
<summary>✅ Resposta Correta</summary>

**B) Tab**

**Explicação:**
- Pressionar **Tab** aceita a sugestão de código cinza do Copilot
- Isso funciona automaticamente quando Copilot faz uma sugestão inline
- A sugestão é inserida na posição do cursor

**Por que as outras estão incorretas:**
- A) Ctrl/Cmd + S salva o arquivo, não aceita sugestões
- C) Enter geralmente cria uma nova linha, não aceita sugestões
- D) Ctrl/Cmd + V cola, não aceita sugestões
</details>

---

### Questão 2
Como você pode ver múltiplas sugestões alternativas do Copilot para um único contexto?

A) Pressionar Shift + Tab
B) Pressionar Ctrl/Cmd + Enter
C) Pressionar F5
D) Esperar 5 segundos

<details>
<summary>✅ Resposta Correta</summary>

**B) Pressionar Ctrl/Cmd + Enter**

**Explicação:**
- **Ctrl/Cmd + Enter** exibe múltiplas sugestões alternativas
- Geralmente são 3 opções diferentes para o mesmo contexto
- Use as setas ↑ ↓ para navegar e Tab para aceitar

**Por que as outras estão incorretas:**
- A) Shift + Tab não é um atalho válido para ver sugestões
- C) F5 recarrega a janela/editor, não mostra sugestões
- D) Esperar não altera as sugestões disponíveis
</details>

---

### Questão 3
Qual plano do GitHub Copilot é grátis e oferece funcionalidades limitadas?

A) Copilot Free
B) Copilot Basic
C) Copilot Starter
D) Copilot Lite

<details>
<summary>✅ Resposta Correta</summary>

**A) Copilot Free**

**Explicação:**
- **Copilot Free** é o plano grátis do GitHub Copilot
- Oferece sugestões inline e chat limitados
- Não requer cartão de crédito
- Ideal para experimentar o Copilot

**Por que as outras estão incorretas:**
- B) Não existe "Copilot Basic" como plano oficial
- C) Não existe "Copilot Starter" como plano oficial
- D) Não existe "Copilot Lite" como plano oficial

**Planos disponíveis:**
- Copilot Free (grátis)
- Copilot Pro (individual, $10/mês)
- Copilot Business (empresarial, $19/usuário/mês)
- Copilot Enterprise (empresarial, recursos avançados)
</details>

---

### Questão 4
Qual atalho é usado para rejeitar uma sugestão de código do Copilot?

A) Backspace
B) Delete
C) Esc
D) Ctrl/Cmd + Z

<details>
<summary>✅ Resposta Correta</summary>

**C) Esc**

**Explicação:**
- Pressionar **Esc** rejeita/descearta a sugestão atual do Copilot
- A sugestão cinza desaparece
- Você pode continuar digitando sem usar a sugestão

**Por que as outras estão incorretas:**
- A) Backspace apaga caractares antes do cursor, não rejeita sugestões
- B) Delete apaga caractares depois do cursor, não rejeita sugestões
- D) Ctrl/Cmd + Z desfaz ações, não rejeita sugestões
</details>

---

### Questão 5
Onde você acessa o Copilot Chat no Visual Studio Code?

A) Na aba Problems
B) Na aba Output
C) Na aba Copilot Chat no sidebar
D) No menu File

<details>
<summary>✅ Resposta Correta</summary>

**C) Na aba Copilot Chat no sidebar**

**Explicação:**
- O **Copilot Chat** está disponível como uma aba no sidebar esquerdo
- O ícone é um robô (🤖)
- Permite fazer perguntas, pedir explicações e gerar código

**Por que as outras estão incorretas:**
- A) A aba Problems mostra erros e avisos do editor
- B) A aba Output mostra logs e mensagens de ferramentas
- D) O menu File contém operações de arquivo, não o chat
</details>

---

### Questão 6
Qual funcionalidade permite ao Copilot analisar o contexto de todo o seu repositório?

A) Copilot Free
B) Copilot Workspace
C) Copilot Pro
D) Copilot Chat

<details>
<summary>✅ Resposta Correta</summary>

**B) Copilot Workspace**

**Explicação:**
- **Copilot Workspace** permite ao Copilot entender o contexto do repositório completo
- Disponível em planos pagos (Pro, Business, Enterprise)
- Permite sugestões mais precisas baseadas em todo o código

**Por que as outras estão incorretas:**
- A) Copilot Free é o plano grátis, não uma funcionalidade
- C) Copilot Pro é um plano de subscrição, não uma funcionalidade específica
- D) Copilot Chat é a interface de conversa, não o contexto do repositório
</details>

---

### Questão 7
Para usar o GitHub Copilot no VS Code, o que é necessário primeiro?

A) Instalar o VS Code
B) Ter uma conta do GitHub
C) Instalar a extensão do GitHub Copilot
D) Todas as alternativas anteriores

<details>
<summary>✅ Resposta Correta</summary>

**D) Todas as alternativas anteriores**

**Explicação:**
- Você precisa do **VS Code** instalado
- Precisa de uma **conta do GitHub** para autenticação
- Precisa da **extensão do GitHub Copilot** instalada
- Após instalar a extensão, você precisa **autenticar** com o GitHub
- Precisa de um **plano** (Free, Pro, ou Business)

**Por que as outras estão incorretas:**
- A, B, C são necessários, mas nenhuma é suficiente sozinha
- A resposta correta é "todas", pois são pré-requisitos conjuntos
</details>

---

## 🔥 Dicas para o Exame

1. **Memorize os atalhos padrão:**
   - **Tab** → Aceitar sugestão
   - **Esc** → Rejeitar sugestão
   - **Ctrl/Cmd + Enter** → Ver múltiplas sugestões

2. **Conheça os planos:**
   - **Free**: Grátis, limitado, bom para experimentar
   - **Pro**: Individual, recursos avançados, sem limites
   - **Business**: Empresarial, recursos corporativos, controle administrativo

3. **Entenda quando usar o Chat:**
   - Explicar código existente
   - Pedir melhorias
   - Gerar código do zero
   - Responder perguntas sobre programação

4. **Saiba sobre Workspace:**
   - Funcionalidade que analisa contexto do repositório
   - Disponível em planos pagos
   - Sugestões mais inteligentes e contextuais

5. **Pratique com diferentes linguagens:**
   - JavaScript/TypeScript
   - Python
   - Java
   - C#
   - Go

## 📚 Recursos Adicionais

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Quickstart for GitHub Copilot](https://docs.github.com/en/copilot/get-started/quickstart)
- [Plans for GitHub Copilot](https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot)
- [Prompt Engineering for Copilot](https://docs.github.com/en/copilot/using-github-copilot/prompt-engineering-for-github-copilot)
- [VS Code Copilot Documentation](https://code.visualstudio.com/docs/copilot/)

---

Pratique usar o Copilot com seu código real e você entenderá rapidamente como ele funciona! 🤖✨
