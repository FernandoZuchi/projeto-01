# Documento de Requisitos do Sistema de Gerenciamento de Projetos

Esta documentação tem como objetivo detalhar os requisitos para o desenvolvimento de um Sistema de Gerenciamento de Projetos. Este sistema será usado para gerenciar projetos, tarefas, e membros da equipe, facilitando a comunicação e o acompanhamento do progresso.

## Estrutura do Projeto 

```
- 📂gerenciamento-projetos
  - 📂backend
    - Container(Caso utilize)
  - 📂frontend
    - Container(Caso utilize)
```

- 📂**gerenciamento-projetos**: Pasta raiz do projeto.
- 📂**backend**: Contém o código relacionado ao servidor (API RESTful).
- 📂**frontend**: Contém o código da interface do usuário.

## Banco de dados 

Abaixo está a estrutura da base de dados do projeto:

Projetos:
```
id: integer
nome: varchar
descricao: text
data_inicio: date
data_fim: date
status: varchar (ex: 'Em andamento', 'Concluído', 'Pendente')
```

Tarefas:
```
id: integer
projeto_id: fk (projetos)
nome: varchar
descricao: text
data_inicio: date
data_fim: date
status: varchar (ex: 'Em andamento', 'Concluída', 'Pendente')
responsavel_id: fk (usuarios)
```

Usuários:
```
id: integer
nome: varchar
email: varchar
senha: varchar
papel: varchar (ex: 'Gerente', 'Desenvolvedor')
```

# **Backend** 

O backend será responsável por fornecer uma API RESTful que permitirá a interação com os dados do sistema. A API terá endpoints para realizar operações CRUD (Create, Read, Update, Delete) em projetos, tarefas e usuários

# **Estrutura do Backend**

Diretório backend: Contém o código do servidor.
Container (opcional): Para facilitar a execução e o isolamento do ambiente.

## Endpoints da API 

Esperamos os seguintes endpoints da API para este primeiro projeto: 

### **Projetos**

- **Listar projetos (GET):** `/api/projetos`

  - **Resposta de Sucesso (200):** Retorna um array com os projetos.

  ```json
  [
    {
      "id": 1,
      "nome": "Nome do Projeto",
      "descricao": "Descrição do Projeto",
      "data_inicio": "2024-01-01",
      "data_fim": "2024-12-31",
      "status": "Em andamento"
    },
  ]
  ```

  - **Resposta de Erro (404):** Retorna uma mensagem indicando que nenhum projeto foi encontrado..
 
    

- **Cadastrar Projeto (POST):** `/api/projetos`

  - **Corpo da Requisição:**

  ```json
  {
    "nome": "Nome do Projeto",
    "descricao": "Descrição do Projeto",
    "data_inicio": "2024-12-31",
    "status": "Em andamento"
  }
  ```

  - **Resposta de Sucesso (201):** Retorna o novo projeto criado.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto.
 
    

- **Editar Projeto (PUT/PATCH):** `/api/projetos/:id`

  - **Corpo da Requisição:**

  ```json
  {
    "nome": "Novo Nome do Projeto",
    "descricao": "Nova Descrição do Projeto",
    "data_inicio": "2024-01-01",
    "data_fim": "2024-12-31",
    "status": "Concluído"
  }
  ```

  - **Resposta de Sucesso (200):** Retorna o projeto atualizado.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto.

- **Remover Projeto (DELETE):** `/api/projetos/:id`
  - **Resposta de Sucesso (204):** Confirma que o projeto foi removido com sucesso. Não retorna corpo..
  - **Resposta de Erro (400):** Retorna uma mensagem indicando problemas na remoção.
 
    

### **Tarefas**

- **Listar Tarefas (GET):** `/api/tarefas`

  - **Resposta de Sucesso (200):** Retorna um array com as tarefas.

  ```json
  [
    {
      "id": 1,
      "projeto_id": 1,
      "nome": "Nome da Tarefa",
      "descricao": "Descrição da Tarefa",
      "data_inicio": "2024-01-01",
      "data_fim": "2024-01-31",
      "status": "Em andamento",
      "responsavel_id": 1
    },
    ...
  ]
  ```

  - **Resposta de Erro (404):** Retorna uma mensagem indicando que nenhuma tarefa foi encontrada..
 
    

