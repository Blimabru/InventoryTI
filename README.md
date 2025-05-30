# 📦 InventoryTI

Sistema Web para controle de dispositivos de TI, com gerenciamento de inventário, localização, usuários e movimentações. Desenvolvido com tecnologias modernas como Vue.js, Quasar, NestJS, Prisma e PostgreSQL.

![Versão](https://img.shields.io/badge/Versão-1.0.0-blue)
![Status](https://img.shields.io/badge/Status-Em%20desenvolvimento-yellow)
![Licença](https://img.shields.io/badge/Licença-CC_BY--NC_4.0-orange)

---

## 📋 Sobre o Projeto

O InventoryTI é uma solução completa para gerenciamento de ativos de TI, permitindo:

- Cadastro e rastreamento de equipamentos
- Controle de movimentações e manutenções
- Associação de dispositivos a usuários e locais
- Histórico completo da vida útil dos equipamentos
- Relatórios gerenciais e dashboards analíticos
- Controle de acesso baseado em perfis

Ideal para empresas que precisam controlar seu parque tecnológico de forma eficiente e segura.

---

## 📁 Estrutura do Projeto

```
inventoryTI/
├── backend/        # Backend com NestJS + Prisma
├── frontend/       # Frontend com Vue.js + Quasar Framework
├── docs/           # Documentação do projeto
│   ├── visao.md
│   ├── requisitos.md
│   ├── casos-de-uso.md
|   ├── diagramas/
│   └── protótipos/
├── README.md
└── .gitignore
```

---

## 🚀 Tecnologias

| Camada     | Tecnologias                      | Justificativa |
|------------|----------------------------------|---------------|
| Frontend   | Vue.js, Quasar Framework         | Framework reativo com componentização e UI kit completo |
| Backend    | Node.js, NestJS, Prisma ORM      | Arquitetura modular com tipagem forte e ORM robusto |
| Banco de Dados | PostgreSQL                   | SGBD relacional com suporte a JSON e recursos avançados |
| Autenticação | JWT, bcrypt                    | Segurança e escalabilidade para controle de acesso |

---

## 🔍 Funcionalidades Principais

- **Cadastro completo de dispositivos**: Computadores, periféricos, servidores e qualquer ativo de TI
- **Controle de localização**: Saiba exatamente onde está cada equipamento
- **Atribuição a usuários**: Associe dispositivos a colaboradores com termos de responsabilidade
- **Histórico de movimentações**: Registro completo de todas as alterações e movimentações
- **Controle de manutenções**: Acompanhe manutenções preventivas e corretivas
- **Dashboard gerencial**: Visualize indicadores importantes para tomada de decisão
- **Relatórios detalhados**: Exporte dados em múltiplos formatos para análise

---

## 🧪 Como rodar localmente

### Pré-requisitos

- Node.js (v18+)
- PostgreSQL
- Yarn ou npm

### Banco de Dados

#### Criar banco de dados PostgreSQL

```bash
createdb inventoryti
```

#### Configurar variáveis de ambiente

```bash
cp .env.example .env
```

#### Edite o arquivo .env com suas configurações

### Backend

```bash
cd backend
npm install
npx prisma migrate dev --name init
npx prisma generate
npm run start:dev
```

### Frontend

```bash
cd frontend
npm install
quasar dev
```

### Acesso
Após iniciar os serviços, acesse:

- Frontend: http://localhost:9000
- API Backend: http://localhost:3000
- Documentação API: http://localhost:3000/api/docs

---

## 🌱 Branches e Fluxo de Desenvolvimento

| Branch                    | Descrição                                     |
|---------------------------|-----------------------------------------------|
| `main`                    | Código estável e pronto para deploy           |
| `develop`                 | Integração contínua de funcionalidades        |
| `frontend/...`            | Alterações específicas na camada de frontend  |
| `backend/...`             | Alterações específicas na camada de backend   |
| `feature/...`             | Desenvolvimento de novas funcionalidades      |
| `fix/...`                 | Correções de bugs                             |
| `docs/...`                | Atualizações e adições de documentação        |

### Combinação de Prefixos

Para maior especificidade, os prefixos podem ser combinados hierarquicamente:

- `backend/feature/...` - Nova funcionalidade específica do backend
- `backend/fix/...` - Correção de bug específica do backend
- `frontend/feature/...` - Nova funcionalidade específica do frontend
- `frontend/fix/...` - Correção de bug específica do frontend

Exemplos:
- `backend/feature/auth-controller` - Implementação do controlador de autenticação
- `frontend/fix/login-validation` - Correção na validação do formulário de login

---

### Padrão de Commits

Utilizamos o padrão Conventional Commits com adição de emojis para facilitar a identificação visual:

```bash
<emoji> <tipo>: <título curto>

<corpo detalhado em linhas com no máximo 72 caracteres>
```

#### Tipos de Commits e Seus Emojis

| Emoji | Tipo        | Descrição                                                   |
|-------|--------------|-------------------------------------------------------------|
| ✨     | feat       | Nova funcionalidade                                         |
| 🐛     | fix        | Correção de bugs                                            |
| 📚     | docs       | Alterações na documentação                                  |
| 💄     | style      | Alterações na estilização                                   |
| ♻️     | refactor   | Alteração no código que não corrige bug ou adiciona feature |
| ⚡️     | perf       | Alteração que melhora performance                           |
| ✅     | test       | Adição ou correção de testes                                |
| 📦     | chore      | Alterações no processo de build ou ferramentas aux.         |
| 🚀     | ci         | Alterações nos arquivos de CI/CD                            |
| 🔧     | build      | Alterações que afetam o sistema de build                    |
| 🔒     | security   | Correções de segurança                                      |

### Exemplos de Commits


# Exemplo de nova funcionalidade

```bash
git commit -m "✨ feat: adiciona módulo de associação de dispositivos a usuários

- Implementa interface para seleção de dispositivos disponíveis
- Adiciona validação para evitar associações duplicadas
- Gera automaticamente termo de responsabilidade em PDF
- Registra o histórico da associação com data e responsável
- Atualiza o status do dispositivo para \"Em Uso\" após associação"
```

# Exemplo de refatoração

```bash
git commit -m "♻️ refactor: otimiza consultas de busca de dispositivos

- Adiciona índices para campos frequentemente consultados
- Implementa lazy loading para reduzir tempo de carregamento inicial
- Reorganiza estrutura das consultas para melhor performance
- Ajusta paginação para limitar resultados a 50 itens por página"
```

# Exemplo de atualização de dependências

```bash
git commit -m "📦 chore: atualiza dependências do frontend

- @quasar/app: ^3.3.3 → ^3.5.7
- core-js: ^3.21.1 → ^3.25.0
- vue: ^3.2.31 → ^3.2.37
- axios: ^0.26.0 → ^0.27.2
- pinia: ^2.0.11 → ^2.0.21"
```

# Exemplo de correção de bug

```bash
git commit -m "🐛 fix: corrige problema na geração de relatórios PDF

- Resolve problema de caracteres especiais quebrados no título
- Corrige alinhamento das tabelas em dispositivos com tela pequena
- Adiciona tratamento de erro para casos sem dados
- Ajusta margens para evitar corte de conteúdo na impressão"
```

---

## 📄 Documentação

A documentação completa está disponível na pasta [`/docs`](./docs):

- [Documento de Visão](./docs/Projeto/visao.md)
- [Documento de Requisitos](./docs/Projeto/requisitos.md)
- [Casos de Uso](./docs/Projeto/casos-de-uso.md)
- [Documentação da API](./docs/API/api.md)
- [Diagramas](./docs/Projeto/Diagramas/)

---

## 📃 Licença

Este projeto está licenciado sob a [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](LICENSE). Esta licença permite o compartilhamento e adaptação do material, desde que seja dado o crédito apropriado e não seja utilizado para fins comerciais sem autorização explícita.