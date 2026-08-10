# Relatório Executivo de Status — Stakeholders

**Projeto:** Aplicativo Móvel de Agendamento de Consultas Médicas
**Período:** Fase de Planejamento e Estruturação (pré-Sprint 1)
**Emitido por:** Gerência de Projetos
**Público:** Patrocinador, Diretoria Clínica, Coordenação de TI, Fornecedor do PEP

---

## 1. Situação geral

**Status: PLANEJAMENTO**

O projeto foi aprovado e está em sua fase inicial de estruturação. Ainda não há desenvolvimento em curso: a equipe está sendo formada, os requisitos estão sendo levantados junto à área médica e administrativa, e as decisões estruturais de arquitetura e de contratação de fornecedores ainda estão em aberto. Este relatório tem como objetivo alinhar expectativas antes do kickoff formal.

| Dimensão | Situação |
|---|---|
| Escopo | Levantamento em andamento; baseline ainda não aprovada |
| Prazo | Cronograma em elaboração; datas ainda não comprometidas |
| Custo | Orçamento aprovado; sem execução até o momento |
| Qualidade | Não aplicável nesta fase |
| Riscos | Registro inicial concluído; dois riscos de alta severidade dependem de decisão externa à equipe |
| Equipe | Em formação; alocação final pendente |

---

## 2. Atividades concluídas na fase de planejamento

- Aprovação da proposta do projeto pelo patrocinador.
- Definição do escopo funcional macro (cadastro de usuários, gestão de agenda médica, agendamento, notificações e integração com prontuário externo).
- Primeira reunião exploratória com o possível fornecedor do sistema de prontuário eletrônico (PEP).
- Elaboração do registro inicial de riscos e da matriz de comunicação com stakeholders (este repositório).
- Início do processo de alocação da equipe técnica.

## 3. Em andamento

- Levantamento detalhado de requisitos com a área médica e a recepção da clínica.
- Definição da arquitetura de alto nível e das tecnologias a adotar.
- Avaliação formal do fornecedor de PEP, incluindo tratativa de SLA.
- Confirmação da disponibilidade de um DPO para apoio ao projeto.

## 4. Próximos passos até o kickoff

1. Aprovar e assinar a baseline funcional do MVP com a diretoria clínica.
2. Formalizar SLA com o fornecedor do PEP ou definir plano B de integração.
3. Confirmar alocação da equipe completa e do DPO de apoio.
4. Definir o cronograma da Sprint 1 com base em estimativas iniciais (sem histórico de velocidade).
5. Realizar o kickoff formal do projeto.

---

## 5. Riscos relevantes para a decisão dos stakeholders

Registro inicial de riscos, produzido antes do início do desenvolvimento. Detalhamento completo em `riscos/identificacao.md` e `riscos/analise.md`.

| ID | Risco | Severidade | Situação | O que pedimos |
|---|---|---|---|---|
| R-01 | Modelo de integração com o prontuário externo ainda indefinido | Crítico | Em avaliação | Apoio da diretoria para priorizar a negociação de SLA com o fornecedor antes do kickoff |
| R-02 | Escopo funcional ainda não consolidado | Alto | Em avaliação | Aprovação formal da baseline do MVP pela área médica |
| R-04 | Conformidade com a LGPD ainda não endereçada | Alto | Em avaliação | Confirmação da alocação de um DPO ao projeto |
| R-03 | Estimativas sem histórico de velocidade | Alto | Conhecido, sem ação anterior ao início | Aceite de que as três primeiras sprints servirão de calibragem |

> Nenhum desses riscos é, a esta altura, uma falha do projeto — são incertezas normais de uma fase de planejamento. O objetivo de trazê-los agora é permitir decisão antes que eles se tornem bloqueio de cronograma.

---

## 6. Decisões necessárias antes do kickoff

| # | Decisão solicitada | Responsável | Prazo sugerido |
|---|---|---|---|
| D-01 | Priorizar tratativa comercial/contratual com o fornecedor do PEP | Patrocinador | Antes do kickoff |
| D-02 | Aprovar formalmente a baseline funcional do MVP | Diretoria Clínica | Antes do kickoff |
| D-03 | Confirmar alocação do DPO de apoio ao projeto | Coordenação de TI / Jurídico | Antes do kickoff |
| D-04 | Validar o cronograma inicial com reserva de 15% para imprevistos | Patrocinador | Antes do kickoff |

> A ausência de decisão em D-01 e D-02 até o kickoff implica adiar o início da Sprint 1, pois ambos afetam diretamente a arquitetura e o escopo do MVP.

---