- **Cadastrar Tarefa (POST):** `/api/tarefas`

  - **Corpo da Requisição:**

  ```json
  {
    "projeto_id": 1,
    "nome": "Nome da Tarefa",
    "descricao": "Descrição da Tarefa",
    "data_inicio": "2024-01-01",
    "data_fim": "2024-01-31",
    "status": "Em andamento",
    "responsavel_id": 1
  }
  ```

  - **Resposta de Sucesso (201):** Retorna a tarefa criada..
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto..
 
    

- **Editar Tarefa (PUT/PATCH):** `/api/tarefas/:id`

  - **Corpo da Requisição:**

  ```json
  {
    "nome": "Novo Nome da Tarefa",
    "descricao": "Nova Descrição da Tarefa",
    "data_inicio": "2024-01-01",
    "data_fim": "2024-01-31",
    "status": "Concluída",
    "responsavel_id": 2
  }
  ```

  - **Resposta de Sucesso (200):** Retorna a tarefa atualizada.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto.
 
    

- **Remover Tarefa (DELETE):** `/api/tarefa/:id`
  - **Resposta de Sucesso (204):** Confirma que a tarefa foi removida com sucesso.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando problemas na remoção..
 
    


### **Usuários**

- **Listar Tarefas (GET):** `/api/usuarios`

  - **Resposta de Sucesso (200):** Retorna um array com os usuários.

  ```json
  [
    {
      "id": 1,
      "nome": "Nome do Usuário",
      "email": "email@exemplo.com",
      "papel": "Desenvolvedor"
    },
    ...
  ]
  ```

  - **Resposta de Erro (404):** Retorna uma mensagem indicando que nenhum usuário foi encontrado.
 
    

- **Cadastrar Usuário (POST):** `/api/usuarios`

  - **Corpo da Requisição:**

  ```json
  {
    "nome": "Nome do Usuário",
    "email": "email@exemplo.com",
    "senha": "senha123",
    "papel": "Desenvolvedor"
  }
  ```

  - **Resposta de Sucesso (201):** Retorna o usuário criado.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto.
    
    

- **Editar Usuário (PUT/PATCH):** `/api/usuarios/:id`

  - **Corpo da Requisição:**

  ```json
  {
    "nome": "Novo Nome do Usuário",
    "email": "novoemail@exemplo.com",
    "senha": "novasenha123",
    "papel": "Gerente”
  }
  ```

  - **Resposta de Sucesso (200):** Retorna o usuário atualizado.
  - **Resposta de Erro (400):** Retorna uma mensagem indicando que o corpo da requisição está incorreto.
    

    
- **Remover Usuário (DELETE):** `/api/usuarios/:id`
  - **Resposta de Sucesso (204):** Confirma que o usuário foi removido com sucesso
  - **Resposta de Erro (400):** Retorna uma mensagem indicando problemas na remoção.



# **Frontend** 

O frontend será uma SPA (Single Page Application) que interage com a API para fornecer uma interface de usuário intuitiva. A aplicação permitirá visualizar, adicionar, editar e remover projetos, tarefas e usuários.

## **Páginas:**

  - **Projetos**:
    - Listagem: Tabela com os projetos cadastrados, com opções de adicionar, editar e remover.
    - Cadastro/Edição: Formulário para cadastro ou edição de projetos, pode ser uma modal ou uma página separada.
    - Exclusão: Confirmação antes de excluir um projeto.


  - **Tarefas**:
    - Listagem: Tabela com as tarefas cadastradas, com opções de adicionar, editar e remover.
    - Cadastro/Edição: Formulário para cadastro ou edição de tarefas, pode ser uma modal ou uma página separada.
    - Exclusão: Confirmação antes de excluir uma tarefa.
   
  - **Usuários**:
    - Listagem: Tabela com os usuários cadastrados, com opções de adicionar, editar e remover.
    - Cadastro/Edição: Formulário para cadastro ou edição de usuários, pode ser uma modal ou uma página separada.
    - Exclusão: Confirmação antes de excluir um usuário.




