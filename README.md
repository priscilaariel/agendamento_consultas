# Aplicativo Móvel de Agendamento de Consultas Médicas — Gestão de Riscos

Repositório de documentação de **gerenciamento de riscos e comunicação** do projeto de desenvolvimento de um aplicativo móvel para agendamento de consultas médicas.

Entrega da atividade prática de Engenharia de Software / Gestão de Projetos com apoio de Inteligência Artificial Generativa.

---

## 1. Contexto do Projeto

O produto é um aplicativo mobile multiplataforma que conecta pacientes, profissionais de saúde e a operação da clínica, eliminando o agendamento por telefone e reduzindo o absenteísmo em consultas.

### 1.1 Escopo funcional

| Módulo | Descrição |
|---|---|
| Cadastro e autenticação de usuários | Perfis de Paciente, Médico e Administrador, com consentimento LGPD e criptografia de dados sensíveis |
| Gestão de agenda médica | Configuração de horários, duração de consulta, bloqueios por férias, congressos e plantões |
| Agendamento de consultas | Busca por especialidade/profissional/unidade, verificação de conflito em tempo real, remarcação e cancelamento |
| Notificações | Push e SMS para confirmação, lembrete de véspera e aviso de alteração de agenda |
| Integração com prontuário externo (PEP) | Sincronização de histórico clínico e elegibilidade do paciente via API de fornecedor terceiro |

### 1.2 Equipe

- 1 Gerente de Projetos (recém-alocado)
- 4 Desenvolvedores (2 mobile, 2 back-end) — em processo de formação do time
- 1 Analista de QA
- Apoio parcial, ainda a confirmar, de um DPO/jurídico para questões de LGPD

Metodologia proposta: Scrum adaptado, sprints de duas semanas. **Ainda não iniciada** — em validação com o patrocinador.

### 1.3 Situação atual

O projeto está em **fase de planejamento e estruturação**, anterior ao início do desenvolvimento. Ainda não há código em produção nem sprint executada. As atividades em curso são:

- Levantamento de requisitos com a área médica e administrativa da clínica.
- Definição da arquitetura de alto nível e escolha de tecnologias.
- Contato inicial com o fornecedor do sistema de prontuário eletrônico (PEP) para entender o modelo de integração disponível.
- Elaboração do plano de projeto, do registro preliminar de riscos e da matriz de comunicação com stakeholders.
- Formação e alocação final da equipe.

Três pontos já concentram a atenção da gerência **antes mesmo do primeiro sprint**, por representarem incerteza estrutural do projeto:

1. Modelo de integração com o PEP do fornecedor externo ainda não está definido nem contratualizado.
2. Escopo funcional carece de baseline formalmente aprovada pela área médica.
3. Estimativas de esforço ainda não têm histórico de velocidade da equipe, por não haver sprint executada.

---

## 2. Estrutura do repositório

```
.
├── README.md                          # Visão geral e contexto (este arquivo)
├── riscos/
│   ├── identificacao.md               # Registro de riscos, causas e gatilhos
│   └── analise.md                     # Probabilidade, impacto, severidade e priorização
└── comunicacao/
    └── status-stakeholders.md         # Relatório executivo de status
```

> Observação: os **planos de resposta aos riscos** (mitigar, transferir, evitar, aceitar) estão consolidados em `riscos/analise.md` e detalhados por risco em `riscos/identificacao.md`.


---

## 5. Status do projeto

**Fase atual:** Planejamento e estruturação (pré-Sprint 1)
**Marco anterior:** Aprovação da proposta e alocação inicial de equipe
**Próximo marco:** Kickoff formal e início da Sprint 1

> Os dados quantitativos deste repositório (probabilidade, impacto, indicadores) refletem uma **estimativa inicial da equipe**, sem histórico de execução do projeto. Serão recalibrados a partir da primeira sprint.
