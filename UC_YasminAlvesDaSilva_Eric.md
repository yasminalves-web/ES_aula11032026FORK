# Documento de Casos de Uso – FitPass Gym Management

---

## UC01 — Realizar Login

### Ator Principal
Usuário (Aluno, Recepcionista, Instrutor, Gerente)

### Objetivo
Permitir que o usuário acesse o sistema com suas credenciais.

### Pré-condições
- Usuário deve possuir cadastro ativo no sistema.

### Pós-condições
- Sessão iniciada com sucesso e usuário redirecionado à tela inicial de acordo com seu perfil.

### Fluxo Principal
1. O usuário acessa a tela de login.
2. O usuário informa e-mail e senha.
3. O sistema valida as credenciais.
4. O sistema autentica o usuário e redireciona para a tela inicial conforme o perfil.

### Fluxos Alternativos
- **A1 — Credenciais inválidas:**  
  O sistema exibe mensagem de erro informando que e-mail ou senha estão incorretos.

- **A2 — Conta bloqueada por inadimplência:**  
  O sistema impede o login do aluno e exibe mensagem orientando a regularizar pagamentos.

- **A3 — Esqueceu a senha:**  
  O usuário solicita redefinição de senha via e-mail cadastrado.

### RF Relacionados
- RF04 — Regularidade do Aluno

### RNF Relacionados
- RNF02 — Segurança
- RNF03 — Performance

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC02 — Cadastrar Aluno

### Ator Principal
Recepcionista

### Objetivo
Registrar um novo aluno no sistema com todos os dados necessários.

### Pré-condições
- Recepcionista deve estar autenticado no sistema.
- Dados pessoais do aluno devem estar disponíveis.

### Pós-condições
- Aluno cadastrado com status ativo e plano vinculado.

### Fluxo Principal
1. A recepcionista acessa o módulo de cadastro de alunos.
2. O sistema exibe o formulário de cadastro.
3. A recepcionista preenche os dados pessoais, contato, endereço e seleciona o plano contratado.
4. O sistema valida os dados informados.
5. O sistema registra o aluno e gera o cartão RFID para controle de acesso.
6. O sistema confirma o cadastro com mensagem de sucesso.

### Fluxos Alternativos
- **A1 — Dados obrigatórios não preenchidos:**  
  O sistema destaca os campos obrigatórios e solicita preenchimento antes de salvar.

- **A2 — CPF já cadastrado:**  
  O sistema informa que o CPF já existe e impede duplicidade.

### RF Relacionados
- RF01 — Cadastro de Alunos
- RF05 — Controle de Acesso

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC03 — Gerenciar Planos

### Ator Principal
Gerente

### Objetivo
Criar, editar, ativar ou desativar planos disponíveis na academia.

### Pré-condições
- Gerente deve estar autenticado no sistema.

### Pós-condições
- Plano criado, atualizado ou com status alterado conforme ação realizada.

### Fluxo Principal
1. O gerente acessa o módulo de gerenciamento de planos.
2. O sistema lista todos os planos cadastrados.
3. O gerente escolhe a ação: criar novo plano, editar, ativar ou desativar.
4. O gerente preenche ou altera os dados do plano (nome, valor, duração, modalidade).
5. O sistema valida e salva as alterações.
6. O sistema confirma a operação com mensagem de sucesso.

### Fluxos Alternativos
- **A1 — Plano com alunos vinculados sendo desativado:**  
  O sistema alerta que há alunos ativos nesse plano e solicita confirmação antes de prosseguir.

- **A2 — Dados inválidos no formulário:**  
  O sistema exibe mensagem de erro e impede o salvamento.

### RF Relacionados
- RF02 — Gerenciamento de Planos

### RNF Relacionados
- RNF04 — Usabilidade
- RNF05 — Escalabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC04 — Registrar Pagamento

### Ator Principal
Recepcionista

### Objetivo
Registrar o pagamento de mensalidade de um aluno.

### Pré-condições
- Recepcionista autenticada no sistema.
- Aluno deve estar cadastrado no sistema.

### Pós-condições
- Pagamento registrado e situação do aluno atualizada para regular.

### Fluxo Principal
1. A recepcionista acessa o módulo de pagamentos.
2. Busca o aluno pelo nome ou CPF.
3. O sistema exibe a mensalidade em aberto.
4. A recepcionista seleciona a forma de pagamento (dinheiro, cartão ou PIX).
5. O sistema registra o pagamento.
6. O sistema atualiza automaticamente a situação do aluno para regular.
7. O sistema emite comprovante de pagamento.

