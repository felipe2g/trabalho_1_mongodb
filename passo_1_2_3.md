Criação da coleção Task

```
db.createCollection("Task", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: ["title", "description", "start_date", "deadline_date", "priority", "status"],
         properties: {
            title: {
               bsonType: "string",
               description: "Título da tarefa é obrigatório e deve ser uma string."
            },
            description: {
               bsonType: "string",
               description: "Descrição da tarefa é obrigatória e deve ser uma string."
            },
            start_date: {
               bsonType: "date",
               description: "Data de início da tarefa é obrigatória e deve ser uma data."
            },
            deadline_date: {
               bsonType: "date",
               description: "Data de prazo da tarefa é obrigatória e deve ser uma data."
            },
            priority: {
               bsonType: "string",
               description: "Prioridade da tarefa é obrigatória e deve ser uma string."
            },
            status: {
               bsonType: "string",
               description: "Status da tarefa é obrigatório e deve ser uma string."
            }
         }
      }
   }
})
```

Criação da coleção Project

```
db.createCollection("Project", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: ["name", "start_date", "end_date"],
         properties: {
            name: {
               bsonType: "string",
               description: "Nome do projeto é obrigatório e deve ser uma string."
            },
            start_date: {
               bsonType: "date",
               description: "Data de início do projeto é obrigatória e deve ser uma data."
            },
            end_date: {
               bsonType: "date",
               description: "Data de término do projeto é obrigatória e deve ser uma data."
            }
         }
      }
   }
})

```

Criação da coleção User

```
db.createCollection("User", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: ["first_name", "last_name", "email", "cell_phone"],
         properties: {
            first_name: {
               bsonType: "string",
               description: "Primeiro nome do usuário é obrigatório e deve ser uma string."
            },
            last_name: {
               bsonType: "string",
               description: "Sobrenome do usuário é obrigatório e deve ser uma string."
            },
            email: {
               bsonType: "string",
               pattern: "^\\S+@\\S+\\.\\S+$",
               description: "E-mail do usuário é obrigatório e deve ser um e-mail válido."
            },
            cell_phone: {
               bsonType: "string",
               description: "Número de celular do usuário é obrigatório e deve ser uma string."
            }
         }
      }
   }
})
```

Relacionamento one-to-many entre Project e Task

```
db.Project.updateMany({}, { $set: { tasks: [] } })
```

Relacionamento one-to-one entre Task e User

```
db.Task.updateMany({}, { $set: { assigned_to: null } })
```

Exemplo de JSON

