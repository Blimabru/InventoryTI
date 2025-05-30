# Documento de Requisitos – InventoryTI

## Controle de Versões

| Versão | Data       | Autor       | Notas da Revisão                       |
|--------|------------|-------------|----------------------------------------|
| 1.0.0  | 30/05/2025 | Bruno Lima  | Criação do documento de requisitos     |

---

## 1. Introdução

Este documento descreve os requisitos funcionais e não funcionais do sistema de controle de dispositivos de TI. Serve como base para o desenvolvimento, validação e testes da aplicação.

### 1.1 Propósito

Definir de forma clara e objetiva os requisitos do sistema para orientar o desenvolvimento e garantir que todas as necessidades dos stakeholders sejam atendidas.

### 1.2 Escopo

Este documento abrange todos os requisitos do sistema de controle de dispositivos de TI, desde o cadastro de equipamentos até a geração de relatórios gerenciais.

---

## 2. Requisitos Funcionais (RF)

| Código | Requisito | Descrição | Prioridade | Dependências |
|--------|-----------|-----------|------------|--------------|
| RF01   | Cadastro de dispositivos | O sistema deve permitir o cadastro de novos dispositivos de TI com informações como marca, modelo, número de série, número de patrimônio (tombo) data de aquisição, valor, garantia, status de funcionamento (novo, antigo, obsoleto) e tipo. | Alta | - |
| RF02   | Cadastro de funcionários | O sistema deve permitir o cadastro de funcionários com nome, email, setor, cargo, , número de matrícula e contato. | Alta | - |
| RF03   | Cadastro de locais | O sistema deve permitir o cadastro de setores, órgãos, filiais, contendo localização física (endereço). | Alta | - |
| RF04   | Associação de dispositivos a usuários | O sistema deve permitir associar dispositivos a funcionários específicos, registrando data. | Alta | RF01, RF02 |
| RF05   | Atualização de status e localização | O sistema deve permitir alterar o status operacional (Ativo, Em Manutenção, Inativo, etc.) e a localização física dos dispositivos. | Alta | RF01 |
| RF06   | Listagem de dispositivos | O sistema deve exibir a lista de dispositivos com filtros por setor, status, tipo, funcionário e localização. | Média | RF01 |
| RF07   | Histórico de movimentações | O sistema deve manter um registro detalhado de todas as movimentações de cada dispositivo, incluindo datas, responsáveis e motivos. | Alta | RF01, RF03, RF04 |
| RF08   | Geração de relatórios | O sistema deve gerar relatórios em PDF e CSV com diversos filtros (status, tipo, localização, valor, idade). | Média | RF01, RF05 |
| RF09   | Autenticação e autorização | O sistema deve permitir login de diferentes perfis de usuário (Administrador, Técnico, Colaborador) com diferentes níveis de acesso. | Alta | - |
| RF10   | Controle de acesso | O sistema deve impedir ações não autorizadas conforme o perfil do usuário logado. | Alta | RF08 |
| RF11   | Busca avançada | O sistema deve oferecer busca por texto em múltiplos campos com filtros combinados. | Média | RF01, RF02 |
| RF12   | Dashboard gerencial | O sistema deve apresentar indicadores visuais sobre a distribuição e status dos dispositivos. | Baixa | RF01, RF05 |

---

## 3. Requisitos Não Funcionais (RNF)

