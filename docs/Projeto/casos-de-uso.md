# Documento de Casos de Uso – InventoryTI

## Controle de Versões

| Versão | Data       | Autor       | Notas da Revisão                             |
|--------|------------|-------------|----------------------------------------------|
| 1.0.0  | 30/05/2023 | Bruno Lima  | Criação inicial do documento de casos de uso |

---

## 1. Introdução

Este documento descreve os casos de uso do sistema de controle de dispositivos de TI, detalhando as interações entre os atores e o sistema, seus fluxos principais e alternativos, além das condições necessárias para cada operação.

### 1.1 Finalidade

Fornecer uma base para entendimento das funcionalidades do sistema e servir como referência para desenvolvimento, testes e validação.

### 1.2 Escopo

Este documento abrange todos os casos de uso essenciais para o funcionamento do sistema de controle de dispositivos de TI.

---

## 2. Atores do Sistema

| Ator              | Descrição                                                                                                             | Responsabilidades |
|-------------------|-----------------------------------------------------------------------------------------------------------------------|-------------------|
| Administrador     | Possui acesso total ao sistema, incluindo gerenciamento de usuários e configurações | Gerir usuários, configurar sistema, definir parâmetros |
| Técnico           | Realiza operações de manutenção, movimentação e atualização de status dos dispositivos | Registrar manutenções, atualizar status, executar movimentações |
| Colaborador       | Usuário final que visualiza apenas seus dispositivos atribuídos | Confirmar recebimento, visualizar seus dispositivos |
| Sistema           | Processos automatizados do próprio sistema | Gerar logs  |

---

## 3. Lista de Casos de Uso

| Código | Caso de Uso                            | Atores                         | Prioridade |
|--------|----------------------------------------|--------------------------------|------------|
| UC01   | Autenticar no Sistema                  | Todos                          | Alta |
| UC02   | Gerenciar Dispositivos                 | Administrador, Técnico         | Alta |
| UC03   | Gerenciar Funcionários                 | Administrador, Técnico         | Alta |
| UC04   | Gerenciar Locais                       | Administrador, Técnico         | Alta |
| UC05   | Associar Dispositivo a Usuário         | Administrador, Técnico         | Alta |
| UC06   | Atualizar Status de Dispositivo        | Administrador, Técnico         | Alta |
| UC07   | Visualizar Dispositivos                | Todos                          | Média |
| UC08   | Consultar Histórico de Movimentações   | Administrador, Técnico         | Média |
| UC09   | Gerar Relatórios                       | Administrador, Técnico         | Média |
| UC10   | Gerenciar Perfis de Acesso             | Administrador                  | Alta |
| UC11   | Buscar Dispositivos                    | Todos                          | Média |
| UC12   | Gerar Dashboard Gerencial              | Administrador                  | Baixa |

---

## 5. Detalhamento dos Casos de Uso

### UC01 - Autenticar no Sistema

**Descrição:** Permite que o usuário acesse o sistema mediante autenticação.

**Atores:** Administrador, Técnico, Colaborador

**Pré-condições:** 
- O usuário deve estar cadastrado no sistema.

**Pós-condições:**
- O usuário está autenticado com seu respectivo nível de acesso.
- Token JWT válido gerado.

**Fluxo Principal:**
1. O usuário acessa a tela de login.
2. O sistema apresenta os campos de nome de usuário e senha.
3. O usuário preenche as credenciais.
4. O sistema valida as informações.
5. O sistema gera um token JWT e um refresh token.
6. O sistema redireciona para a página inicial de acordo com o perfil.

**Fluxo Alternativo 1:** Credenciais inválidas
1. O sistema exibe mensagem de erro específica (nome de usuário não encontrado ou senha incorreta).
2. O usuário pode tentar novamente ou solicitar recuperação de senha.
3. Após 5 tentativas incorretas, a conta é temporariamente bloqueada por 15 minutos.

