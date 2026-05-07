db.cursos.insertOne({
  nome: "Curso de Desenvolvimento Web",
  categoria: "Tecnologia",
  modulos: [
    {
      nome: "HTML e CSS",
      carga_horaria: 20
    },
    {
      nome: "JavaScript",
      carga_horaria: 30
    },
    {
      nome: "MongoDB",
      carga_horaria: 25
    }
  ]
})