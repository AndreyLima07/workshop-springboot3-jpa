# 🛒 E-commerce Web Services API

Uma API REST completa desenvolvida com **Spring Boot 3** e **JPA/Hibernate** para gerenciamento de um sistema de e-commerce, incluindo usuários, produtos, categorias e pedidos.

## 📋 Sobre o Projeto

Este projeto foi desenvolvido como parte do curso Java COMPLETO do Prof. Dr. Nelio Alves, implementando uma API robusta para um sistema de e-commerce com todas as funcionalidades CRUD e tratamento de exceções.

## 🚀 Funcionalidades

- ✅ **Gestão de Usuários** - CRUD completo com validações
- ✅ **Catálogo de Produtos** - Organização por categorias
- ✅ **Sistema de Pedidos** - Controle de status e itens
- ✅ **Processamento de Pagamentos** - Integração com sistema de pagamento
- ✅ **Tratamento de Exceções** - Respostas padronizadas para erros
- ✅ **Banco de Dados** - Suporte para H2 (desenvolvimento) com configuração para PostgreSQL

## 🛠️ Tecnologias Utilizadas

### Backend

- **Java 17** - Linguagem de programação
- **Spring Boot 3** - Framework principal
- **Spring Data JPA** - Abstração para acesso a dados
- **Hibernate** - ORM (Object-Relational Mapping)
- **Maven** - Gerenciamento de dependências

### Banco de Dados

- **H2 Database** - Banco em memória para desenvolvimento e testes
- **PostgreSQL** - Compatível para ambiente de produção

### Ambiente

- **Desenvolvimento Local** - Configuração otimizada para estudo e testes

## 📊 Modelo de Domínio

```
User ←→ Order ←→ OrderItem ←→ Product ←→ Category
         ↓
      Payment
```

### Entidades Principais

- **User**: Usuários do sistema
- **Order**: Pedidos realizados
- **Product**: Produtos disponíveis
- **Category**: Categorias dos produtos
- **OrderItem**: Itens de cada pedido
- **Payment**: Informações de pagamento

## ⚙️ Configuração do Ambiente

### Pré-requisitos

- Java 17 ou superior
- Maven 3.6+
- IDE de sua preferência (IntelliJ IDEA, Eclipse, VS Code)

### Instalação

1. **Clone o repositório**

```bash
git clone https://github.com/AndreyLima07/workshop-springboot3-jpa.git
cd workshop-springboot3-jpa
```

2. **Configure o banco de dados**

   O projeto utiliza H2 Database por padrão:

   ```properties
   spring.profiles.active=test
   ```

   Para ambiente de produção (PostgreSQL):

   ```properties
   spring.profiles.active=dev
   ```

3. **Execute a aplicação**

```bash
mvn spring-boot:run
```

4. **Acesse a aplicação**
   - API: `http://localhost:8080`
   - Console H2: `http://localhost:8080/h2-console`
     - JDBC URL: `jdbc:h2:mem:testdb`
     - Username: `sa`
     - Password: (deixe em branco)

## 🗄️ Configuração do Banco de Dados

### Perfil de Teste (H2)

```properties
# application-test.properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

### Perfil de Desenvolvimento (PostgreSQL)

```properties
# application-dev.properties
spring.datasource.url=jdbc:postgresql://localhost:5432/springboot_course
spring.datasource.username=postgres
spring.datasource.password=1234567
spring.jpa.hibernate.ddl-auto=update
```

## 📡 API Endpoints

| Método | Endpoint           | Descrição                  |
| ------ | ------------------ | -------------------------- |
| GET    | `/users`           | Listar todos os usuários   |
| GET    | `/users/{id}`      | Buscar usuário por ID      |
| POST   | `/users`           | Criar novo usuário         |
| PUT    | `/users/{id}`      | Atualizar usuário          |
| DELETE | `/users/{id}`      | Deletar usuário            |
| GET    | `/products`        | Listar todos os produtos   |
| GET    | `/products/{id}`   | Buscar produto por ID      |
| GET    | `/categories`      | Listar todas as categorias |
| GET    | `/categories/{id}` | Buscar categoria por ID    |
| GET    | `/orders`          | Listar todos os pedidos    |
| GET    | `/orders/{id}`     | Buscar pedido por ID       |

## 📝 Exemplos de Uso

### Criar Usuário

```json
POST /users
{
  "name": "João Silva",
  "email": "joao@email.com",
  "phone": "11999999999",
  "password": "123456"
}
```

### Atualizar Usuário

```json
PUT /users/1
{
  "name": "João Santos",
  "email": "joao.santos@email.com",
  "phone": "11888888888"
}
```

## 🚨 Tratamento de Exceções

A API implementa um sistema robusto de tratamento de exceções:

- **ResourceNotFoundException** - Recurso não encontrado (404)
- **DatabaseException** - Violação de integridade (400)
- **EntityNotFoundException** - Entidade não encontrada para atualização (404)

Todas as exceções retornam uma resposta padronizada:

```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "status": 404,
  "error": "Resource not found",
  "message": "Entity not found",
  "path": "/users/999"
}
```

## 📂 Estrutura do Projeto

```
src/main/java/
├── entities/          # Entidades JPA
├── repositories/      # Interfaces de acesso a dados
├── services/          # Lógica de negócio
├── resources/         # Controladores REST
├── config/           # Configurações
└── exceptions/       # Tratamento de exceções
```

## 🌐 Execução Local

### Como testar a API

1. **Inicie a aplicação**

```bash
mvn spring-boot:run
```

2. **Acesse o console H2**

   - URL: `http://localhost:8080/h2-console`
   - Veja os dados inseridos automaticamente

3. **Teste os endpoints**
   - Use Postman, Insomnia ou curl
   - Base URL: `http://localhost:8080`

### Exemplo de teste com curl

```bash
# Listar usuários
curl -X GET http://localhost:8080/users

# Buscar usuário por ID
curl -X GET http://localhost:8080/users/1

# Criar novo usuário
curl -X POST http://localhost:8080/users \
  -H "Content-Type: application/json" \
  -d '{"name":"João Silva","email":"joao@email.com","phone":"11999999999","password":"123456"}'
```

## 📈 Próximas Implementações

- [ ] Sistema de autenticação JWT
- [ ] Validações com Bean Validation
- [ ] Paginação e filtros
- [ ] Documentação com Swagger/OpenAPI
- [ ] Testes unitários e de integração
- [ ] Deploy em plataforma gratuita (Railway, Render)
- [ ] Cache com Redis
- [ ] Containerização com Docker

## 👨‍💻 Autor

**Andrey Felipe de Lima**

- GitHub: [@AndreyLima07](https://github.com/AndreyLima07)
- LinkedIn: [Andrey Felipe de Lima](https://www.linkedin.com/in/andrey-felipe-de-lima/)
- Email: andreylima@alunos.utfpr.edu.br

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 🙏 Agradecimentos

- Prof. Dr. Nelio Alves pelo excelente curso
- DevSuperior pela metodologia de ensino
- Comunidade Spring Boot pelas contribuições

---

⭐ **Se este projeto te ajudou, deixe uma estrela!**
