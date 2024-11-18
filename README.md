# Usuarios.App

**Usuarios.App** é um sistema desenvolvido em **C# .NET** que implementa autenticação e criação de usuários, com autenticação baseada em **JWT (JSON Web Token)** e persistência de dados utilizando **Entity Framework (EF)** com **SQL Server**. O projeto segue os princípios de **SOLID** e foi desenvolvido com foco em **TDD (Test-Driven Development)**. 

## Tecnologias Utilizadas

- **C# .NET 8**
- **Entity Framework Core (EF Core)** para acesso a dados
- **SQL Server** como banco de dados
- **JWT (JSON Web Token)** para autenticação
- **xUnit** para testes unitários e de integração
- **Princípios de SOLID**

## Funcionalidades

### Endpoints Disponíveis

1. **Criar Usuário**  
   Endpoint para cadastrar um novo usuário.
   - **Rota**: `/usuarios/criar`
   - **Método**: `POST`
   - **Corpo da Requisição**:
     ```json
     {
       "nome": "string",
       "email": "string",
       "senha": "string"
     }
     ```
   - **Resposta (sucesso)**:
     ```json
     {
       "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
       "nome": "string",
       "email": "string",
       "dataHoraCadastro": "2024-11-18T22:35:36.792Z",
       "perfil": {
         "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
         "nome": "string"
       }
     }
     ```

2. **Autenticar Usuário**  
   Endpoint para autenticar um usuário e retornar um token JWT.
   - **Rota**: `/usuarios/autenticar`
   - **Método**: `POST`
   - **Corpo da Requisição**:
     ```json
     {
       "email": "string",
       "senha": "string"
     }
     ```
   - **Resposta (sucesso)**:
     ```json
     {
       "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
       "nome": "string",
       "email": "string",
       "perfil": {
         "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
         "nome": "string"
       },
       "dataHoraAcesso": "2024-11-18T22:40:29.026Z",
       "dataHoraExpiracao": "2024-11-18T22:40:29.026Z",
       "accessToken": "string"
     }
     ```

### Autenticação JWT
- Autenticação baseada em **JWT**, com suporte a perfis de usuário (`Admin`, `Usuário`, etc.).
- Tokens possuem expiração configurável.

## Estrutura do Projeto

- **Controllers**: Gerenciam as rotas e chamam os serviços.
- **Services**: Implementam as regras de negócio.
- **Repositories**: Realizam o acesso aos dados.
- **Models**: Incluem as entidades e DTOs utilizados no sistema.
- **Tests**: Contêm os testes unitários e de integração desenvolvidos com **xUnit**.

## Configuração do Banco de Dados

O projeto utiliza **Entity Framework Core (EF Core)** para gerenciar a persistência de dados. Certifique-se de que o SQL Server está configurado e siga os passos abaixo:

1. **Configurar a String de Conexão**  
   A string de conexão está localizada na classe `DataContext` dentro do diretório `Contexts`. Edite o método `OnConfiguring` para definir a sua string de conexão com o banco de dados. Exemplo:
   ```csharp
   protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
   {
       optionsBuilder.UseSqlServer("Server=seu_servidor;Database=UsuariosDB;User Id=seu_usuario;Password=sua_senha;");
   }

2.**Criar o Banco de Dados e Aplicar Migrações
Após configurar a string de conexão e definir o projeto correto de inicialização, siga os passos abaixo

Aplique as migrações ao banco de dados:

Update-Database

3.**Inserir Perfis de Usuário
Após a configuração inicial do banco de dados, insira os perfis básicos executando o seguinte script SQL:

## Inserir Perfis de Usuário

O script para inserir os perfis de usuário (`OPERADOR` e `ADMINISTRADOR`) já está incluído nos arquivos do projeto e foi versionado no Git. Para rodar esse script diretamente no banco de dados, basta acessar o arquivo na pasta `Scripts` do projeto e executá-lo no seu SQL Server.

**Script SQL para carga de dados na tabela de perfil:**
```sql
-- SCRIPT PARA CARGA DE DADOS NA TABELA DE PERFIL
INSERT INTO TB_PERFIL(ID, NOME)
    VALUES
        (NEWID(), 'OPERADOR'),
        (NEWID(), 'ADMINISTRADOR');
GO

SELECT * FROM TB_PERFIL;