**Fluxo Alternativo 2:** Esqueceu a senha
1. O usuário clica em "Esqueci minha senha".
2. O sistema solicita o e-mail cadastrado.
3. O sistema envia link de recuperação com token único e validade de 1 hora.
4. O usuário acessa o link e define nova senha.

**Fluxo Alternativo 3:** Primeiro acesso
1. Se for o primeiro acesso, o sistema solicita troca da senha provisória.
2. O usuário define nova senha seguindo política de segurança.
3. O sistema valida e salva a nova senha.
4. O fluxo principal continua a partir do passo 5.

**Exemplo de Dados:**
- E-mail: usuario@empresa.com
- Senha: Pa$$w0rd123
- Token JWT: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
- Refresh Token: a1b2c3d4e5f6g7h8i9j0...

**Requisitos Relacionados:** RF08, RNF01, RNF07

**Protótipo de Tela:**
[Link para o protótipo da tela de login](./docs/Projeto/Protótipos/login.png)

---

### UC02 - Gerenciar Dispositivos

**Descrição:** Permite cadastrar, consultar, atualizar e excluir dispositivos de TI.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.

**Pós-condições:**
- Dispositivos são criados, atualizados ou excluídos no sistema.
- Registro de log da operação realizada.

**Fluxo Principal:**
1. O usuário acessa o módulo de dispositivos.
2. O sistema apresenta a lista de dispositivos cadastrados.
3. O usuário seleciona a operação desejada (cadastrar, visualizar, editar, excluir).
4. Para cadastro/edição, o sistema exibe formulário com campos necessários.
5. O usuário preenche as informações (modelo, número de série, tombo, status, etc.).
6. O sistema valida e salva as informações.
7. O sistema registra a operação no log de auditoria.

**Fluxo Alternativo 1:** Dados inválidos
1. O sistema destaca campos com erro e mostra mensagem explicativa.
2. O usuário corrige as informações.
3. O sistema valida novamente.
4. Se válido, o fluxo principal continua do passo 6.

**Fluxo Alternativo 2:** Dispositivo já cadastrado
1. O sistema notifica a duplicidade (mesmo número de série ou tombo).
2. O usuário pode:
   a. Cancelar a operação
   b. Atualizar o existente
   c. Verificar o dispositivo existente
3. O sistema processa a opção escolhida.

**Fluxo Alternativo 3:** Exclusão de dispositivo
1. O sistema verifica se o dispositivo tem associações.
2. Se houver associações, o sistema alerta e oferece opções:
   a. Cancelar exclusão
   b. Remover associações e continuar
3. O usuário confirma a exclusão digitando "CONFIRMAR".
4. O sistema marca o dispositivo como excluído (exclusão lógica).

**Exemplo de Dados:**
- Tipo: Notebook
- Marca: Dell
- Modelo: Latitude 5420
- Número de Série: ABC123XYZ
- Tombo: 2023001
- Data de Aquisição: 10/01/2023
- Valor: R$ 5.800,00
- Período de Garantia: 36 meses
- Status: Disponível
- Observações: Equipamento com 16GB RAM e SSD 512GB

**Requisitos Relacionados:** RF01, RF04, RF10

**Protótipo de Tela:**
[Link para o protótipo do cadastro de dispositivos](./docs/Projeto/Protótipos/cadastro-dispositivo.png)

---

### UC03 - Gerenciar Funcionários

**Descrição:** Permite cadastrar, consultar, atualizar e excluir funcionários.

**Atores:** Administrador

**Pré-condições:** 
- O usuário deve estar autenticado como administrador.

**Pós-condições:**
- Funcionários são criados, atualizados ou excluídos no sistema.
- Registro de log da operação realizada.