| Código | Requisito | Descrição | Métrica de Aceitação |
|--------|-----------|-----------|----------------------|
| RNF01  | Autenticação segura | O sistema deve utilizar autenticação segura via JWT com expiração de token. | Tokens com validade máxima de 24h e refresh token de 7 dias. |
| RNF02  | Responsividade | O sistema deve ser responsivo para desktop e dispositivos móveis. | Funcional em telas a partir de 320px até 1920px sem quebras de layout. |
| RNF03  | Banco de dados | O banco de dados deve ser PostgreSQL 14 ou superior. | Tempo médio de consultas complexas abaixo de 500ms. |
| RNF04  | Backend | O backend deve ser desenvolvido com Node.js 18+ e NestJS 10+. | Cobertura de testes mínima de 80%. |
| RNF05  | Frontend | O frontend deve utilizar Vue.js 3 e Quasar Framework 2+. | Lighthouse score mínimo de 90 para performance e acessibilidade. |
| RNF06  | Arquitetura | O sistema deve ser escalável e modular, seguindo princípios SOLID. | Cada módulo deve ter responsabilidade única e interface bem definida. |
| RNF07  | Segurança | A senha dos usuários deve ser armazenada de forma criptografada usando bcrypt. | Mínimo de 10 rounds no fator de custo do bcrypt. |
| RNF08  | Disponibilidade | A aplicação deve estar disponível 99% do tempo (exceto janelas de manutenção). | Monitoramento contínuo com alerta para downtime superior a 5 minutos. |
| RNF09  | Performance | O sistema deve responder a operações básicas em menos de 2 segundos. | Tempo médio de resposta abaixo de 500ms para 95% das requisições. |
| RNF10  | Logs e Auditoria | O sistema deve manter logs de todas as operações críticas. | Log estruturado com nível, timestamp, usuário e operação. |
| RNF11  | Backup | O sistema deve permitir backup automático diário do banco de dados. | RTO de 4 horas e RPO de 24 horas no máximo. |
| RNF12  | Compatibilidade | O sistema deve funcionar nos navegadores Chrome, Firefox, Edge e Safari. | Funcionalidade completa nas duas últimas versões de cada navegador. |

---

## 4. Requisitos Futuros (RFU)

| Código | Requisito Futuro | Descrição | Prioridade |
|--------|------------------|-----------|------------|
| RFU02  | QR Code | O sistema poderá gerar etiquetas QR Code para cada equipamento facilitando inventário. | Alta |

---

## 5. Critérios de Aceitação

### 5.1 Critérios Gerais

- Todos os formulários devem validar campos obrigatórios.
- Apenas administradores podem excluir registros.
- Usuário comum só pode visualizar seus próprios dispositivos.
- Os relatórios devem ser exportáveis em PDF e/ou CSV.

### 5.2 Critérios Específicos por Requisito

**RF01 - Cadastro de dispositivos:**
- Deve validar número de série como único
- Deve permitir upload de nota fiscal
- Deve calcular automaticamente fim da garantia

**RF03 - Associação de dispositivos:**
- Deve gerar termo de responsabilidade em PDF
- Deve registrar quem fez a associação
- Deve impedir associação de dispositivos inativos

**RF06 - Histórico de movimentações:**
- Deve ser imutável após registro
- Deve conter carimbos de data/hora e usuário
- Deve permitir comentários em cada movimentação

---

## 6. Dependências entre Requisitos

| Requisito | Depende de | Justificativa |
|-----------|------------|---------------|
| RF04      | RF01, RF02 | Precisa de dispositivos e funcionários cadastrados para fazer associação |
| RF05      | RF01, RF03 | Precisa de dispositivos cadastrados e locais para atualizar localização |
| RF06      | RF01, RF03 | Precisa de dispositivos cadastrados e locais para filtrar listagens |
| RF07      | RF01, RF04, RF05 | Registra histórico de ações relacionadas a dispositivos, suas associações e mudanças de status |
| RF08      | RF01, RF06 | Gera relatórios baseados nos dispositivos cadastrados e suas listagens |
| RF10      | RF09 | Controle de acesso depende da autenticação e autorização |
| RF11      | RF01, RF02, RF03 | Busca avançada em múltiplos campos relacionados a dispositivos, funcionários e locais |
| RF12      | RF01, RF06, RF07 | Dashboard é baseado nas listagens, filtros e histórico de dispositivos |

---

## 7. Glossário

| Termo | Definição |
|-------|-----------|
| Dispositivo | Qualquer equipamento de TI: computadores, monitores, impressoras, etc. |
| Tombo | Número de patrimônio único do dispositivo na organização |
| Status | Estado atual do dispositivo: Ativo, Em Manutenção, Inativo, etc. |
| Movimentação | Qualquer alteração de localização, usuário ou status de um dispositivo |
| JWT | JSON Web Token - padrão para autenticação segura |

---

## 8. Referências

- [Documento de Visão do Projeto](./visao.md)
- [Documentação Vue.js](https://vuejs.org/guide/introduction.html)
- [Documentação NestJS](https://docs.nestjs.com/)
- [Documentação Prisma](https://www.prisma.io/docs/)
- [Documentação PostgreSQL](https://www.postgresql.org/docs/)