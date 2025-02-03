Aqui está um **README.md** completo para o projeto **LeetCode Insight**, baseado na ideia que discutimos:

---

# **LeetCode Insight**

![LeetCode](https://img.shields.io/badge/LeetCode-API-orange)
[![GraphQL](https://img.shields.io/badge/GraphQL-Middleware-blue?logo=graphql)](https://graphql.org)
[![Node.js](https://img.shields.io/badge/Node.js-Server-green?logo=node.js)](https://nodejs.org)

O **LeetCode Insight** é uma API GraphQL que atua como um **middleware stateless** entre o cliente e a API do LeetCode. Ele organiza e refina os dados disponíveis, fornecendo gráficos personalizados, informações detalhadas sobre problemas e a capacidade de escolher problemas aleatórios com base em parâmetros específicos.

---

## **Visão Geral**

O objetivo principal do **LeetCode Insight** é facilitar o acesso e a visualização dos dados do LeetCode, oferecendo funcionalidades como:

- **Gráficos de Desempenho**: Visualizações personalizadas do progresso do usuário.
- **Detalhes de Problemas**: Informações detalhadas sobre problemas específicos.
- **Escolha de Problemas Aleatórios**: Seleção de problemas com base em dificuldade, tags ou status.

A API é projetada para ser leve, escalável e fácil de integrar em aplicações como bots de Discord, interfaces web ou aplicativos móveis.

---

## **Funcionalidades Principais**

### **1. Gráficos de Desempenho**
- Exibe o progresso do usuário ao longo do tempo.
- Inclui métricas como:
  - Total de problemas resolvidos.
  - Problemas resolvidos por dificuldade (fácil, médio, difícil).
  - Progresso diário/semanal.

### **2. Detalhes de Problemas**
- Fornece informações detalhadas sobre um problema específico, como:
  - Título.
  - Descrição.
  - Dificuldade.
  - Tags (ex: arrays, hash tables, dynamic programming).

### **3. Escolha de Problemas Aleatórios**
- Seleciona problemas aleatórios com base em parâmetros como:
  - Dificuldade (fácil, médio, difícil).
  - Tags (ex: arrays, strings, trees).
  - Status (resolvido/não resolvido).

### **4. Middleware Stateless**
- Atua como uma camada intermediária entre o cliente e a API do LeetCode.
- Refina e organiza os dados para facilitar o uso.

---

## **Tecnologias Utilizadas**

### **Backend**
- **Node.js**: Runtime para execução do servidor.
- **Express GraphQL**: Para criar a API GraphQL e gerenciar as requisições.
- **Axios**: Para fazer chamadas à API do LeetCode.

### **Frontend (Opcional)**
- **React.js** ou **Next.js**: Para criar uma interface de usuário amigável.
- **Chart.js** ou **D3.js**: Para renderizar gráficos.

### **Banco de Dados (Opcional)**
- **MongoDB**: Para armazenar dados de usuários ou cache de problemas.

---

## **Como Funciona?**

1. **Requisição do Cliente**:
   - O cliente (bot do Discord, frontend, etc.) faz uma requisição GraphQL.
   - Exemplo de requisição:
     ```graphql
     query {
       getUserProgress(username: "leetcodeUser") {
         totalSolved
         easySolved
         mediumSolved
         hardSolved
         progressOverTime {
           date
           problemsSolved
         }
       }
     }
     ```

2. **Middleware**:
   - A API recebe a requisição e faz uma chamada à API do LeetCode para obter os dados brutos.
   - Processa e organiza os dados, filtrando apenas as informações necessárias.

3. **Resposta**:
   - A API retorna os dados refinados no formato GraphQL.
   - Exemplo de resposta:
     ```json
     {
       "data": {
         "getUserProgress": {
           "totalSolved": 150,
           "easySolved": 70,
           "mediumSolved": 60,
           "hardSolved": 20,
           "progressOverTime": [
             {
               "date": "2023-10-01",
               "problemsSolved": 5
             },
             {
               "date": "2023-10-02",
               "problemsSolved": 3
             }
           ]
         }
       }
     }
     ```

---

## **Instalação e Configuração**

### **Pré-requisitos**
- Node.js (v18 ou superior).
- Conta no LeetCode (opcional, dependendo das funcionalidades).

### **Passos para Executar o Projeto**
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/leetcode-insight.git
   cd leetcode-insight
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

3. Configure o arquivo `.env`:
   ```plaintext
   LEETCODE_API_KEY=sua_chave_aqui
   ```

4. Execute o projeto:
   ```bash
   npm start
   ```

5. Acesse a API GraphQL em:
   ```
   http://localhost:4000/graphql
   ```

---

## **Exemplos de Uso**

### **1. Obter Progresso do Usuário**
**Requisição**:
```graphql
query {
  getUserProgress(username: "leetcodeUser") {
    totalSolved
    easySolved
    mediumSolved
    hardSolved
    progressOverTime {
      date
      problemsSolved
    }
  }
}
```

**Resposta**:
```json
{
  "data": {
    "getUserProgress": {
      "totalSolved": 150,
      "easySolved": 70,
      "mediumSolved": 60,
      "hardSolved": 20,
      "progressOverTime": [
        {
          "date": "2023-10-01",
          "problemsSolved": 5
        },
        {
          "date": "2023-10-02",
          "problemsSolved": 3
        }
      ]
    }
  }
}
```

### **2. Detalhes de um Problema**
**Requisição**:
```graphql
query {
  getProblemDetails(titleSlug: "two-sum") {
    title
    difficulty
    description
    tags
  }
}
```

**Resposta**:
```json
{
  "data": {
    "getProblemDetails": {
      "title": "Two Sum",
      "difficulty": "Easy",
      "description": "Given an array of integers...",
      "tags": ["array", "hash-table"]
    }
  }
}
```

### **3. Problema Aleatório**
**Requisição**:
```graphql
query {
  getRandomProblem(difficulty: "medium", tags: ["array", "hash-table"]) {
    title
    difficulty
    description
  }
}
```

**Resposta**:
```json
{
  "data": {
    "getRandomProblem": {
      "title": "Container With Most Water",
      "difficulty": "Medium",
      "description": "Given n non-negative integers..."
    }
  }
}
```

---

## **Contribuição**

Contribuições são bem-vindas! Siga os passos abaixo:
1. Faça um fork do repositório.
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`).
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`).
4. Faça push para a branch (`git push origin feature/nova-feature`).
5. Abra um pull request.

---

## **Licença**

Este projeto está licenciado sob a **MIT License**. Consulte o arquivo `LICENSE` para mais detalhes.

---

## Contato
- **Discord:** umgnomochamadoaltair
- **GitHub:** [eRRe-i](https://github.com/eRRe-i)