**Fluxo Principal:**
1. O administrador acessa o módulo de funcionários.
2. O sistema apresenta a lista de funcionários cadastrados.
3. O administrador seleciona a operação desejada (cadastrar, visualizar, editar, excluir).
4. Para cadastro/edição, o sistema exibe formulário com os campos necessários.
5. O administrador preenche as informações (nome, setor, sala, etc.).
6. O sistema valida e salva as informações.
7. O sistema registra a operação no log de auditoria.

**Fluxo Alternativo 1:** Dados inválidos
1. O sistema destaca campos com erro e mostra mensagem explicativa.
2. O administrador corrige as informações.
3. O sistema valida novamente.
4. Se válido, o fluxo principal continua do passo 6.

**Fluxo Alternativo 2:** E-mail duplicado
1. O sistema notifica que o e-mail já está cadastrado para outro funcionário.
2. O administrador pode:
   a. Verificar o funcionário existente
   b. Usar outro e-mail
   c. Cancelar a operação
3. O sistema processa a opção escolhida.

**Fluxo Alternativo 3:** Exclusão de funcionário com dispositivos associados
1. O sistema alerta sobre a existência de dispositivos vinculados.
2. O administrador decide por:
   a. Continuar (desvinculando os dispositivos)
   b. Visualizar os dispositivos associados
   c. Cancelar a operação
3. O sistema processa a opção escolhida.

**Exemplo de Dados:**
- Nome: João da Silva
- E-mail: joao.silva@empresa.com
- Matrícula: F12345
- Cargo: Analista de Sistemas
- Setor: Tecnologia da Informação
- Sala: 302
- Andar: 3
- Ramal: 4567
- Data de Admissão: 15/03/2022
- Status: Ativo

**Requisitos Relacionados:** RF02

**Protótipo de Tela:**
[Link para o protótipo do cadastro de funcionários](./docs/Projeto/Protótipos/cadastro-funcionario.png)

---

### UC04 - Gerenciar Locais

**Descrição:** Permite cadastrar, consultar, atualizar e excluir locais físicos onde os dispositivos podem ser alocados.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.

**Pós-condições:**
- Locais são criados, atualizados ou excluídos no sistema.
- Registro de log da operação realizada.

**Fluxo Principal:**
1. O usuário acessa o módulo de locais.
2. O sistema apresenta a lista de locais cadastrados.
3. O usuário seleciona a operação desejada (cadastrar, visualizar, editar, excluir).
4. Para cadastro/edição, o sistema exibe formulário com campos necessários.
5. O usuário preenche as informações (nome do local, endereço, tipo de local, etc.).
6. O sistema valida e salva as informações.
7. O sistema registra a operação no log de auditoria.

**Fluxo Alternativo 1:** Dados inválidos
1. O sistema destaca campos com erro e mostra mensagem explicativa.
2. O usuário corrige as informações.
3. O sistema valida novamente.
4. Se válido, o fluxo principal continua do passo 6.

**Fluxo Alternativo 2:** Local já cadastrado
1. O sistema notifica a duplicidade (mesmo nome/endereço).
2. O usuário pode:
   a. Cancelar a operação
   b. Atualizar o existente
   c. Verificar o local existente
3. O sistema processa a opção escolhida.

**Fluxo Alternativo 3:** Exclusão de local com dispositivos associados
1. O sistema alerta sobre a existência de dispositivos vinculados ao local.
2. O usuário pode:
   a. Cancelar a exclusão
   b. Transferir os dispositivos para outro local e continuar
   c. Visualizar dispositivos associados
3. O usuário confirma a ação escolhida.
4. O sistema processa a operação.

**Fluxo Alternativo 4:** Estrutura hierárquica de locais
1. O usuário indica que o local é subordinado a outro local existente.
2. O sistema exibe lista de locais que podem ser selecionados como superior.
3. O usuário seleciona o local superior.
4. O sistema estabelece a relação hierárquica.

