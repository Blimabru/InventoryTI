# Documentação da API – InventoryTI

Este documento descreve os principais endpoints da API RESTful do sistema InventoryTI, desenvolvida com NestJS.

---

## Autenticação

- **Login**
  - `POST /auth/login`
  - Body: `{ "email": "admin@exemplo.com", "password": "123456" }`
  - Retorna: token JWT

---

## Dispositivos

- **Listar todos**
  - `GET /devices`
- **Buscar por ID**
  - `GET /devices/:id`
- **Criar novo**
  - `POST /devices`
  - Body: `{ "name": "Notebook", "model": "Dell", ... }`
- **Atualizar**
  - `PUT /devices/:id`
- **Deletar**
  - `DELETE /devices/:id`

---

## Usuários

- **Listar usuários**
  - `GET /users`
- **Cadastrar**
  - `POST /users`
- **Atualizar**
  - `PUT /users/:id`
- **Excluir**
  - `DELETE /users/:id`

---

## Localizações

- **Listar locais**
  - `GET /locations`
- **Cadastrar local**
  - `POST /locations`
- **Atualizar local**
  - `PUT /locations/:id`

---

## Relatórios

- **Resumo geral**
  - `GET /reports/summary`
- **Por status**
  - `GET /reports/status`
- **Por local**
  - `GET /reports/location`

---

## Observações

- Todas as rotas protegidas requerem o header:
  ```
  Authorization: Bearer <token>
  ```

- As respostas seguem o formato JSON padrão com:
  ```json
  {
    "status": "success",
    "data": { ... }
  }
  ```

- Em caso de erro:
  ```json
  {
    "status": "error",
    "message": "Descrição do erro"
  }
  ```

---

## Referências

- [NestJS Docs](https://docs.nestjs.com/)
- [JWT Auth](https://jwt.io/)
