# Identificação de Riscos

Registro **inicial** de riscos do projeto do aplicativo de agendamento de consultas médicas, produzido na fase de **planejamento e estruturação**, antes do início do desenvolvimento. Não há, portanto, sprint executada nem dado real de produção — os riscos abaixo foram antecipados a partir de experiência prévia da equipe e de projetos similares, e serão recalibrados assim que houver histórico de execução.

**Técnicas utilizadas:** workshop de brainstorming com o time recém-formado, revisão de lições aprendidas de projetos anteriores de integração com sistemas de saúde, análise preliminar da EAP (ainda em rascunho) módulo a módulo, checklist de riscos de projetos de saúde digital e reunião exploratória inicial com o possível fornecedor do PEP.

**Categorias:** Técnico · Externo · Organizacional · Gerência de Projeto · Conformidade/Legal

---

## R-01 — Integração com o prontuário externo (PEP) ainda indefinida

- **Categoria:** Externo / Técnico
- **Causa raiz:** o modelo de integração com o sistema de prontuário eletrônico ainda não foi definido; até o momento houve apenas uma conversa exploratória com o fornecedor, sem documentação técnica de API nem contrato formal de nível de serviço.
- **Evento potencial:** ao iniciar a integração, a API se mostrar mal documentada, instável, ou o fornecedor não aceitar formalizar SLA e prazo de aviso para mudanças.
- **Consequência:** atraso já na primeira fase de desenvolvimento; necessidade de redesenhar a arquitetura de integração; risco de o agendamento depender de um sistema fora do controle do projeto.
- **Sinais de alerta a monitorar a partir do kickoff:** demora do fornecedor em disponibilizar documentação; recusa em assinar SLA; ambiente de homologação indisponível para testes.
- **Responsável:** Tech Lead de back-end (a confirmar na formação da equipe)

## R-02 — Escopo funcional ainda não consolidado (risco de scope creep futuro)

- **Categoria:** Gerência de Projeto
- **Causa raiz:** o levantamento de requisitos com a área médica está em andamento e ainda não há baseline funcional formalmente aprovada; não existe, até o momento, processo definido de controle de mudanças.
- **Evento potencial:** uma vez iniciado o desenvolvimento, novas validações e exceções de agendamento passarem a ser solicitadas diretamente à equipe, fora de um fluxo formal.
- **Consequência:** caso o processo de controle de mudanças não seja instituído antes do kickoff, o risco de atraso e retrabalho se torna praticamente certo já nas primeiras sprints.
- **Ação preventiva antes do início:** aprovar e assinar a baseline do MVP com a diretoria clínica antes da Sprint 1.
- **Responsável:** Gerente de Projetos / Product Owner (papel a ser definido)

## R-03 — Estimativas iniciais sem histórico de velocidade

- **Categoria:** Organizacional / Gerência de Projeto
- **Causa raiz:** por não haver sprint executada, qualquer estimativa de esforço nesta fase é necessariamente especulativa; a equipe ainda está sendo formada e é enxuta, com pessoas-chave únicas previstas em cada especialidade.
- **Evento potencial:** o planejamento inicial do cronograma ser construído sobre estimativas otimistas, gerando sobrecarga já nas primeiras sprints.
- **Consequência:** desgaste da equipe, queda de produtividade, aumento de defeitos, logo no início do projeto.
- **Ação preventiva antes do início:** tratar as três primeiras sprints como período de calibragem, sem compromissos externos de prazo firmados sobre elas.
- **Responsável:** Gerente de Projetos / Scrum Master (a definir)

## R-04 — Não conformidade com a LGPD no tratamento de dados de saúde

- **Categoria:** Conformidade / Legal
- **Causa raiz:** dados de saúde são dados pessoais sensíveis; nesta fase de planejamento, ainda não há DPO formalmente alocado ao projeto nem RIPD (Relatório de Impacto à Proteção de Dados) iniciado.
- **Evento potencial:** o desenvolvimento avançar sem que o fluxo de consentimento e a política de retenção tenham sido validados pelo jurídico, exigindo retrabalho de telas e de modelo de dados já construídos.
- **Consequência:** sanções da ANPD, dano reputacional para a clínica, possível bloqueio do lançamento se identificado tardiamente.
- **Ação preventiva antes do início:** confirmar a alocação do DPO e iniciar o RIPD em paralelo ao levantamento de requisitos, antes da primeira linha de código.
- **Responsável:** DPO (alocação pendente) com apoio do Tech Lead