### Fluxos Alternativos
- **A1 — Tentativa de pagamento parcial:**  
  O sistema rejeita e informa que o pagamento deve ser integral.

- **A2 — Aluno não encontrado:**  
  O sistema exibe mensagem informando que o aluno não foi localizado.

### RF Relacionados
- RF03 — Controle de Pagamentos
- RF04 — Regularidade do Aluno

### RNF Relacionados
- RNF02 — Segurança
- RNF03 — Performance

### RN Relacionadas
- RN04 — Pagamento parcial
- RN07 — Atualização automática da regularidade

---

## UC05 — Validar Acesso pela Catraca

### Ator Principal
Sistema de Catraca (API externa)

### Objetivo
Liberar ou bloquear a entrada do aluno na academia via RFID.

### Pré-condições
- Sistema de catraca integrado via API REST.
- Aluno com cartão RFID cadastrado.

### Pós-condições
- Acesso liberado ou bloqueado conforme a situação do aluno.

### Fluxo Principal
1. O aluno aproxima o cartão RFID da catraca.
2. O sistema de catraca envia o código RFID via API para o sistema FitPass.
3. O sistema verifica se o aluno está cadastrado e com mensalidade em dia.
4. O sistema retorna autorização de acesso.
5. A catraca libera a passagem.
6. O sistema registra o acesso no histórico do aluno.

### Fluxos Alternativos
- **A1 — Aluno inadimplente:**  
  O sistema retorna bloqueio; a catraca permanece fechada e exibe aviso.

- **A2 — RFID não reconhecido:**  
  O sistema retorna erro; a catraca permanece fechada.

### RF Relacionados
- RF05 — Controle de Acesso
- RF04 — Regularidade do Aluno

### RNF Relacionados
- RNF03 — Performance
- RNF06 — Integração

### RN Relacionadas
- RN01 — Bloqueio por inadimplência

---

## UC06 — Agendar Aula

### Ator Principal
Aluno

### Objetivo
Reservar uma vaga em uma aula disponível na academia.

### Pré-condições
- Aluno autenticado no sistema.
- Aluno com mensalidade em dia.
- Existir vagas disponíveis na aula desejada.

### Pós-condições
- Vaga reservada e confirmação enviada ao aluno.

### Fluxo Principal
1. O aluno acessa o módulo de agendamento de aulas.
2. O sistema exibe a grade de horários disponíveis.
3. O aluno seleciona a aula desejada.
4. O sistema verifica a disponibilidade de vagas.
5. O sistema confirma a reserva e registra o agendamento.
6. O sistema envia notificação de confirmação ao aluno.

### Fluxos Alternativos
- **A1 — Aula sem vagas:**  
  O sistema informa que a aula está lotada e bloqueia novo agendamento.

- **A2 — Aluno inadimplente:**  
  O sistema bloqueia o agendamento e orienta a regularizar o pagamento.

### RF Relacionados
- RF06 — Agendamento de Aulas
- RF10 — Notificações

### RNF Relacionados
- RNF04 — Usabilidade
- RNF03 — Performance

### RN Relacionadas
- RN02 — Limite de vagas
- RN01 — Bloqueio por inadimplência

---

## UC07 — Cancelar Agendamento de Aula

### Ator Principal
Aluno

### Objetivo
Cancelar uma reserva previamente feita em uma aula.

### Pré-condições
- Aluno autenticado no sistema.
- Aluno deve possuir um agendamento ativo.
- O cancelamento deve ser feito com pelo menos 1 hora de antecedência.

### Pós-condições
- Reserva cancelada e vaga liberada para outros alunos.

### Fluxo Principal
1. O aluno acessa seus agendamentos.
2. O sistema lista as aulas agendadas.
3. O aluno seleciona a aula que deseja cancelar.
4. O sistema verifica se o cancelamento ainda é permitido pelo prazo.
5. O sistema cancela a reserva e libera a vaga.
6. O sistema confirma o cancelamento ao aluno.

### Fluxos Alternativos
- **A1 — Cancelamento fora do prazo:**  
  O sistema informa que não é possível cancelar com menos de 1 hora de antecedência.

### RF Relacionados
- RF06 — Agendamento de Aulas

### RNF Relacionados
- RNF04 — Usabilidade

### RN Relacionadas
- RN03 — Cancelamento de agendamento

---

