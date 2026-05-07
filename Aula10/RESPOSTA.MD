# Exercício Prático: Modelagem e Consultas em MongoDB

Este exercício visa consolidar os conceitos de modelagem NoSQL (Incorporação vs. Referência) e o uso do Framework de Agregação.

---

# Parte 1: Modelagem de Dados

## 1. Incorporação (Embedding)

### Documento do curso com módulos incorporados

```json
{
  "_id": 1,
  "nome": "Curso de Desenvolvimento Web",
  "categoria": "Tecnologia",
  "modulos": [
    {
      "nome": "HTML e CSS",
      "carga_horaria": 20
    },
    {
      "nome": "JavaScript",
      "carga_horaria": 30
    },
    {
      "nome": "MongoDB",
      "carga_horaria": 25
    }
  ]
}
```

### Pergunta:
Por que incorporar os módulos melhora o desempenho de leitura?

### Resposta:
Porque todas as informações relacionadas ao curso ficam em um único documento. Assim, ao consultar um curso, o MongoDB retorna os módulos junto com ele, evitando múltiplas consultas ou junções (`joins`), melhorando o desempenho da leitura.

---

## 2. Referência (Reference)

### Documento do Instrutor

```json
{
  "_id": 100,
  "nome": "Ana Souza",
  "especialidade": "Banco de Dados",
  "email": "ana@email.com"
}
```

### Documento do Curso referenciando o instrutor

```json
{
  "_id": 200,
  "nome": "MongoDB Avançado",
  "categoria": "Tecnologia",
  "instrutor_id": 100
}
```

### Pergunta:
Em que situação seria melhor usar referência?

### Resposta:
Quando o mesmo instrutor ministra vários cursos. Nesse caso, usar referência evita duplicação de dados, facilita atualizações e mantém as informações consistentes.

---

# Parte 2: Consultas e Filtros

## 1. Filtro de Existência

```javascript
db.clientes.find({
  email: { $exists: true }
})
```

---

## 2. Filtro de Comparação

```javascript
db.clientes.find({
  idade: { $gte: 21 }
})
```

---

## 3. Filtro Complexo

```javascript
db.clientes.find({
  cidade: "São Paulo",
  idade: { $lt: 30 }
})
```

---

# Parte 3: Aggregation Framework (Relatórios)

## Pipeline de Agregação

```javascript
db.vendas.aggregate([
  {
    $match: {
      status: "concluída"
    }
  },
  {
    $group: {
      _id: "$categoria",
      total_quantidade_vendida: {
        $sum: "$quantidade"
      }
    }
  }
])
```

---

# Explicação do Pipeline

## `$match`
Filtra apenas as vendas com status `"concluída"`.

## `$group`
Agrupa os documentos pelo campo `categoria`.

## `$sum`
Realiza a soma da quantidade total vendida por categoria.