**Exemplo de Dados:**
- Nome: Escritório Central
- Tipo: Filial
- Endereço: Av. Paulista, 1000
- Complemento: 10º andar
- Cidade: São Paulo
- Estado: SP
- CEP: 01310-100
- Responsável: João Silva
- Telefone: (11) 3333-4444
- Sublocais: Sala de TI, Sala de Reuniões, Recepção
- Observações: Acesso restrito após 18h

**Requisitos Relacionados:** RF03, RF05, RF06

**Protótipo de Tela:**
[Link para o protótipo do cadastro de locais](./docs/Projeto/Protótipos/cadastro-local.png)

---

### UC05 - Associar Dispositivo a Usuário

**Descrição:** Permite vincular dispositivos a funcionários específicos.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.
- O dispositivo deve estar cadastrado no sistema.
- O funcionário deve estar cadastrado no sistema.
- O dispositivo deve estar com status "Disponível".

**Pós-condições:**
- O dispositivo fica associado ao funcionário.
- O status do dispositivo é alterado para "Em Uso".
- Um registro de movimentação é criado no histórico.
- Termo de responsabilidade é gerado.

**Fluxo Principal:**
1. O usuário acessa o módulo de dispositivos.
2. O usuário seleciona um dispositivo específico.
3. O usuário seleciona a opção "Associar a Funcionário".
4. O sistema exibe a lista de funcionários disponíveis.
5. O usuário seleciona o funcionário.
6. O sistema solicita a finalidade da associação e observações.
7. O sistema registra a associação, cria entrada no histórico e gera termo.
8. O sistema altera o status do dispositivo para "Em Uso".

**Fluxo Alternativo 1:** Dispositivo já associado
1. O sistema exibe alerta sobre associação atual.
2. O usuário pode:
   a. Cancelar operação
   b. Confirmar a transferência
   c. Visualizar histórico atual
3. Em caso de transferência, o sistema registra a devolução do dispositivo anterior.
4. O fluxo principal continua do passo 4.

**Fluxo Alternativo 2:** Funcionário inativo
1. O sistema alerta que o funcionário selecionado está inativo.
2. O usuário pode:
   a. Selecionar outro funcionário
   b. Solicitar reativação do funcionário
   c. Cancelar a operação
3. O sistema processa a opção escolhida.

**Fluxo Alternativo 3:** Limite de dispositivos por usuário atingido
1. O sistema verifica o limite de dispositivos por tipo permitido para o funcionário.
2. Se o limite for atingido, o sistema notifica o usuário.
3. O usuário pode:
   a. Selecionar outro funcionário
   b. Solicitar exceção (requer aprovação)
   c. Cancelar a operação
4. O sistema processa a opção escolhida.

**Exemplo de Dados:**
- Dispositivo: Notebook Dell Latitude 5420, Tombo: 2023001, Status: Disponível
- Funcionário: João Silva, Setor: TI, Sala: 302
- Finalidade: Trabalho remoto
- Observações: Equipamento para desenvolvimento de software
- Data da Associação: 15/06/2023
- Responsável: Maria Costa (Técnica de TI)

**Requisitos Relacionados:** RF03, RF06

**Protótipo de Tela:**
[Link para o protótipo de associação de dispositivo](./docs/Projeto/Protótipos/associar-dispositivo.png)

---

### UC06 - Atualizar Status de Dispositivo

**Descrição:** Permite alterar o status operacional de um dispositivo.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.
- O dispositivo deve estar cadastrado no sistema.

**Pós-condições:**
- O status do dispositivo é atualizado.
- Um registro de alteração é criado no histórico.

**Fluxo Principal:**
1. O usuário acessa o módulo de dispositivos.
2. O usuário seleciona um dispositivo específico.
3. O usuário seleciona a opção "Alterar Status".
4. O sistema exibe os possíveis status (Ativo, Em Manutenção, Inativo, etc.).
5. O usuário seleciona o novo status e adiciona observações.
6. O sistema registra a alteração e cria entrada no histórico.

