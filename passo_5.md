```
// 1. Alterar o usuário responsável por uma tarefa
db.Task.updateOne(
  { _id: ObjectId("task_id_here") }, // Filtra a tarefa pelo ID
  { $set: { "assigned_to._id": ObjectId("new_user_id_here"), "assigned_to.first_name": "Novo Primeiro Nome" } } // Define o novo usuário responsável
)

// 2. Dilatar o prazo de entrega de uma tarefa
db.Task.updateOne(
  { _id: ObjectId("task_id_here") }, // Filtra a tarefa pelo ID
  { $set: { deadline_date: ISODate("nova_data_aqui") } } // Define a nova data de prazo de entrega
)

// 3. Mudar o status de "In Progress" para "Complete"
db.Task.updateOne(
  { _id: ObjectId("task_id_here"), status: "In Progress" }, // Filtra a tarefa pelo ID e status
  { $set: { status: "Complete" } } // Define o novo status
)

// 4. Alterar a prioridade de uma tarefa
db.Task.updateOne(
  { _id: ObjectId("task_id_here") }, // Filtra a tarefa pelo ID
  { $set: { priority: "Alta" } } // Define a nova prioridade
)

// 5. Adicionar uma nova descrição a uma tarefa
db.Task.updateOne(
  { _id: ObjectId("task_id_here") }, // Filtra a tarefa pelo ID
  { $set: { description: "Nova descrição da tarefa" } } // Define a nova descrição
)

// 6. Mudar o status de "Complete" para "In Progress":
db.Task.updateOne(
  { _id: ObjectId("task_id_here"), status: "Complete" },
  { $set: { status: "In Progress" } }
)

// 7. Aumentar a prioridade de uma tarefa para "Alta":
db.Task.updateOne(
  { _id: ObjectId("task_id_here"), priority: { $ne: "Alta" } },
  { $set: { priority: "Alta" } }
)

// 8. Diminuir a prioridade de uma tarefa para "Baixa":
db.Task.updateOne(
  { _id: ObjectId("task_id_here"), priority: { $ne: "Baixa" } },
  { $set: { priority: "Baixa" } }
)

// 9. Atualizar a data de início de uma tarefa:
db.Task.updateOne(
  { _id: ObjectId("task_id_here") },
  { $set: { start_date: ISODate("nova_data_de_inicio") } }
)

// 10. Atribuir uma tarefa a um usuário diferente:
db.Task.updateOne(
  { _id: ObjectId("task_id_here") },
  { $set: { "assigned_to._id": ObjectId("novo_user_id_aqui") } }
)

// 11. Remover a descrição de uma tarefa:
db.Task.updateOne(
  { _id: ObjectId("task_id_here") },
  { $unset: { description: "" } }
)

// 12. Aumentar a prioridade de todas as tarefas de um projeto:
db.Task.updateMany(
  { project_id: ObjectId("project_id_here"), priority: { $ne: "Alta" } },
  { $set: { priority: "Alta" } }
)

// 13. Marcar todas as tarefas com prazo de entrega vencido como "Atrasadas":
db.Task.updateMany(
  { deadline_date: { $lt: new Date() } },
  { $set: { status: "Atrasadas" } }
)

// 14. Atualizar a data de início de todas as tarefas de um projeto:
db.Task.updateMany(
  { project_id: ObjectId("project_id_here") },
  { $set: { start_date: ISODate("nova_data_de_inicio") } }
)

// 15. Alterar o nome de um projeto:
db.Project.updateOne(
  { _id: ObjectId("project_id_here") },
  { $set: { name: "Novo Nome do Projeto" } }
)
```
