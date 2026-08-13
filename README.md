# Agendador de Horarios

Este e um projeto de API REST desenvolvido em Java 21 utilizando o ecossistema Spring Boot. O objetivo principal do projeto e gerenciar o agendamento de servicos com profissionais, permitindo a criacao, consulta diaria, atualizacao e remocao de agendamentos.

O projeto foi construido como parte de estudos praticos em desenvolvimento Java moderno, com persistencia em banco de dados em memoria e boas praticas de estruturacao de codigo.

---

## Tecnologias Utilizadas

- Java 21: Versao mais recente com suporte de longo prazo (LTS).
- Spring Boot 4.x / 3.x: Framework para facilitacao da configuracao e inicializacao do projeto.
- Spring Data JPA: Abstracao de persistencia e integracao com o banco de dados.
- H2 Database: Banco de dados relacional em memoria para desenvolvimento agil e testes.
- Lombok: Biblioteca para reducao de codigo boilerplate (como getters, setters e construtores).
- Maven: Gerenciador de dependencias e build do projeto.

---

## Estrutura do Projeto

O codigo esta estruturado seguindo os conceitos classicos de arquitetura MVC/Service-Repository:

- `infrastructure/entity`: Contem a classe `Agendamento`, que mapeia a tabela no banco de dados.
- `infrastructure/repository`: Contem a interface `AgendamentoRepository` que estende `JpaRepository`.
- `services`: Contem a classe `AgendamentoService`, responsavel pelas regras de negocio (como validacao de choque de horarios).
- `controller`: Contem a classe `AgendamentoController`, que expoe os endpoints HTTP da API REST.

---

## Endpoints da API

A API expoe o recurso `/agendamentos` com os seguintes metodos HTTP:

### 1. Criar Agendamento
- Metodo: `POST`
- Caminho: `/agendamentos`
- Corpo da Requisicao (JSON):
  ```json
  {
    "servico": "Corte de Cabelo",
    "profissional": "Carlos Henrique",
    "dataHoraAgendamento": "2026-08-15T14:00:00",
    "cliente": "Maria Eduarda",
    "telefoneCliente": "11999999999"
  }
  ```

### 2. Buscar Agendamentos por Dia
- Metodo: `GET`
- Caminho: `/agendamentos`
- Query Params:
  - `data` (Formato: `YYYY-MM-DD`, ex: `2026-08-15`)

### 3. Alterar Agendamento
- Metodo: `PUT`
- Caminho: `/agendamentos`
- Query Params:
  - `cliente` (Nome do cliente cadastrado)
  - `dataHoraAgendamento` (Data e hora atuais do agendamento, ex: `2026-08-15T14:00:00`)
- Corpo da Requisicao (JSON): Dados atualizados do agendamento.

### 4. Deletar Agendamento
- Metodo: `DELETE`
- Caminho: `/agendamentos`
- Query Params:
  - `cliente` (Nome do cliente)
  - `dataHoraAgendamento` (Data e hora do agendamento a ser cancelado)

---

## Banco de Dados & Console H2

Durante a execucao da aplicacao, o banco de dados H2 fica disponivel em memoria.
- URL do H2 Console: `http://localhost:8080/h2-console`
- JDBC URL: `jdbc:h2:mem:agendamentos-db`
- Usuario (sa): `sa`
- Senha: *(em branco)*

---

## Como Executar o Projeto

1. Certifique-se de ter o JDK 21 instalado em sua maquina.
2. Clone o repositorio.
3. Navegue ate a pasta do projeto:
   ```bash
   cd agendador-horarios
   ```
4. Execute a aplicacao com o Maven Wrapper:
   - No Windows:
     ```cmd
     mvnw.cmd spring-boot:run
     ```
   - No Linux/macOS:
     ```bash
     ./mvnw spring-boot:run
     ```
5. A API estara disponivel em `http://localhost:8080`.