## O que será avaliado? 

No geral, tudo será avaliado. Porém nosso foco é descobrir como você aplica os conceitos da programação nos seus projetos, como você soluciona problemas e como irá gerar valor ao produto desenvolvido.

Estamos de olho em: 🔎

- Estrutura do Código: Organização e clareza do código.
- Cumprimento de Requisitos: Atendimento aos requisitos especificados.
- Lógica de Programação: Soluções implementadas e sua eficiência.
- Metodologia Aplicada: Abordagem para resolver problemas e entregar valor.
- Documentação: Qualidade e clareza da documentação fornecida.


## Checklist 📝

Abaixo estão as implementações que terão de ser feitas no seu projeto. Quanto mais itens você entregar, melhor será sua avaliação. Utilize este checklist como um guia e faça os itens que conseguir.

Os itens estão separados por níveis, e o nível 1 é o mínimo que esperamos que vocês entreguem

---

**Legenda:**

- B -> Backend
- F -> Frontend

---

### Nível 1

|     | Descrição                  | Local |
| --- | -------------------------- | ----- |
| [ ] | Listar projetos            |  F B  |
| [ ] | Cadastrar um projeto       |  F B  |
| [ ] | Editar um projeto          |  F B  |
| [ ] | Remover um projeto         |  F B  |
| [ ] | Listar tarefas             |  F B  |
| [ ] | Cadastrar uma tarefa       |  F B  |
| [ ] | Editar uma tarefa          |  F B  |
| [ ] | Remover uma tarefa         |  F B  |
| [ ] | Listar usuários            |  F B  |
| [ ] | Cadastrar um usuário       |  F B  |
| [ ] | Editar um usuário          |  F B  |
| [ ] | Remover um usuário         |  F B  |


### Nível 2

|     | Descrição	                                            | Local |
| --- | ------------------------------------------------      | ----- |
| [ ] | Impedir remoção de projeto com tarefas associadas	    |   B   
| [ ] | Adicionar busca via query para a listagem de projetos	|  F B  |
| [ ] | Adicionar busca via query para a listagem de tarefas	|  F B  |
| [ ] | Adicionar busca via query para a listagem de usuários	|  F B  |
| [ ] |	Tratamento de exceções / Retornos erros concisos	    |  F B  |
| [ ] | Paginação na listagem de projetos	                    |  F B  |
| [ ] | Paginação na listagem de tarefas	                    |  F B  |
| [ ] | Paginação na listagem de usuários	                    |  F B  |
| [ ] | Mensagens de sucesso e/ou erros	                      |  F   |
| [ ] | Confirmação para exclusão de itens	                  |  F   |
| [ ] | Ordenação das tabelas clicando no nome da coluna	    |   B  |
| [ ] | Validações de campos	                                |  F B  |
| [ ] | Na página de projetos, adicionar uma coluna com a qtde de tarefas associadas |  F   |

### Nível 3

|     | Descrição                              | Local |
| --- | -------------------------------------- | ----- |
| [ ] | Tipagem de dados                       |  F B  |
| [ ] | Organização e estrutura de pastas      |  F B  |
| [ ] | Clean Code                             |  F B  |
| [ ] | Testes unitários                       |  F B  |
| [ ] | Documentação/Apresentação do Código    |  F B  |

### Nível 4

|     | Descrição                                                               | Local |
| --- | ----------------------------------------------------------------------- | ----- |
| [ ] | Disponibilização do backend via Containers                              |    B  |
| [ ] | Disponibilização do frontend via Containers                             |  F    |
| [ ] | Disponibilização dos containers (backend + frontend)                    |  F B  |