**Fluxo Alternativo 1:** Status incompatível com a situação atual
1. O sistema alerta sobre possíveis incompatibilidades.
   - Ex: Não é possível alterar para "Disponível" um dispositivo associado a um usuário.
2. O sistema sugere ações complementares:
   - Ex: Para status "Em Manutenção", sugerir remover associação com usuário.
3. O usuário confirma ou cancela a operação.
4. Se confirmado com ações complementares, o sistema realiza todas as atualizações necessárias.

**Fluxo Alternativo 2:** Status "Descartado" ou "Roubado/Perdido"
1. O sistema solicita documentação comprobatória (laudo técnico, B.O., etc.).
2. O usuário fornece informações adicionais obrigatórias:
   - Para "Descartado": Motivo, laudo técnico, data, responsável
   - Para "Roubado/Perdido": Data do ocorrido, número do B.O., circunstâncias
3. O sistema requer aprovação de nível superior (apenas Administrador).
4. O sistema registra todas as informações e evidências no histórico.

**Fluxo Alternativo 3:** Status "Em Garantia"
1. O sistema verifica se o dispositivo ainda possui garantia válida.
2. Se sim, o sistema solicita:
   - Número do chamado com fabricante
   - Data prevista de retorno
   - Descrição do problema
3. Se não, o sistema sugere alterar para "Em Manutenção" em vez de "Em Garantia".
4. O sistema registra todas as informações no histórico.

**Exemplo de Dados:**
- Dispositivo: Monitor Dell P2419H, Tombo: 2023015
- Status Atual: Ativo
- Novo Status: Em Manutenção
- Motivo: Falha intermitente na imagem
- Previsão de Retorno: 25/06/2023
- Responsável pela Alteração: Carlos Santos (Técnico)
- Observações: Enviado para assistência técnica autorizada

**Requisitos Relacionados:** RF04, RF06

**Protótipo de Tela:**
[Link para o protótipo de alteração de status](./docs/Projeto/Protótipos/alterar-status.png)

---

### UC07 - Visualizar Dispositivos

**Descrição:** Permite consultar a lista de dispositivos com filtros diversos.

**Atores:** Administrador, Técnico, Colaborador

**Pré-condições:** 
- O usuário deve estar autenticado.

**Pós-condições:**
- Exibição dos dispositivos conforme os filtros aplicados.

**Fluxo Principal:**
1. O usuário acessa o módulo de dispositivos.
2. O sistema exibe a lista de dispositivos conforme o perfil do usuário:
   - Administrador/Técnico: Todos os dispositivos
   - Colaborador: Apenas seus dispositivos
3. O usuário pode aplicar filtros (setor, status, tipo, etc.).
4. O sistema atualiza a lista conforme os filtros.
5. O usuário pode selecionar um dispositivo para visualizar detalhes.

**Fluxo Alternativo 1:** Nenhum dispositivo encontrado
1. O sistema exibe mensagem informativa.
2. O usuário pode ajustar os filtros.
3. O sistema oferece sugestões de filtros menos restritivos.

**Fluxo Alternativo 2:** Exportação da lista
1. O usuário seleciona a opção "Exportar".
2. O sistema oferece formatos (PDF, CSV, Excel).
3. O usuário escolhe o formato desejado.
4. O sistema gera e disponibiliza o arquivo para download.

**Fluxo Alternativo 3:** Visualização em mapa
1. O usuário seleciona a opção "Visualizar em Mapa".
2. O sistema exibe mapa do prédio com localização dos dispositivos.
3. O usuário pode filtrar por andar e setor.
4. O sistema atualiza o mapa conforme os filtros.

**Exemplo de Dados:**
- Filtros aplicados: 
  - Tipo: Notebook
  - Status: Ativo
  - Setor: Tecnologia da Informação
  - Período de Aquisição: 01/01/2023 a 30/06/2023
