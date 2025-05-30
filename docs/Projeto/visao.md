# Documento de Visão – InventoryTI

**Sistema Web para Gerenciamento de Dispositivos de TI**

---

## Controle de Versões

| Versão | Data       | Autor       | Notas da Revisão               |
|--------|------------|-------------|--------------------------------|
| 1.0.0  | 30/05/2025 | Bruno Lima  | Criação do Documento de Visão  |

---

## Sumário

- [Documento de Visão – InventoryTI](#documento-de-visão--inventoryti)
  - [Controle de Versões](#controle-de-versões)
  - [Sumário](#sumário)
  - [1. Objetivo Deste Documento](#1-objetivo-deste-documento)
  - [2. Justificativa](#2-justificativa)
  - [3. Objetivos do Sistema](#3-objetivos-do-sistema)
  - [4. Fluxo Operacional](#4-fluxo-operacional)
  - [5. Descrição do Produto](#5-descrição-do-produto)
  - [6. Tecnologias Definidas](#6-tecnologias-definidas)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [Banco de Dados](#banco-de-dados)
    - [Ferramentas Adicionais](#ferramentas-adicionais)
  - [7. Requisitos](#7-requisitos)
  - [8. Stakeholders](#8-stakeholders)
  - [9. Escopo](#9-escopo)
    - [Incluído](#incluído)
    - [Fora do Escopo](#fora-do-escopo)
  - [10. Restrições](#10-restrições)
  - [11. Riscos](#11-riscos)
  - [12. Cronograma](#12-cronograma)
  - [14. Referências](#14-referências)

---

## 1. Objetivo Deste Documento

Estabelecer uma visão clara e compartilhada do projeto de um sistema web para controle de dispositivos de TI, definindo funcionalidades, tecnologias, fluxo de uso e contexto organizacional. Este documento serve como base para o desenvolvimento e validação do sistema, alinhando expectativas entre stakeholders e equipe técnica.

---

## 2. Justificativa

O controle manual de ativos de TI em planilhas ou anotações gera perdas, retrabalho e dificuldade de gestão. Um sistema web centralizado proporciona melhor rastreabilidade, segurança e eficiência administrativa. A implementação deste sistema visa:

- Aumentar eficiência na localização de equipamentos
- Melhorar controle de manutenções
- Otimizar a distribuição de recursos de TI
- Facilitar auditorias e inventários periódicos

---

## 3. Objetivos do Sistema

- Cadastrar, atualizar e excluir dispositivos
- Cadastrar, atualizar e excluir usuários
- Cadastrar, atualizar e excluir locais físicos
- Atribuir dispositivos a usuários e locais físicos
- Controlar status de funcionamento e movimentações
- Gerar relatórios de situação e inventário
- Manter histórico completo de cada dispositivo
- Permitir busca avançada por diversos critérios

---

## 4. Fluxo Operacional

1. Administrador faz login no sistema.
2. Cadastra ou atualiza dispositivo com modelo, tombo, status e localização.
3. Atribui dispositivo a um colaborador/setor.
4. Atualiza status em caso de manutenção, movimentação ou descarte.
5. Gera relatórios filtrando por setor, status ou tipo de dispositivo.

**Fluxo de Movimentação de Dispositivo:**
1. Técnico identifica necessidade de movimentação
2. Acessa sistema e localiza dispositivo atual
3. Técnico executa movimentação física
4. Atualiza sistema com nova localização/usuário
5. Sistema registra histórico completo da movimentação

---

## 5. Descrição do Produto

| Nº | Funcionalidade                   | Descrição                                                                              |
|----|----------------------------------|----------------------------------------------------------------------------------------|
| 01 | Cadastro de Dispositivos         | Contem informações referentes ao dispositivos (marca, modelo, quantidade)              |
| 02 | Cadastro de Funcionários         | Contem informações obre os funcionários e o setores onde trabalham                     |
| 04 | Cadastro de Locais               | Contem informações sobre filial, endereço, sala, setor, superintendência               |
| 05 | Associação Usuário x Dispositivo | Relacionamento lógico entre colaborador e equipamento com data                         |
| 06 | Controle de Localização          | Acompanhamento de onde o equipamento está com histórico de movimentações               |
| 07 | Histórico de Movimentações       | Registro de todas as mudanças de localização/usuário com responsável pela movimentação |
| 08 | Geração de Relatórios            | Relatórios por status, setor, tipo, valor, idade, garantia                             |
| 09 | Controle de Acesso               | Perfis de acesso com login e autenticação segura via JWT                               |
| 10 | Dashboard Gerencial              | Visão consolidada de estatísticas e indicadores de estado dos equipamentos             |

---

## 6. Tecnologias Definidas

### Frontend
- **Vue.js**: Framework progressivo para construção de interfaces reativas
  - *Justificativa*: Curva de aprendizado baixa, documentação excelente, componentização
- **Quasar Framework**: Framework UI baseado em Vue.js
  - *Justificativa*: Componentes prontos, responsividade, temas personalizáveis

### Backend
- **Node.js**: Ambiente de execução JavaScript server-side
  - *Justificativa*: Performance, mesma linguagem do frontend, vasto ecossistema
- **NestJS**: Framework Node.js para aplicações server-side
  - *Justificativa*: Arquitetura modular, injeção de dependências, tipagem forte
- **Prisma ORM**: ORM de próxima geração para Node.js e TypeScript
  - *Justificativa*: Type-safety, migrações automatizadas, client gerado

### Banco de Dados
- **PostgreSQL**: Sistema de banco de dados relacional
  - *Justificativa*: Confiabilidade, recursos avançados, suporte a JSON, extensibilidade

### Ferramentas Adicionais
- **Docker**: Containerização para desenvolvimento e implantação
- **Jest**: Framework de testes para garantir qualidade
- **Swagger**: Documentação automática da API

---

## 7. Requisitos

Os requisitos detalhados do sistema estão disponíveis no seguinte documento:

[Documento de Requisitos (requisitos.md)](./requisitos.md)

---

## 8. Stakeholders

| Nome             | Papel                 | Interesse no sistema                                     | Responsabilidades                            |
|------------------|-----------------------|----------------------------------------------------------|----------------------------------------------|
| Gerente de TI    | Administrador         | Gerenciar todos os recursos, gerar relatórios gerenciais |                                              |
| Suporte técnico  | Técnico de manutenção | Atualizar status, movimentar equipamentos                | Registrar manutenções, atualizar informações |
| Usuário comum    | Colaborador           | Visualizar seus dispositivos e status                    | Confirmar recebimento, reportar problemas    |
| Auditor          | Fiscalizador          | Verificar conformidade de processos e ativos             | Realizar inventários periódicos              |

---

## 9. Escopo

### Incluído
- Sistema web completo com login, CRUD, histórico e relatórios
- Responsividade para desktop e mobile
- Controle de acesso baseado em perfis
- Exportação de relatórios em PDF e CSV
- API documentada para integrações futuras

### Fora do Escopo
- Integração com sistemas legados
- Aplicativos móveis nativos
- Controle financeiro detalhado
- Gestão de contratos com fornecedores
- Módulo de helpdesk
- Reconhecimento de imagem para identificação de ativos

---

## 10. Restrições

- Banco de dados será PostgreSQL
- Frontend será responsivo para dispositivos a partir de 320px
- Backend baseado em módulos com NestJS
- Autenticação segura utilizando JWT com renovação
- Conformidade com LGPD para dados pessoais
- Compatibilidade com navegadores modernos (Chrome, Firefox, Edge, Safari)

---

## 11. Riscos

| ID  | Risco                                     | Probabilidade | Impacto | Mitigação                                                                        |
|-----|-------------------------------------------|---------------|---------|----------------------------------------------------------------------------------|
| R01 | Mudança frequente de escopo               | Alta          | Alto    | Validação de requisitos com stakeholders, documentação detalhada, sprints curtos |
| R02 | Infraestrutura externa instável           | Baixa         | Alto    | Plano de contingência para hospedagem, caching, design resiliente                |
| R03 | Resistência dos usuários à adoção         | Média         | Médio   | Treinamento adequado, interface intuitiva, comunicação dos benefícios            |
| R04 | Vulnerabilidades de segurança             | Baixa         | Alto    | Testes de penetração, code reviews, atualizações frequentes                      |

---

## 12. Cronograma

| Etapa                      | Início     | Fim        | Entregas                                             |
|----------------------------|------------|------------|------------------------------------------------------|
| Levantamento de Requisitos | 29/05/2025 | 30/05/2025 | Documentos de visão, requisitos e casos de uso       |
| Prototipação das Telas     | 30/05/2025 | 31/05/2025 | Wireframes e mockups                                 |
| Desenvolvimento Backend    |            |            | API funcional com documentação                       |
| Desenvolvimento Frontend   |            |            | Interface responsiva com fluxos completos            |
| Testes e Ajustes           |            |            | Relatório de testes e correções                      |
| Implantação                |            |            | Sistema em produção com monitoramento                |

---

## 14. Referências

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Vue.js Guide](https://vuejs.org/guide/introduction.html)
- [Quasar Framework](https://quasar.dev/)
- [NestJS Documentation](https://docs.nestjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs/)