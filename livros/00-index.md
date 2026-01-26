---
tags: [livros, indice, colecao]
cssclass: indice-principal
created: 2026-01-26
updated: 2026-01-26
---

# 📚 Índice de Livros

Bem-vindo à biblioteca pessoal de leitura e estudos.

## Categorias

### 📖 Programação e Desenvolvimento de Software

| Livro | Status | Progresso | Última Leitura |
|-------|--------|-----------|----------------|
| [[programador-pragmático]] | 📖 Em leitura | 10% | 2026-01-26 |

### 📚 Outras Categorias

*Mais categorias serão adicionadas conforme necessário.*

## Livros Recentes

### 📕 Programador Pragmático

> [[programador-pragmático|Ver todas as notas]]

**Autores:** Andrew Hunt, David Thomas

**Capítulos Lidos:**
- [[programador-pragmático/capitulo-01-o-pragmatico|Capítulo 1: O Pragmático]]
- [[programador-pragmático/capitulo-02-manejando-grep|Capítulo 2: Manejando Grep]]

**Resumo Rápido:**
Um guia essencial para desenvolvedores que desejam melhorar suas habilidades e adotar uma mentalidade pragmática na programação.

## Estatísticas

| Métrica | Valor |
|---------|-------|
| 📚 Total de livros | 1 |
| 📖 Em leitura | 1 |
| ✅ Concluídos | 0 |
| 📝 Total de notas | 3 |

## Filtros

### Por Status

```dataview
TABLE WITHOUT ID
  link(file.link, title) AS "Livro",
  status AS "Status",
  progress AS "Progresso"
FROM "livros"
WHERE file.name != "00-index"
SORT status DESC
```

### Por Data de Leitura

```dataview
TABLE WITHOUT ID
  link(file.link, title) AS "Livro",
  date(ultima-leitura) AS "Última Leitura"
FROM "livros"
WHERE ultima-leitura
SORT date(ultima-leitura) DESC
```

## Metas de Leitura

### 🎯 2026

- [x] Começar a ler Programador Pragmático
- [ ] Concluir Programador Pragmático
- [ ] Ler Clean Code
- [ ] Ler Design Patterns
- [ ] Ler Refactoring

### 📅 Leitura Atual

**Livro:** [[programador-pragmático|Programador Pragmático]]

**Meta:** Ler 1 capítulo por semana

**Próximo capítulo:** [[programador-pragmático/capitulo-03-a-batalha-pela-pureza|Capítulo 3: A Batalha pela Pureza]]

## Links Rápidos

- 📌 [[programador-pragmático|Programador Pragmático]] - Notas detalhadas
- 📌 [[livros/00-index|Livros]] - Coleção de livros
- 📌 [[desenvolvimento-de-software]] - Área de conhecimento
- 📌 [[melhores-praticas]] - Guia de práticas recomendadas

---

**Última atualização:** 2026-01-26