- Resultados: 15 dispositivos encontrados
- Ordenação: Por data de aquisição (mais recente primeiro)

**Requisitos Relacionados:** RF05, RF09, RF10

**Protótipo de Tela:**
[Link para o protótipo da listagem de dispositivos](./docs/Projeto/Protótipos/listar-dispositivos.png)

---

### UC08 - Consultar Histórico de Movimentações

**Descrição:** Permite visualizar o histórico de movimentações e alterações de status dos dispositivos.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.
- O dispositivo deve estar cadastrado no sistema.

**Pós-condições:**
- Exibição do histórico de movimentações do dispositivo.

**Fluxo Principal:**
1. O usuário acessa o módulo de dispositivos.
2. O usuário seleciona um dispositivo específico.
3. O usuário seleciona a opção "Histórico".
4. O sistema exibe a lista cronológica de eventos relacionados ao dispositivo:
   - Cadastro inicial
   - Associações a funcionários
   - Alterações de status
   - Manutenções
   - Movimentações físicas
5. O usuário pode filtrar o histórico por tipo de evento, data ou responsável.

**Fluxo Alternativo 1:** Sem histórico disponível
1. O sistema exibe mensagem informativa.
2. O sistema sugere verificar se o dispositivo foi recém-cadastrado.

**Fluxo Alternativo 2:** Exportação do histórico
1. O usuário seleciona a opção "Exportar Histórico".
2. O sistema oferece formatos (PDF, CSV).
3. O usuário escolhe o formato desejado.
4. O sistema gera e disponibiliza o arquivo para download.

**Fluxo Alternativo 3:** Comparação de estados
1. O usuário seleciona dois eventos do histórico.
2. O sistema apresenta uma comparação lado a lado das informações.
3. O sistema destaca as diferenças entre os dois estados.

**Exemplo de Dados:**
- Dispositivo: Notebook Dell Latitude 5420, Tombo: 2023001
- Histórico:
  1. 10/01/2023 - Cadastro inicial - Ana Oliveira (Administradora)
  2. 15/01/2023 - Configuração inicial - Pedro Santos (Técnico)
  3. 20/01/2023 - Associado a João Silva - Maria Costa (Técnica)
  4. 15/03/2023 - Manutenção preventiva - Carlos Santos (Técnico)
  5. 20/05/2023 - Atualização de software - Pedro Santos (Técnico)

**Requisitos Relacionados:** RF06

**Protótipo de Tela:**
[Link para o protótipo de histórico de dispositivo](./docs/Projeto/Protótipos/historico-dispositivo.png)

---

### UC09 - Gerar Relatórios

**Descrição:** Permite gerar relatórios com diferentes filtros e formatos.

**Atores:** Administrador, Técnico

**Pré-condições:** 
- O usuário deve estar autenticado com perfil adequado.

**Pós-condições:**
- Relatório gerado no formato escolhido.

**Fluxo Principal:**
1. O usuário acessa o módulo de relatórios.
2. O sistema exibe as opções de relatórios disponíveis:
   - Inventário geral
   - Dispositivos por setor
   - Dispositivos por status
   - Movimentações no período
   - Dispositivos próximos ao fim da garantia
   - Valor patrimonial total
3. O usuário seleciona o tipo de relatório e define filtros.
4. O usuário escolhe o formato de saída (PDF, CSV, Excel).
5. O sistema processa e disponibiliza o relatório para download.

**Fluxo Alternativo 1:** Erro na geração do relatório
1. O sistema exibe mensagem de erro específica.
2. O sistema sugere ajustes nos parâmetros:
   - Reduzir o período selecionado
   - Limitar o número de campos
   - Aplicar filtros adicionais
3. O usuário pode ajustar os parâmetros e tentar novamente.

**Fluxo Alternativo 2:** Programação de relatórios
1. O usuário seleciona a opção "Programar Relatório".
2. O sistema exibe opções de periodicidade (diário, semanal, mensal).
3. O usuário configura a programação e destinatários por email.
4. O sistema agenda a geração e envio automático do relatório.

