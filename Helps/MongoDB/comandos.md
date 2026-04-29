# MongoDB - Comandos de Apoio

Este arquivo reúne os principais comandos MongoDB usados na aula, desde o CRUD ate a criacao de indices, com a explicacao de cada um.

## Acessar o MongoDB

O comando abaixo abre o terminal interativo do MongoDB.

```bash
mongosh
```

## Criar e selecionar banco de dados

O comando `use` seleciona um banco de dados. Se ele nao existir, sera criado no primeiro insert.

```javascript
use loja_virtual
```

## Ver bancos e colecoes

`show dbs` lista os bancos existentes.
`show collections` lista as colecoes do banco atual.
`db` mostra qual banco esta selecionado no momento.

```javascript
show dbs
show collections
db
```

## CREATE - Inserir documentos

### Inserir um produto

`insertOne()` insere um unico documento na colecao.

```javascript
db.produtos.insertOne({
  nome: "Smartphone Galaxy A15",
  categoria: "Eletronicos",
  preco: 1299.90,
  marca: "Samsung"
})
```

### Inserir varios produtos

`insertMany()` insere varios documentos de uma vez. Cada documento pode ter campos diferentes, o que mostra a flexibilidade do MongoDB.

```javascript
db.produtos.insertMany([
  {
    nome: "Livro MongoDB na Pratica",
    categoria: "Livros",
    preco: 79.90,
    autor: "Joao Silva"
  },
  {
    nome: "Camiseta Basica",
    categoria: "Roupas",
    preco: 49.90,
    tamanho: "M",
    cor: "Preta"
  }
])
```

## READ - Consultar documentos

### Listar todos os produtos

`find()` retorna todos os documentos da colecao.
`pretty()` organiza melhor a exibicao no terminal.

```javascript
db.produtos.find()
db.produtos.find().pretty()
```

### Buscar um unico documento

`findOne()` retorna apenas o primeiro documento encontrado.

```javascript
db.produtos.findOne()
db.produtos.findOne({ nome: "Camiseta Basica" })
```

### Filtrar por campo

Aqui a busca retorna apenas documentos que atendem a condicao informada.

```javascript
db.produtos.find({ categoria: "Livros" })
db.produtos.find({ preco: 79.90 })
```

### Filtrar com operadores

Esses operadores comparam valores:
- `$gt`: maior que
- `$lt`: menor que
- `$gte`: maior ou igual
- `$lte`: menor ou igual
- `$ne`: diferente de

```javascript
db.produtos.find({ preco: { $gt: 100 } })
db.produtos.find({ preco: { $lt: 100 } })
db.produtos.find({ preco: { $gte: 50 } })
db.produtos.find({ preco: { $lte: 1300 } })
db.produtos.find({ preco: { $ne: 49.90 } })
```

### Consultar com AND e OR

Quando colocamos mais de um campo no mesmo objeto, o MongoDB entende como `AND`.
Ja o operador `$or` permite buscar por uma condicao ou outra.

```javascript
db.produtos.find({
  categoria: "Roupas",
  preco: { $lt: 100 }
})

db.produtos.find({
  $or: [
    { categoria: "Livros" },
    { categoria: "Eletronicos" }
  ]
})
```

### Projecao

A projecao serve para escolher quais campos devem aparecer no resultado.
No exemplo abaixo, serao exibidos apenas `nome` e `preco`, escondendo o `_id`.

```javascript
db.produtos.find(
  {},
  { nome: 1, preco: 1, _id: 0 }
)
```

### Ordenacao

`sort({ campo: 1 })` ordena em ordem crescente.
`sort({ campo: -1 })` ordena em ordem decrescente.

```javascript
db.produtos.find().sort({ preco: 1 })
db.produtos.find().sort({ preco: -1 })
```

### Limitar resultados

`limit()` restringe a quantidade de documentos retornados.

```javascript
db.produtos.find().limit(2)
```

### Contar documentos

`countDocuments()` conta quantos documentos existem na colecao ou quantos atendem a um filtro.

```javascript
db.produtos.countDocuments()
db.produtos.countDocuments({ categoria: "Livros" })
```

## UPDATE - Atualizar documentos

### Atualizar um unico documento

`updateOne()` atualiza apenas o primeiro documento que combinar com o filtro.
`$set` altera ou cria o campo informado.

```javascript
db.produtos.updateOne(
  { nome: "Smartphone Galaxy A15" },
  { $set: { preco: 1199.90 } }
)
```

### Adicionar campo em todos os documentos

`updateMany()` atualiza varios documentos ao mesmo tempo.
Neste caso, o campo `estoque` sera criado em todos os produtos.

```javascript
db.produtos.updateMany(
  {},
  { $set: { estoque: 10 } }
)
```

### Atualizar varios documentos com filtro

Aqui o MongoDB altera apenas os documentos que pertencem a categoria `Roupas`.

```javascript
db.produtos.updateMany(
  { categoria: "Roupas" },
  { $set: { promocao: true } }
)
```

### Incrementar valor

`$inc` aumenta ou diminui automaticamente um valor numerico.

```javascript
db.produtos.updateOne(
  { nome: "Camiseta Basica" },
  { $inc: { estoque: 5 } }
)
```

## DELETE - Remover documentos

### Remover um documento

`deleteOne()` remove apenas o primeiro documento que corresponder ao filtro.

```javascript
db.produtos.deleteOne({ nome: "Livro MongoDB na Pratica" })
```

### Remover varios documentos

`deleteMany()` remove todos os documentos que atenderem a condicao.

```javascript
db.produtos.deleteMany({ categoria: "Roupas" })
```

### Remover todos os documentos da colecao

Com filtro vazio `{}`, todos os documentos da colecao sao removidos.

```javascript
db.produtos.deleteMany({})
```

## INDEX - Criar indices

### Criar indice simples

`createIndex({ nome: 1 })` cria um indice crescente no campo `nome`, melhorando consultas por esse campo.

```javascript
db.produtos.createIndex({ nome: 1 })
```

### Criar indice composto

O indice composto usa mais de um campo e ajuda consultas que combinam esses campos.

```javascript
db.produtos.createIndex({ categoria: 1, preco: -1 })
```

### Listar indices

`getIndexes()` mostra todos os indices criados na colecao.

```javascript
db.produtos.getIndexes()
```

### Remover indice pelo nome

`dropIndex()` remove um indice especifico pelo nome gerado ou definido.

```javascript
db.produtos.dropIndex("nome_1")
```

## Comandos extras uteis

### Ver estrutura de um documento

Este comando ajuda a visualizar como os dados estao organizados dentro da colecao.

```javascript
db.produtos.findOne()
```

### Apagar a colecao inteira

`drop()` remove a colecao completa, incluindo documentos e indices.

```javascript
db.produtos.drop()
```

### Apagar o banco atual

`db.dropDatabase()` remove todo o banco de dados atualmente selecionado.

```javascript
db.dropDatabase()
```
