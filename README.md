# 🗄️ Modelagem de Dados: As 5 Formas Normais (FN)

Este repositório contém um resumo técnico sobre o processo de **Normalização**, técnica aplicada ao modelo relacional para reduzir a redundância de dados e evitar anomalias de atualização, inserção e exclusão.

---

## 📌 Visão Geral

A normalização é baseada na aplicação de regras sucessivas. Para que uma tabela esteja em uma forma normal superior, ela obrigatoriamente deve atender aos requisitos de todas as formas anteriores.

---

## 🚀 As 5 Formas Normais

### 1ª Forma Normal (1FN) - Atomicidade
**Objetivo:** Eliminar grupos repetidos e colunas com múltiplos valores.
* **Regra:** Cada célula deve conter apenas um valor **atômico** (indivisível).
* **Ação:** Remova listas, conjuntos ou vetores de uma única coluna e crie novas linhas ou tabelas.
* *Exemplo:* Uma coluna "Telefones" com "9999-9999, 8888-8888" fere a 1FN.

### 2ª Forma Normal (2FN) - Dependência Parcial
**Objetivo:** Garantir que todos os atributos dependam da chave primária inteira.
* **Regra:** Deve estar na 1FN e nenhum atributo não-chave pode depender de apenas **parte** de uma chave primária composta.
* **Ação:** Se um atributo depende apenas de um dos campos da chave composta, mova-o para uma nova tabela.
* *Exemplo:* Em uma tabela "ItemPedido" (ID_Pedido, ID_Produto), o "Nome_Produto" deve sair, pois depende apenas do ID_Produto.

### 3ª Forma Normal (3FN) - Dependência Transitiva
**Objetivo:** Eliminar dependências entre colunas que não são chaves.
* **Regra:** Deve estar na 2FN e nenhum atributo não-chave pode depender de outro atributo não-chave.
* **Ação:** Se a Coluna B depende da Coluna A, e a Coluna A depende da Chave, mova A e B para uma tabela própria.
* *Exemplo:* Na tabela "Cliente", o "Nome_Cidade" depende do "CEP", que por sua vez depende do ID_Cliente. O ideal é ter uma tabela de CEPs.

### 4ª Forma Normal (4FN) - Dependências Multivaloradas
**Objetivo:** Separar fatos independentes sobre a mesma entidade.
* **Regra:** Deve estar na 3FN e não pode conter duas ou mais dependências multivaloradas independentes entre si.
* **Ação:** Se uma entidade possui dois atributos independentes que podem ter múltiplos valores, separe-os.
* *Exemplo:* Um "Professor" que possui vários "Cursos" e vários "Hobbies". Cursos e Hobbies não têm relação e devem ser tabelas distintas.

### 5ª Forma Normal (5FN) - Dependência de Junção
**Objetivo:** Tratar de casos raros onde a informação só faz sentido quando três ou mais tabelas são unidas.
* **Regra:** Também chamada de PJNF (*Projection-Join Normal Form*), ocorre quando uma tabela não pode ser decomposta em tabelas menores sem perder a integridade da regra de negócio original.
* **Ação:** É a forma mais complexa e garante que a reconstrução dos dados via `JOIN` seja idêntica ao original.

---

## 💡 Resumo Prático

| Forma Normal | Foco Principal |
| :--- | :--- |
| **1FN** | Valores Atômicos (Células únicas) |
| **2FN** | Dependência da Chave Primária Total |
| **3FN** | Fim da dependência entre colunas comuns |
| **4FN** | Isolamento de multivalores independentes |
| **5FN** | Integridade na reconstrução de junções complexas |

---
> **Nota:** No mercado, atingir a **3ª Forma Normal** é considerado o padrão de excelência para a maioria dos sistemas OLTP (Online Transaction Processing).