**Fluxo Alternativo 3:** Visualização prévia
1. O usuário seleciona "Visualizar" antes de gerar o relatório final.
2. O sistema exibe uma prévia com amostra limitada de dados.
3. O usuário pode ajustar filtros ou formato.
4. O usuário confirma a geração do relatório completo.

**Exemplo de Dados:**
- Tipo de Relatório: Dispositivos por Setor
- Filtros:
  - Período: 01/01/2023 a 30/06/2023
  - Status: Ativo, Em Uso
  - Tipos: Notebooks, Desktops, Monitores
- Agrupamento: Por Setor > Por Tipo
- Formato: PDF
- Campos: Tombo, Tipo, Modelo, Funcionário, Data de Aquisição, Valor

**Requisitos Relacionados:** RF07

**Protótipo de Tela:**
[Link para o protótipo de geração de relatórios](./docs/Projeto/Protótipos/gerar-relatorios.png)

---

### UC10 - Gerenciar Perfis de Acesso

**Descrição:** Permite configurar os níveis de acesso dos usuários do sistema.

**Atores:** Administrador

**Pré-condições:** 
- O usuário deve estar autenticado como administrador.

**Pós-condições:**
- Permissões de usuários atualizadas.
- Registro de log da operação realizada.

**Fluxo Principal:**
1. O administrador acessa o módulo de usuários.
2. O sistema exibe a lista de usuários do sistema.
3. O administrador seleciona um usuário.
4. O sistema exibe os dados e o perfil atual do usuário.
5. O administrador seleciona o novo perfil (Administrador, Técnico, Colaborador).
6. O sistema atualiza as permissões do usuário.
7. O sistema registra a alteração no log de auditoria.

**Fluxo Alternativo 1:** Alteração do próprio perfil
1. O sistema impede a alteração para um perfil inferior.
2. O administrador recebe alerta e a operação é cancelada.
3. O sistema sugere que outro administrador faça a alteração.

**Fluxo Alternativo 2:** Perfil personalizado
1. O administrador seleciona "Criar Perfil Personalizado".
2. O sistema exibe lista de permissões disponíveis.
3. O administrador seleciona permissões específicas.
4. O administrador nomeia o novo perfil.
5. O sistema salva o perfil personalizado para uso futuro.

**Fluxo Alternativo 3:** Desativação de usuário
1. O administrador seleciona "Desativar Usuário".
2. O sistema verifica se o usuário possui dispositivos associados.
3. Se sim, o sistema alerta e sugere transferência.
4. O administrador confirma a desativação.
5. O sistema marca o usuário como inativo sem excluir o registro.

**Exemplo de Dados:**
- Usuário: maria.costa@empresa.com
- Nome: Maria Costa
- Perfil Atual: Técnico
- Novo Perfil: Administrador
- Permissões adicionadas:
  - Gerenciar usuários
  - Excluir registros
  - Configurar sistema
  - Gerar relatórios gerenciais
- Data da Alteração: 20/06/2023
- Responsável: João Silva (Administrador)

**Requisitos Relacionados:** RF08, RF09

**Protótipo de Tela:**
[Link para o protótipo de gerenciamento de perfis](./docs/Projeto/Protótipos/gerenciar-perfis.png)

---

### UC11 - Buscar Dispositivos

**Descrição:** Permite realizar busca avançada de dispositivos por diversos critérios.

**Atores:** Todos (com visões diferentes conforme perfil)

**Pré-condições:** 
- O usuário deve estar autenticado.

**Pós-condições:**
- Exibição dos resultados da busca.

**Fluxo Principal:**
1. O usuário acessa a função de busca.
2. O sistema exibe os campos de busca avançada:
   - Texto livre (busca em múltiplos campos)
   - Tipo de dispositivo
   - Período de aquisição
   - Status
   - Localização
   - Responsável
