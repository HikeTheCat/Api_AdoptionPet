🐾 Pet Adoption API
API RESTful completa para gerenciamento de adoções de animais de estimação. Desenvolvida com Node.js, Express e MySQL, oferece funcionalidades para usuários, pets e processos de adoção.

🌟 Recursos Principais
Autenticação segura com JWT

Gestão de usuários (adotantes e administradores)

Cadastro e gerenciamento de pets

Processo completo de adoção

Controle de acesso baseado em roles

Validação de dados rigorosa

🛠 Tecnologias Utilizadas
Backend: Node.js + Express

Banco de Dados: MySQL

Autenticação: JWT + Bcrypt

Ferramentas: ESLint, Prettier, REST Client

Testes: Testes de integração via REST Client

⚙️ Pré-requisitos
Node.js v18+

MySQL 8.0+

NPM 9+

🚀 Como Executar
Baixe o projeto

Acesse:
https://github.com/HikeTheCat/Api_AdoptionPet

Clique em Code → Download ZIP

Extraia o ZIP em uma pasta no seu computador.

Abra em uma IDE

Abra sua IDE favorita (ex: VS Code).

Abra a pasta onde extraiu o projeto.

Instale as dependências

No terminal da IDE, rode:

bash
Copiar
Editar
npm install
Configure o banco de dados

Na raiz do projeto, crie um arquivo .env com as variáveis necessárias para o banco.

env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=sua_senha
DB_DATABASE=pets_db
JWT_SECRET=seu_segredo_jwt
PORT=3000
Execute os scripts SQL:

sql
CREATE DATABASE IF NOT EXISTS pets_db;
USE pets_db;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL UNIQUE,
  password VARCHAR(100) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  role ENUM('admin', 'adopter') DEFAULT 'adopter'
);

CREATE TABLE pets (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL,
  species ENUM('dog', 'cat', 'bird', 'other') NOT NULL,
  size ENUM('small', 'medium', 'large') NOT NULL,
  status ENUM('available', 'adopted') DEFAULT 'available',
  description TEXT
);

CREATE TABLE adoptions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  pet_id INT NOT NULL,
  adoption_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (pet_id) REFERENCES pets(id)
);
4. Inicie o servidor
bash
npm run dev
📚 Endpoints da API
🔐 Autenticação
Login de Usuário

http
POST /auth/login
Content-Type: application/json

{
  "email": "usuario@example.com",
  "password": "senha123"
}
👤 Usuários
Criar Novo Usuário

http
POST /users
Content-Type: application/json

{
  "name": "Novo Usuário",
  "email": "novo@example.com",
  "password": "senha456",
  "phone": "11999998888"
}
Listar Usuários (apenas admin)

http
GET /users
Authorization: Bearer <token_admin>
🐕 Pets
Listar Pets Disponíveis (público)

http
GET /pets/available
Criar Novo Pet (apenas admin)

http
POST /pets
Authorization: Bearer <token_admin>
Content-Type: application/json

{
  "name": "Rex",
  "age": 3,
  "species": "dog",
  "size": "medium",
  "description": "Cachorro brincalhão"
}
❤️ Adoções
Solicitar Adoção

http
POST /adoptions
Authorization: Bearer <token_usuario>
Content-Type: application/json

{
  "petId": 1
}
Listar Adoções (apenas admin)

http
GET /adoptions
Authorization: Bearer <token_admin>
🧪 Testando a API
Os testes estão disponíveis no arquivo tests/pet_adoption_tests.rest. Para executar:

Instale a extensão REST Client no VS Code

Abra o arquivo de testes

Clique em "Send Request" acima de cada endpoint para executar

Exemplo de teste:

http
### Testar login de admin
POST http://localhost:3000/auth/login
Content-Type: application/json

{
  "email": "admin@example.com",
  "password": "senhaadmin"
}
📂 Estrutura do Projeto
text
src/
├── config/          # Configuração do banco de dados
├── controllers/     # Lógica das requisições
├── models/          # Acesso ao banco de dados
├── services/        # Regras de negócio
├── routes/          # Definição das rotas
├── middlewares/     # Autenticação e tratamento de erros
├── utils/           # Validações e utilitários
└── app.js           # Configuração principal
⚠️ Regras de Negócio
Apenas administradores podem gerenciar pets

Usuários comuns só podem atualizar seus próprios dados

Pets adotados não podem ser excluídos

Um pet só pode ser adotado uma vez

Usuários não podem alterar seu próprio role

📜 Licença
Este projeto está licenciado sob a MIT License. Sinta-se à vontade para usar e modificar para suas necessidades.

🙋‍♂️ Suporte
Para problemas ou dúvidas, abra uma issue no repositório do projeto.