## R-05 — Falha na entrega de notificações push e SMS

- **Categoria:** Técnico / Externo
- **Causa raiz:** dependência de provedores terceiros (FCM/APNs e gateway de SMS), permissões negadas pelo usuário no dispositivo e cadastros com telefone inválido.
- **Evento:** lembrete de consulta não chega ao paciente.
- **Consequência:** aumento do absenteísmo, que é justamente o principal indicador de valor do produto.
- **Gatilhos a observar após o início:** taxa de entrega abaixo de 90%; aumento de faltas registradas; erros no webhook do gateway.
- **Responsável:** Desenvolvedor mobile

## R-06 — Conflito de horários e overbooking na agenda médica

- **Categoria:** Técnico
- **Causa raiz:** concorrência entre múltiplos usuários agendando o mesmo slot, além de divergência de fuso e de regras de bloqueio.
- **Evento:** dois pacientes confirmam o mesmo horário com o mesmo profissional.
- **Consequência:** perda de confiança no aplicativo, atrito na recepção da clínica, necessidade de correção manual.
- **Gatilhos a observar após o início:** registros duplicados em banco; reclamações da recepção; falhas em testes de carga simultânea.
- **Responsável:** Tech Lead de back-end

## R-07 — Baixa adoção pelos usuários finais (pacientes e médicos)

- **Categoria:** Externo / Organizacional
- **Causa raiz:** público com faixa etária ampla e baixa familiaridade digital; médicos resistentes a abandonar a agenda em papel ou o sistema atual.
- **Evento:** o aplicativo é publicado, mas o volume de agendamentos digitais permanece baixo.
- **Consequência:** o benefício projetado não se concretiza e o investimento não se paga.
- **Gatilhos a observar após o início:** baixa taxa de conclusão de cadastro nos testes-piloto; feedback negativo de usabilidade; poucas agendas configuradas pelos médicos.
- **Responsável:** Product Owner

## R-08 — Rejeição da publicação nas lojas de aplicativos

- **Categoria:** Externo
- **Causa raiz:** políticas específicas de App Store e Google Play para aplicativos de saúde, exigência de política de privacidade e de justificativa de permissões.
- **Evento:** o build é rejeitado na revisão, próximo à data de lançamento.
- **Consequência:** atraso no go-live e replanejamento de comunicação de marketing.
- **Gatilhos a observar após o início:** ausência de política de privacidade publicada; permissões sem justificativa no manifesto; primeira submissão deixada para a última semana.
- **Responsável:** Desenvolvedor mobile

## R-09 — Dependência de pessoa-chave (fator caminhão)

- **Categoria:** Organizacional
- **Causa raiz:** apenas um desenvolvedor domina a camada de integração com o PEP; conhecimento não documentado.
- **Evento:** afastamento, férias ou desligamento dessa pessoa.
- **Consequência:** paralisação da frente mais crítica do projeto.
- **Gatilhos a observar após o início:** commits concentrados em um único autor por módulo; ausência de revisão cruzada de código; documentação técnica desatualizada.
- **Responsável:** Gerente de Projetos

## R-10 — Vazamento de dados por falha de segurança na aplicação

- **Categoria:** Técnico / Conformidade
- **Causa raiz:** ausência de teste de segurança automatizado na esteira; armazenamento local de token no dispositivo; APIs sem limitação de taxa.
- **Evento:** exploração de vulnerabilidade que expõe dados de pacientes.
- **Consequência:** incidente de segurança de gravidade máxima, com notificação obrigatória à ANPD e aos titulares.
- **Gatilhos a observar após o início:** achados em análise estática; dependências com CVEs abertas; ausência de pentest antes do go-live.
- **Responsável:** Tech Lead com apoio de segurança da informação

---

## Riscos monitorados como oportunidades

- **O-01 — Reuso da camada de integração:** o conector construído para o PEP pode ser reaproveitado em outros produtos da clínica, diluindo o custo de desenvolvimento.
- **O-02 — Dados de absenteísmo:** o histórico gerado pelo app permite prever faltas e realizar overbooking controlado no futuro.

---

**Data do levantamento inicial:** fase de planejamento, pré-Sprint 1 · **Próxima revisão:** ao final da Sprint 1, com dados reais de execução
