```
// Buscar todos os projetos
db.Project.find({})

// Buscar um projeto específico por nome
db.Project.find({ name: "Nome do Projeto" })

// Buscar todas as tarefas
db.Task.find({})

// Buscar uma tarefa específica por título
db.Task.find({ title: "Título da Tarefa" })

// Buscar todos os usuários
db.User.find({})

// Buscar um usuário específico por email
db.User.find({ email: "email@exemplo.com" })

// Todas as tarefas de um projeto específico
db.Task.find({ project_id: ObjectId("project_id_here") })

// Todas as tarefas de um usuário específico
db.Task.find({ "assigned_to._id": ObjectId("user_id_here") })

// Todas as tarefas com status "To-Do" (a fazer) de um projeto específico
db.Task.find({ project_id: ObjectId("project_id_here"), status: "To-Do" })

// Todas as tarefas com status "To-Do" (a fazer) de um usuário específico
db.Task.find({ "assigned_to._id": ObjectId("user_id_here"), status: "To-Do" })

// Todas as tarefas com prazo de entrega vencido
db.Task.find({ deadline_date: { $lt: new Date() } })

// Buscar todos os projetos em andamento (com data de término no futuro)
db.Project.find({ end_date: { $gte: new Date() } })

// Buscar todas as tarefas com prioridade "Alta" de um projeto específico
db.Task.find({ project_id: ObjectId("project_id_here"), priority: "Alta" })

// Buscar todas as tarefas atribuídas a um usuário específico com status "Concluída"
db.Task.find({ "assigned_to._id": ObjectId("user_id_here"), status: "Concluída" })

// Buscar projetos com um nome que contenha uma palavra-chave
db.Project.find({ name: { $regex: /palavra-chave/i } })

```