## UC08 — Registrar Presença em Aula

### Ator Principal
Instrutor

### Objetivo
Registrar a presença dos alunos em uma aula ministrada.

### Pré-condições
- Instrutor autenticado no sistema.
- Aula deve estar em andamento ou recém-encerrada.

### Pós-condições
- Presença dos alunos registrada no sistema.

### Fluxo Principal
1. O instrutor acessa o módulo de lista de presença.
2. O sistema exibe a lista de alunos agendados para a aula.
3. O instrutor marca os alunos presentes.
4. O sistema salva as presenças registradas.
5. O sistema confirma o registro com mensagem de sucesso.

### Fluxos Alternativos
- **A1 — Aluno presente mas sem agendamento:**  
  O instrutor pode registrar presença avulsa, com observação no sistema.

### RF Relacionados
- RF07 — Lista de Presença

### RNF Relacionados
- RNF04 — Usabilidade
- RNF03 — Performance

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC09 — Realizar Avaliação Física

### Ator Principal
Instrutor

### Objetivo
Registrar os dados da avaliação física de um aluno.

### Pré-condições
- Instrutor autenticado no sistema.
- Aluno deve estar ativo e com mensalidade em dia.

### Pós-condições
- Avaliação física registrada e histórico do aluno atualizado.

### Fluxo Principal
1. O instrutor acessa o módulo de avaliações físicas.
2. Busca o aluno pelo nome ou CPF.
3. O sistema verifica que o aluno está ativo e regular.
4. O instrutor preenche os dados da avaliação (peso, altura, IMC, percentual de gordura etc.).
5. O instrutor pode anexar arquivos complementares.
6. O sistema salva a avaliação e atualiza o histórico do aluno.

### Fluxos Alternativos
- **A1 — Aluno inadimplente:**  
  O sistema bloqueia o registro e exibe mensagem informando que o aluno não está regular.

- **A2 — Aluno inativo:**  
  O sistema bloqueia o registro e informa que o aluno está inativo.

### RF Relacionados
- RF08 — Avaliação Física

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN05 — Avaliação física
- RN06 — Acesso restrito por perfil

---

## UC10 — Emitir Relatório de Inadimplência

### Ator Principal
Gerente

### Objetivo
Visualizar a lista de alunos com mensalidades em atraso.

### Pré-condições
- Gerente autenticado no sistema.

### Pós-condições
- Relatório de inadimplência gerado e disponível para visualização ou exportação.

### Fluxo Principal
1. O gerente acessa o módulo de relatórios.
2. Seleciona o relatório de inadimplência.
3. O gerente pode filtrar por período ou unidade.
4. O sistema processa os dados e exibe a lista de alunos inadimplentes.
5. O gerente pode exportar o relatório em PDF ou planilha.

### Fluxos Alternativos
- **A1 — Nenhum aluno inadimplente no período:**  
  O sistema exibe mensagem informando que não há registros de inadimplência.

### RF Relacionados
- RF09 — Relatórios Gerenciais

### RNF Relacionados
- RNF03 — Performance
- RNF05 — Escalabilidade

### RN Relacionadas
- RN01 — Bloqueio por inadimplência
- RN06 — Acesso restrito por perfil

---

## UC11 — Emitir Relatório de Alunos Ativos

### Ator Principal
Gerente

### Objetivo
Visualizar a lista de alunos ativos na academia.

### Pré-condições
- Gerente autenticado no sistema.

### Pós-condições
- Relatório de alunos ativos gerado com sucesso.

### Fluxo Principal
1. O gerente acessa o módulo de relatórios.
2. Seleciona o relatório de alunos ativos.
3. O sistema exibe os alunos com cadastro e mensalidade ativos.
4. O gerente pode filtrar por plano ou unidade.
5. O gerente pode exportar o relatório.

### Fluxos Alternativos
- **A1 — Nenhum aluno ativo no filtro selecionado:**  
  O sistema informa que não foram encontrados registros.

### RF Relacionados
- RF09 — Relatórios Gerenciais

### RNF Relacionados
- RNF03 — Performance
- RNF05 — Escalabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC12 — Consultar Histórico de Acessos

### Ator Principal
Gerente

### Objetivo
Visualizar o histórico de entradas e saídas dos alunos na academia.

### Pré-condições
- Gerente autenticado no sistema.

### Pós-condições
- Relatório de histórico de acessos exibido com sucesso.