```json
{
   "_id":"ObjectId(""project_id_here"")",
   "name":"Projeto de Desenvolvimento Web",
   "start_date":"ISODate(""2023-10-15T00:00:00Z"")",
   "end_date":"ISODate(""2023-12-31T23:59:59Z"")",
   "tasks":[
      {
         "_id":"ObjectId(""task_id_1"")",
         "title":"Realizar reunião de equipe 1",
         "description":"Reunião semanal de equipe para discutir andamento dos projetos 1",
         "start_date":"ISODate(""2023-11-01T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-01T10:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_1"")",
            "first_name":"João",
            "last_name":"Silva",
            "email":"joao.silva1@email.com",
            "cell_phone":"+55 11 9999-9999"
         }
      },
      {
         "_id":"ObjectId(""task_id_2"")",
         "title":"Realizar reunião de equipe 2",
         "description":"Reunião semanal de equipe para discutir andamento dos projetos 2",
         "start_date":"ISODate(""2023-11-01T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-01T10:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_2"")",
            "first_name":"Maria",
            "last_name":"Ferreira",
            "email":"maria.ferreira2@email.com",
            "cell_phone":"+55 11 8888-8888"
         }
      },
      {
         "_id":"ObjectId(""task_id_3"")",
         "title":"Desenvolver novo recurso",
         "description":"Desenvolver um novo recurso para o aplicativo móvel",
         "start_date":"ISODate(""2023-11-02T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-02T14:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_3"")",
            "first_name":"Ana",
            "last_name":"Martins",
            "email":"ana.martins@email.com",
            "cell_phone":"+55 11 7777-7777"
         }
      },
      {
         "_id":"ObjectId(""task_id_4"")",
         "title":"Revisar documento de projeto",
         "description":"Revisar e atualizar o documento de projeto para a apresentação",
         "start_date":"ISODate(""2023-11-03T13:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-03T16:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_4"")",
            "first_name":"Pedro",
            "last_name":"Santos",
            "email":"pedro.santos@email.com",
            "cell_phone":"+55 11 6666-6666"
         }
      },
      {
         "_id":"ObjectId(""task_id_5"")",
         "title":"Testar nova funcionalidade",
         "description":"Realizar testes de qualidade na nova funcionalidade do software",
         "start_date":"ISODate(""2023-11-04T14:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-04T16:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_5"")",
            "first_name":"Carla",
            "last_name":"Oliveira",
            "email":"carla.oliveira@email.com",
            "cell_phone":"+55 11 5555-5555"
         }
      },
      {
         "_id":"ObjectId(""task_id_6"")",
         "title":"Preparar apresentação de vendas",
         "description":"Preparar uma apresentação para a reunião de vendas",
         "start_date":"ISODate(""2023-11-05T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-05T12:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_6"")",
            "first_name":"Lucas",
            "last_name":"Pereira",
            "email":"lucas.pereira@email.com",
            "cell_phone":"+55 11 4444-4444"
         }
      },
      {
         "_id":"ObjectId(""task_id_7"")",
         "title":"Testar aplicativo em dispositivos móveis",
         "description":"Realizar testes em diversos dispositivos móveis",
         "start_date":"ISODate(""2023-11-06T14:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-06T16:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_7"")",
            "first_name":"Mariana",
            "last_name":"Ribeiro",
            "email":"mariana.ribeiro@email.com",
            "cell_phone":"+55 11 3333-3333"
         }
      },
      {
         "_id":"ObjectId(""task_id_8"")",
         "title":"Revisar conteúdo do blog",
         "description":"Revisar e publicar novos artigos no blog da empresa",
         "start_date":"ISODate(""2023-11-07T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-07T12:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_8"")",
            "first_name":"Rafael",
            "last_name":"Lima",
            "email":"rafael.lima@email.com",
            "cell_phone":"+55 11 2222-2222"
         }
      },
      {
         "_id":"ObjectId(""task_id_9"")",
         "title":"Entrevistar candidatos para a equipe",
         "description":"Realizar entrevistas para preencher vagas na equipe de desenvolvimento",
         "start_date":"ISODate(""2023-11-08T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-08T17:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_9"")",
            "first_name":"Paula",
            "last_name":"Gonçalves",
            "email":"paula.goncalves@email.com",
            "cell_phone":"+55 11 1111-1111"
         }
      },
      {
         "_id":"ObjectId(""task_id_10"")",
         "title":"Realizar teste de carga no servidor",
         "description":"Executar testes de carga no servidor para avaliar o desempenho",
         "start_date":"ISODate(""2023-11-09T15:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-09T18:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_10"")",
            "first_name":"Gustavo",
            "last_name":"Machado",
            "email":"gustavo.machado@email.com",
            "cell_phone":"+55 11 9999-8888"
         }
      },
      {
         "_id":"ObjectId(""task_id_11"")",
         "title":"Gerar relatório de vendas mensais",
         "description":"Compilar dados e criar um relatório de vendas do mês",
         "start_date":"ISODate(""2023-11-10T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-10T14:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_11"")",
            "first_name":"Carolina",
            "last_name":"Sousa",
            "email":"carolina.sousa@email.com",
            "cell_phone":"+55 11 7777-8888"
         }
      },
      {
         "_id":"ObjectId(""task_id_12"")",
         "title":"Atualizar site da empresa",
         "description":"Realizar atualizações no site da empresa, incluindo novos conteúdos",
         "start_date":"ISODate(""2023-11-11T11:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-11T15:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_12"")",
            "first_name":"André",
            "last_name":"Rocha",
            "email":"andre.rocha@email.com",
            "cell_phone":"+55 11 3333-4444"
         }
      },
      {
         "_id":"ObjectId(""task_id_13"")",
         "title":"Realizar treinamento de equipe",
         "description":"Conduzir um treinamento para a equipe de suporte técnico",
         "start_date":"ISODate(""2023-11-12T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-12T12:00:00Z"")",
         "priority":"Baixa",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_13"")",
            "first_name":"Lucia",
            "last_name":"Gomes",
            "email":"lucia.gomes@email.com",
            "cell_phone":"+55 11 5555-4444"
         }
      },
      {
         "_id":"ObjectId(""task_id_14"")",
         "title":"Avaliar propostas de fornecedores",
         "description":"Avaliar e comparar propostas de fornecedores para seleção",
         "start_date":"ISODate(""2023-11-13T13:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-13T16:00:00Z"")",
         "priority":"Alta",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_14"")",
            "first_name":"Eduardo",
            "last_name":"Mendes",
            "email":"eduardo.mendes@email.com",
            "cell_phone":"+55 11 6666-5555"
         }
      },
      {
         "_id":"ObjectId(""task_id_15"")",
         "title":"Desenvolver protótipo de interface",
         "description":"Criar um protótipo de interface para um novo aplicativo",
         "start_date":"ISODate(""2023-11-14T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-14T13:00:00Z"")",
         "priority":"Alta",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_15"")",
            "first_name":"Luis",
            "last_name":"Costa",
            "email":"luis.costa@email.com",
            "cell_phone":"+55 11 7777-6666"
         }
      },
      {
         "_id":"ObjectId(""task_id_16"")",
         "title":"Gerenciar redes sociais",
         "description":"Agendar postagens e interagir com seguidores nas redes sociais",
         "start_date":"ISODate(""2023-11-15T13:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-15T16:00:00Z"")",
         "priority":"Baixa",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_16"")",
            "first_name":"Camila",
            "last_name":"Ramos",
            "email":"camila.ramos@email.com",
            "cell_phone":"+55 11 5555-6666"
         }
      },
      {
         "_id":"ObjectId(""task_id_17"")",
         "title":"Realizar manutenção de servidores",
         "description":"Realizar atualizações e manutenção nos servidores da empresa",
         "start_date":"ISODate(""2023-11-16T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-16T12:00:00Z"")",
         "priority":"Média",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_17"")",
            "first_name":"Daniel",
            "last_name":"Almeida",
            "email":"daniel.almeida@email.com",
            "cell_phone":"+55 11 4444-5555"
         }
      },
      {
         "_id":"ObjectId(""task_id_18"")",
         "title":"Elaborar relatório de desempenho",
         "description":"Preparar um relatório mensal de desempenho da equipe de vendas",
         "start_date":"ISODate(""2023-11-17T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-17T14:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_18"")",
            "first_name":"Fernanda",
            "last_name":"Rodrigues",
            "email":"fernanda.rodrigues@email.com",
            "cell_phone":"+55 11 3333-5555"
         }
      },
      {
         "_id":"ObjectId(""task_id_19"")",
         "title":"Implementar novos recursos no aplicativo",
         "description":"Desenvolver e implementar novos recursos no aplicativo móvel",
         "start_date":"ISODate(""2023-11-18T14:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-18T17:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_19"")",
            "first_name":"Miguel",
            "last_name":"Santos",
            "email":"miguel.santos@email.com",
            "cell_phone":"+55 11 7777-5555"
         }
      },
      {
         "_id":"ObjectId(""task_id_20"")",
         "title":"Realizar testes de segurança",
         "description":"Conduzir testes de segurança em sistemas da empresa",
         "start_date":"ISODate(""2023-11-19T11:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-19T13:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_20"")",
            "first_name":"Cláudia",
            "last_name":"Ferreira",
            "email":"claudia.ferreira@email.com",
            "cell_phone":"+55 11 6666-7777"
         }
      },
      {
         "_id":"ObjectId(""task_id_21"")",
         "title":"Realizar pesquisa de mercado",
         "description":"Conduzir uma pesquisa de mercado para avaliar a concorrência",
         "start_date":"ISODate(""2023-11-20T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-20T13:00:00Z"")",
         "priority":"Alta",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_21"")",
            "first_name":"Isabela",
            "last_name":"Pereira",
            "email":"isabela.pereira@email.com",
            "cell_phone":"+55 11 1111-2222"
         }
      },
      {
         "_id":"ObjectId(""task_id_22"")",
         "title":"Atualizar manual do usuário",
         "description":"Revisar e atualizar o manual do usuário para o novo software",
         "start_date":"ISODate(""2023-11-21T14:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-21T17:00:00Z"")",
         "priority":"Média",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_22"")",
            "first_name":"Carlos",
            "last_name":"Sousa",
            "email":"carlos.sousa@email.com",
            "cell_phone":"+55 11 5555-7777"
         }
      },
      {
         "_id":"ObjectId(""task_id_23"")",
         "title":"Realizar manutenção de hardware",
         "description":"Realizar manutenção e atualizações nos computadores da empresa",
         "start_date":"ISODate(""2023-11-22T11:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-22T14:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_23"")",
            "first_name":"Patrícia",
            "last_name":"Lima",
            "email":"patricia.lima@email.com",
            "cell_phone":"+55 11 4444-6666"
         }
      },
      {
         "_id":"ObjectId(""task_id_24"")",
         "title":"Realizar treinamento de segurança",
         "description":"Ministrar treinamento de segurança para os funcionários",
         "start_date":"ISODate(""2023-11-23T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-23T12:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_24"")",
            "first_name":"Roberto",
            "last_name":"Alves",
            "email":"roberto.alves@email.com",
            "cell_phone":"+55 11 7777-2222"
         }
      },
      {
         "_id":"ObjectId(""task_id_25"")",
         "title":"Analisar feedback de clientes",
         "description":"Avaliar feedback de clientes e propor melhorias",
         "start_date":"ISODate(""2023-11-24T13:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-24T16:00:00Z"")",
         "priority":"Alta",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_25"")",
            "first_name":"Sofia",
            "last_name":"Fernandes",
            "email":"sofia.fernandes@email.com",
            "cell_phone":"+55 11 5555-2222"
         }
      },
      {
         "_id":"ObjectId(""task_id_26"")",
         "title":"Realizar auditoria financeira",
         "description":"Conduzir uma auditoria financeira na empresa",
         "start_date":"ISODate(""2023-11-25T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-25T14:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_26"")",
            "first_name":"Felipe",
            "last_name":"Pereira",
            "email":"felipe.pereira@email.com",
            "cell_phone":"+55 11 4444-2222"
         }
      },
      {
         "_id":"ObjectId(""task_id_27"")",
         "title":"Desenvolver plano de marketing",
         "description":"Criar um plano de marketing para promover um novo produto",
         "start_date":"ISODate(""2023-11-26T11:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-26T14:00:00Z"")",
         "priority":"Alta",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_27"")",
            "first_name":"Vanessa",
            "last_name":"Rocha",
            "email":"vanessa.rocha@email.com",
            "cell_phone":"+55 11 1111-3333"
         }
      },
      {
         "_id":"ObjectId(""task_id_28"")",
         "title":"Conduzir reunião de planejamento",
         "description":"Realizar reunião de planejamento estratégico com a equipe",
         "start_date":"ISODate(""2023-11-27T14:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-27T16:00:00Z"")",
         "priority":"Média",
         "status":"Pendente",
         "assigned_to":{
            "_id":"ObjectId(""user_id_28"")",
            "first_name":"Guilherme",
            "last_name":"Melo",
            "email":"guilherme.melo@email.com",
            "cell_phone":"+55 11 5555-3333"
         }
      },
      {
         "_id":"ObjectId(""task_id_29"")",
         "title":"Realizar inspeção de qualidade",
         "description":"Realizar inspeção de qualidade nos produtos antes do envio",
         "start_date":"ISODate(""2023-11-28T09:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-28T12:00:00Z"")",
         "priority":"Baixa",
         "status":"Concluída",
         "assigned_to":{
            "_id":"ObjectId(""user_id_29"")",
            "first_name":"Marcelo",
            "last_name":"Costa",
            "email":"marcelo.costa@email.com",
            "cell_phone":"+55 11 4444-3333"
         }
      },
      {
         "_id":"ObjectId(""task_id_30"")",
         "title":"Realizar análise de dados",
         "description":"Coletar, analisar e apresentar dados de desempenho da empresa",
         "start_date":"ISODate(""2023-11-29T10:00:00Z"")",
         "deadline_date":"ISODate(""2023-11-29T13:00:00Z"")",
         "priority":"Média",
         "status":"Em andamento",
         "assigned_to":{
            "_id":"ObjectId(""user_id_30"")",
            "first_name":"Raquel",
            "last_name":"Santos",
            "email":"raquel.santos@email.com",
            "cell_phone":"+55 11 7777-3333"
         }
      }
   ]
}

```