3. O usuário preenche um ou mais critérios.
4. O sistema exibe os resultados em tempo real à medida que o usuário digita.
5. O usuário pode refinar a busca ou selecionar um dispositivo.

**Fluxo Alternativo 1:** Busca por código QR/Tombo
1. O usuário seleciona "Escanear QR" ou digita código de tombo.
2. O sistema localiza o dispositivo específico.
3. O sistema exibe diretamente os detalhes do dispositivo.

**Fluxo Alternativo 2:** Nenhum resultado encontrado
1. O sistema exibe sugestões baseadas em termos similares.
2. O sistema sugere correção para possíveis erros de digitação.
3. O usuário pode reformular a busca ou usar filtros sugeridos.

**Fluxo Alternativo 3:** Salvar busca
1. O usuário seleciona "Salvar Busca".
2. O sistema solicita um nome para a busca salva.
3. O usuário fornece o nome.
4. O sistema salva os critérios para uso futuro.

**Exemplo de Dados:**
- Busca por: "notebook dell i7 2023"
- Critérios detectados automaticamente:
  - Tipo: Notebook
  - Marca: Dell
  - Processador: i7
  - Ano: 2023
- Resultados: 5 dispositivos encontrados

**Requisitos Relacionados:** RF05, RF10

**Protótipo de Tela:**
[Link para o protótipo de busca avançada](./docs/Projeto/Protótipos/busca-avancada.png)

---

## 6. Matriz de Rastreabilidade

| Caso de Uso | RF01 | RF02 | RF03 | RF04 | RF05 | RF06 | RF07 | RF08 | RF09 | RF10 | RF11 | RF12 |
|-------------|------|------|------|------|------|------|------|------|------|------|------|------|
| UC01        |      |      |      |      |      |      |      |  X   |  X   |      |      |      |
| UC02        |  X   |      |      |  X   |      |      |      |      |      |  X   |      |      |
| UC03        |      |  X   |      |      |      |      |      |      |      |      |      |      |
| UC04        |      |      |  X   |      |      |  X   |      |      |      |      |      |      |
| UC05        |      |      |      |  X   |      |  X   |      |      |      |      |      |      |
| UC06        |      |      |      |      |  X   |      |      |      |  X   |  X   |      |      |
| UC07        |      |      |      |      |      |  X   |      |      |      |      |      |      |
| UC08        |      |      |      |      |  X   |      |  X   |      |      |      |      |      |
| UC09        |      |      |      |      |      |      |      |  X   |  X   |      |      |      |
| UC10        |      |      |      |      |  X   |      |      |      |      |  X   |      |      |
| UC11        |      |      |  X   |      |      |  X   |      |      |      |      |      |      |
| UC12        |      |      |      |      |  X   |      |      |      |      |      |      |  X   |

---

## 7. Glossário de Termos

| Termo          | Descrição                                                                     |
|----------------|-------------------------------------------------------------------------------|
| Tombo          | Número de patrimônio único atribuído a cada dispositivo                       |
| Status         | Estado operacional atual do dispositivo (Ativo, Em Manutenção, etc.)          |
| Movimentação   | Qualquer alteração na localização, atribuição ou estado de um dispositivo     |
| Termo de Resp. | Documento que formaliza a entrega de um dispositivo a um funcionário          |
| Dashboard      | Painel visual com indicadores e estatísticas do sistema                       |
| Perfil         | Conjunto de permissões atribuídas a um usuário do sistema                     |
| Token JWT      | JSON Web Token - mecanismo de autenticação segura baseado em tokens           |

---

## 8. Referências

- [Documento de Visão](./visao.md)
- [Documento de Requisitos](./requisitos.md)
- [Documentação Vue.js](https://vuejs.org/guide/introduction.html)
- [Documentação NestJS](https://docs.nestjs.com/)