### Fluxo Principal
1. O gerente acessa o módulo de relatórios.
2. Seleciona o relatório de histórico de acessos.
3. O sistema exibe os registros de acesso com data, hora e identificação do aluno.
4. O gerente pode filtrar por aluno, período ou unidade.
5. O gerente pode exportar o relatório.

### Fluxos Alternativos
- **A1 — Nenhum acesso registrado no período:**  
  O sistema informa que não há registros para os filtros selecionados.

### RF Relacionados
- RF09 — Relatórios Gerenciais
- RF05 — Controle de Acesso

### RNF Relacionados
- RNF03 — Performance

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC13 — Consultar Ocupação das Aulas

### Ator Principal
Gerente

### Objetivo
Visualizar a taxa de ocupação das aulas por período.

### Pré-condições
- Gerente autenticado no sistema.

### Pós-condições
- Relatório de ocupação das aulas gerado com sucesso.

### Fluxo Principal
1. O gerente acessa o módulo de relatórios.
2. Seleciona o relatório de ocupação de aulas.
3. O gerente filtra por período, modalidade ou instrutor.
4. O sistema exibe a taxa de ocupação de cada aula.
5. O gerente pode exportar o relatório.

### Fluxos Alternativos
- **A1 — Nenhuma aula no período selecionado:**  
  O sistema informa que não há registros para o período.

### RF Relacionados
- RF09 — Relatórios Gerenciais
- RF06 — Agendamento de Aulas

### RNF Relacionados
- RNF03 — Performance
- RNF05 — Escalabilidade

### RN Relacionadas
- RN02 — Limite de vagas
- RN06 — Acesso restrito por perfil

---

## UC14 — Enviar Notificação de Vencimento de Mensalidade

### Ator Principal
Sistema (automático)

### Objetivo
Notificar o aluno sobre o vencimento próximo ou ocorrido da mensalidade.

### Pré-condições
- Aluno com cadastro ativo e e-mail/telefone registrado.
- Mensalidade com vencimento próximo ou vencida.

### Pós-condições
- Notificação enviada ao aluno com sucesso.

### Fluxo Principal
1. O sistema verifica diariamente as mensalidades próximas do vencimento.
2. Para cada aluno com vencimento em até 3 dias, o sistema envia notificação de aviso.
3. Para mensalidades já vencidas, o sistema envia notificação de cobrança.
4. O sistema registra o envio da notificação no histórico do aluno.

### Fluxos Alternativos
- **A1 — Falha no envio da notificação:**  
  O sistema registra a falha e agenda nova tentativa.

### RF Relacionados
- RF10 — Notificações
- RF04 — Regularidade do Aluno

### RNF Relacionados
- RNF01 — Disponibilidade

### RN Relacionadas
- RN01 — Bloqueio por inadimplência

---

## UC15 — Enviar Notificação de Confirmação de Agendamento

### Ator Principal
Sistema (automático)

### Objetivo
Notificar o aluno sobre a confirmação de uma reserva em aula.

### Pré-condições
- Aluno deve ter realizado um agendamento.
- Aluno com e-mail ou telefone cadastrado.

### Pós-condições
- Notificação de confirmação enviada ao aluno.

### Fluxo Principal
1. Após o aluno concluir um agendamento, o sistema dispara automaticamente uma notificação.
2. A notificação inclui nome da aula, data, horário e instrutor responsável.
3. O sistema registra o envio no histórico.

### Fluxos Alternativos
- **A1 — Falha no envio:**  
  O sistema registra o erro e realiza nova tentativa.

### RF Relacionados
- RF10 — Notificações
- RF06 — Agendamento de Aulas

### RNF Relacionados
- RNF01 — Disponibilidade

### RN Relacionadas
- RN03 — Cancelamento de agendamento

---

## UC16 — Notificar Liberação de Avaliação Física

### Ator Principal
Sistema (automático)

### Objetivo
Notificar o aluno quando uma nova avaliação física estiver disponível.

### Pré-condições
- Aluno ativo e regular.
- Período mínimo desde a última avaliação atingido.

### Pós-condições
- Aluno notificado sobre a disponibilidade de nova avaliação física.

### Fluxo Principal
1. O sistema verifica periodicamente se algum aluno está apto a realizar nova avaliação.
2. Para os alunos elegíveis, o sistema envia notificação informando a disponibilidade.
3. O sistema registra o envio no histórico do aluno.

### Fluxos Alternativos
- **A1 — Aluno inadimplente:**  
  O sistema não envia a notificação até que a situação seja regularizada.

