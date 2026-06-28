# CatálogoX API – Secure Programming and Coding

## Descrição

Este projeto foi desenvolvido como atividade prática da disciplina **Secure Programming and Coding**.

A aplicação consiste em uma API REST para gerenciamento de produtos (CRUD), desenvolvida em Python utilizando Flask e SQLite. O objetivo deste trabalho foi identificar vulnerabilidades presentes na aplicação original, aplicar correções utilizando boas práticas de Secure Coding e documentar todo o processo.

---

# Tecnologias Utilizadas

* Python 3.x
* Flask
* SQLite
* python-dotenv
* Werkzeug
* Bandit (SAST)
* CycloneDX (SBOM)

---

# Estrutura do Projeto

```text
.
├── app.py
├── catalogox.db
├── .env
├── requirements.txt
├── sbom.json
└── README.md
```

---

# Instalação

Clone o repositório:

```bash
git clone <URL_DO_REPOSITORIO>
```

Entre na pasta:

```bash
cd nome-aluno-pratica-codigo-seguro
```

Crie o ambiente virtual:

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

Instale as dependências:

```bash
pip install -r requirements.txt
```

Caso não exista o arquivo `requirements.txt`:

```bash
pip install flask python-dotenv werkzeug bandit cyclonedx-bom
```

---

# Configuração

Crie um arquivo chamado `.env` na raiz do projeto.

Exemplo:

```env
API_USER=admin
API_PASSWORD_HASH=<HASH_GERADO_COM_generate_password_hash>
```

O hash da senha pode ser gerado com:

```python
from werkzeug.security import generate_password_hash

print(generate_password_hash("admin123"))
```

---

# Executando a aplicação

Execute:

```bash
python app.py
```

A API ficará disponível em:

```
http://127.0.0.1:5000
```

---

# Endpoints

## Criar produto

POST

```
/produtos
```

Body:

```json
{
    "nome": "Notebook",
    "preco": 3500
}
```

---

## Listar produtos

GET

```
/produtos
```

---

## Atualizar produto

PUT

```
/produtos/{id}
```

---

## Remover produto

DELETE

```
/produtos/{id}
```

---

# Autenticação

A API utiliza autenticação simples através do cabeçalho HTTP:

```
Authorization
```

Formato:

```
admin:admin123
```

A senha é validada utilizando hash seguro através da biblioteca Werkzeug.

---

# Ferramentas Utilizadas

## Bandit

Ferramenta utilizada para análise estática (SAST).

Execução:

```bash
bandit -r .
```

Objetivo:

* identificar falhas de segurança no código;
* localizar práticas inseguras;
* validar as correções implementadas.

---

## CycloneDX

Ferramenta utilizada para geração da SBOM (Software Bill of Materials).

Execução:

```bash
cyclonedx-py requirements -o sbom.json
```

Objetivo:

* inventariar dependências;
* facilitar rastreabilidade;
* identificar bibliotecas vulneráveis.

---

# Vulnerabilidades Identificadas

Durante a análise foram encontradas as seguintes vulnerabilidades:

* Uso de MD5 para armazenamento de senhas;
* Credenciais hardcoded no código-fonte;
* SQL Injection;
* Falta de validação de entrada;
* Debug habilitado em ambiente de produção;
* Tratamento genérico de exceções.

---

# Correções Implementadas

## Hash de senha

Foi removido o algoritmo MD5.

Implementado:

* `check_password_hash()`

Benefício:

* armazenamento seguro de senhas.

---

## Variáveis de ambiente

As credenciais deixaram de ficar no código.

Foi implementado:

* arquivo `.env`
* biblioteca `python-dotenv`

Benefício:

* redução da exposição de credenciais.

---

## SQL Injection

Todas as consultas SQL passaram a utilizar consultas parametrizadas.

Antes:

```python
cursor.execute(f"...")
```

Depois:

```python
cursor.execute(
    "... VALUES (?, ?)",
    (nome, preco)
)
```

Benefício:

* eliminação de SQL Injection.

---

## Validação de entrada

Foi implementada validação para:

* nome obrigatório;
* tipo de dado;
* preço numérico;
* preço maior que zero.

Benefício:

* evita inserção de dados inválidos.

---

## Tratamento de exceções

O uso de:

```python
except:
```

foi substituído por exceções específicas.

Benefício:

* melhora auditoria e manutenção.

---

## Configuração da aplicação

O modo debug foi desabilitado.

Antes:

```python
app.run(debug=True)
```

Depois:

```python
app.run(debug=False)
```

Benefício:

* impede exposição de informações sensíveis.

---

# Resultados Obtidos

Após a remediação foram alcançados os seguintes resultados:

* eliminação das vulnerabilidades de SQL Injection;
* substituição do MD5 por algoritmo seguro;
* remoção das credenciais do código-fonte;
* implementação de validação de entradas;
* configuração segura da aplicação;
* redução significativa da superfície de ataque;
* melhoria na manutenção e segurança do projeto.

---

# Histórico de Correções

Os commits do repositório demonstram a evolução da aplicação durante o processo de correção das vulnerabilidades.

Principais alterações:

* remoção de credenciais hardcoded;
* substituição do MD5;
* implementação de consultas parametrizadas;
* validação dos dados recebidos;
* melhoria do tratamento de exceções;
* desativação do modo debug.

---

# Referências

* OWASP Top 10
* OWASP API Security Top 10
* MITRE CWE
* Bandit Documentation
* CycloneDX Documentation
* Flask Documentation
* Werkzeug Documentation

---

# Autora

**Barbara Nayumi Chagas Sato**

Disciplina: Secure Programming and Coding

Curso: Defesa Cibernética
