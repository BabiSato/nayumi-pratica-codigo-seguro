# CatálogoX API

API REST desenvolvida em **Python**, **Flask** e **SQLite** para gerenciamento de produtos (CRUD).

Este projeto foi utilizado como estudo de práticas de **Secure Programming and Coding**, com foco na identificação e correção de vulnerabilidades de segurança em uma aplicação web.

---

# Tecnologias

* Python 3
* Flask
* SQLite
* Werkzeug
* python-dotenv

Ferramentas utilizadas durante a análise de segurança:

* Bandit (SAST)
* CycloneDX (SBOM)

---

# Estrutura do Projeto

```text
.
├── app.py
├── catalogox.db
├── requirements.txt
├── sbom.json
├── .env
└── README.md
```

---

# Configuração

## 1. Clonar o repositório

```bash
git clone <URL_DO_REPOSITORIO>
cd nayumi-pratica-codigo-seguro
```

## 2. Criar ambiente virtual

### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### Linux/macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## 3. Instalar as dependências

```bash
pip install -r requirements.txt
```

## 4. Configurar as variáveis de ambiente

Criar um arquivo `.env` na raiz do projeto.

Exemplo:

```env
API_USER=admin
API_PASSWORD_HASH=<HASH_DA_SENHA>
```

---

# Executando a aplicação

```bash
python app.py
```

A API ficará disponível em:

```
http://127.0.0.1:5000
```

---

# Endpoints

| Método | Endpoint         | Descrição                |
| ------ | ---------------- | ------------------------ |
| GET    | `/produtos`      | Lista todos os produtos  |
| POST   | `/produtos`      | Cadastra um novo produto |
| PUT    | `/produtos/{id}` | Atualiza um produto      |
| DELETE | `/produtos/{id}` | Remove um produto        |

---

# Autenticação

As rotas da API utilizam autenticação por meio do cabeçalho:

```
Authorization
```

Formato:

```
admin:admin123
```

As credenciais são armazenadas em variáveis de ambiente e a senha é validada utilizando hash seguro com a biblioteca Werkzeug.

---

# Segurança Implementada

Durante a evolução do projeto foram implementadas melhorias relacionadas à segurança da aplicação, entre elas:

* substituição do algoritmo MD5 por hash seguro;
* remoção de credenciais hardcoded;
* utilização de variáveis de ambiente;
* consultas SQL parametrizadas;
* validação dos dados recebidos pela API;
* tratamento mais específico de exceções;
* desativação do modo Debug.

---

# Análise de Segurança

## Bandit (SAST)

Execução:

```bash
bandit app.py
```

Resultado obtido:

```
No issues identified.
```

## CycloneDX (SBOM)

Geração da Software Bill of Materials:

```bash
cyclonedx-py requirements -o sbom.json
```

---

# Repositório

**GitHub:**

> Inserir o link do repositório.

---

# Demonstração

**Vídeo no YouTube:**

> Inserir o link da demonstração.

---

# Autora

**Barbara Nayumi Chagas Sato

**Disciplina: Secure Programming and Coding

**Curso: Defesa Cibernética