### RF Relacionados
- RF10 — Notificações
- RF08 — Avaliação Física

### RNF Relacionados
- RNF01 — Disponibilidade

### RN Relacionadas
- RN05 — Avaliação física

---

## UC17 — Editar Cadastro de Aluno

### Ator Principal
Recepcionista

### Objetivo
Atualizar os dados cadastrais de um aluno já registrado no sistema.

### Pré-condições
- Recepcionista autenticada no sistema.
- Aluno deve estar cadastrado.

### Pós-condições
- Dados do aluno atualizados com sucesso.

### Fluxo Principal
1. A recepcionista acessa o módulo de cadastro de alunos.
2. Busca o aluno pelo nome ou CPF.
3. O sistema exibe os dados atuais do aluno.
4. A recepcionista edita os campos necessários.
5. O sistema valida os dados e salva as alterações.
6. O sistema confirma a atualização.

### Fluxos Alternativos
- **A1 — Aluno não encontrado:**  
  O sistema informa que o aluno não foi localizado.

- **A2 — Dados inválidos:**  
  O sistema destaca os campos com erro e impede o salvamento.

### RF Relacionados
- RF01 — Cadastro de Alunos

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC18 — Inativar Aluno

### Ator Principal
Recepcionista

### Objetivo
Inativar o cadastro de um aluno que deixou de ser membro da academia.

### Pré-condições
- Recepcionista autenticada no sistema.
- Aluno deve estar cadastrado e ativo.

### Pós-condições
- Aluno com status inativo; acesso à academia bloqueado.

### Fluxo Principal
1. A recepcionista acessa o módulo de cadastro de alunos.
2. Busca o aluno pelo nome ou CPF.
3. O sistema exibe os dados do aluno.
4. A recepcionista seleciona a opção de inativar cadastro.
5. O sistema solicita confirmação da ação.
6. Após confirmação, o sistema inativa o aluno e bloqueia o RFID.

### Fluxos Alternativos
- **A1 — Aluno com agendamentos futuros:**  
  O sistema alerta sobre os agendamentos existentes e solicita confirmação para cancelá-los antes de inativar.

### RF Relacionados
- RF01 — Cadastro de Alunos
- RF05 — Controle de Acesso

### RNF Relacionados
- RNF02 — Segurança

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC19 — Consultar Histórico de Avaliações Físicas

### Ator Principal
Instrutor / Aluno

### Objetivo
Visualizar o histórico completo de avaliações físicas de um aluno.

### Pré-condições
- Usuário autenticado no sistema.
- Aluno deve possuir ao menos uma avaliação física registrada.

### Pós-condições
- Histórico de avaliações exibido com sucesso.

### Fluxo Principal
1. O instrutor ou aluno acessa o módulo de avaliações físicas.
2. O instrutor busca o aluno (caso seja o próprio aluno, o sistema exibe diretamente seu histórico).
3. O sistema lista as avaliações em ordem cronológica.
4. O usuário pode selecionar uma avaliação para ver os detalhes completos.
5. O usuário pode baixar arquivos anexados às avaliações.

### Fluxos Alternativos
- **A1 — Nenhuma avaliação registrada:**  
  O sistema informa que não há avaliações no histórico.

### RF Relacionados
- RF08 — Avaliação Física

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN05 — Avaliação física
- RN06 — Acesso restrito por perfil

---

## UC20 — Consultar Grade de Horários das Aulas

### Ator Principal
Aluno

### Objetivo
Visualizar os horários e detalhes das aulas disponíveis na academia.

### Pré-condições
- Aluno autenticado no sistema.

### Pós-condições
- Grade de horários exibida com sucesso.

### Fluxo Principal
1. O aluno acessa o módulo de agendamento de aulas.
2. O sistema exibe a grade completa de horários disponíveis.
3. O aluno pode filtrar por modalidade, instrutor ou dia da semana.
4. O sistema exibe as informações de cada aula: nome, horário, instrutor, vagas disponíveis.
5. O aluno pode iniciar um agendamento diretamente a partir da grade.

### Fluxos Alternativos
- **A1 — Nenhuma aula disponível no filtro selecionado:**  
  O sistema informa que não há aulas para os filtros aplicados.

### RF Relacionados
- RF06 — Agendamento de Aulas

### RNF Relacionados
- RNF04 — Usabilidade
- RNF03 — Performance

### RN Relacionadas
- RN02 — Limite de vagas
