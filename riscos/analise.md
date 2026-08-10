# Análise e Planos de Resposta aos Riscos

Análise qualitativa **inicial** dos riscos registrados em `identificacao.md`, realizada na fase de planejamento do projeto, antes do início do desenvolvimento. Probabilidade e impacto foram estimados pela equipe com base em experiência prévia e em projetos análogos, na ausência de dados reais de execução. A matriz será recalibrada ao final da Sprint 1.

## 1. Escalas adotadas

**Probabilidade**

| Nível | Significado |
|---|---|
| 1 | Raro — improvável no horizonte do projeto |
| 2 | Pouco provável |
| 3 | Possível — já ocorreu em projetos semelhantes |
| 4 | Provável |
| 5 | Quase certo — sinais já presentes hoje |

**Impacto**

| Nível | Significado |
|---|---|
| 1 | Desprezível — absorvido dentro do sprint |
| 2 | Menor — pequeno retrabalho |
| 3 | Moderado — atraso de até uma sprint |
| 4 | Alto — atraso de marco ou perda de funcionalidade relevante |
| 5 | Severo — inviabiliza o go-live ou gera passivo legal |

**Severidade = Probabilidade × Impacto** · Baixo 1–6 · Médio 7–12 · Alto 13–19 · Crítico 20–25

---

## 2. Matriz de riscos

| ID | Risco | Prob. | Imp. | Sev. | Faixa | Estratégia |
|---|---|:---:|:---:|:---:|---|---|
| R-01 | Instabilidade da API do PEP | 5 | 5 | 25 | Crítico | Mitigar + Transferir |
| R-04 | Não conformidade com a LGPD | 3 | 5 | 15 | Alto | Evitar |
| R-10 | Vazamento de dados | 3 | 5 | 15 | Alto | Mitigar |
| R-02 | Crescimento de escopo | 4 | 4 | 16 | Alto | Mitigar |
| R-03 | Estimativas otimistas e sobrecarga | 4 | 4 | 16 | Alto | Mitigar |
| R-06 | Overbooking na agenda | 3 | 4 | 12 | Médio | Mitigar |
| R-05 | Falha de notificações | 4 | 3 | 12 | Médio | Mitigar |
| R-09 | Dependência de pessoa-chave | 3 | 4 | 12 | Médio | Mitigar |
| R-07 | Baixa adoção pelos usuários | 3 | 4 | 12 | Médio | Mitigar |
| R-08 | Rejeição nas lojas | 3 | 3 | 9 | Médio | Mitigar |

### Distribuição

```
Impacto
  5 |            |        | R-04   | R-01
    |            | R-10   |        |
  4 |            | R-06   | R-02   |
    |            | R-09   | R-03   |
    |            | R-07   |        |
  3 |            | R-08   | R-05   |
  2 |            |        |        |
  1 |            |        |        |
    +------------+--------+--------+--------
        Prob 2       3        4       5
```

**Concentração:** oito dos dez riscos estão em faixa Alta ou Crítica logo na fase de planejamento, o que é coerente com um projeto que ainda tem sua dependência externa mais crítica sem contrato definido e sua baseline funcional sem aprovação formal. Isso reforça a recomendação de **não iniciar a Sprint 1** antes de endereçar R-01, R-02 e R-04, que dependem de decisões externas à equipe técnica. A priorização de esforço na fase de estruturação deve seguir a ordem R-01 → R-04 → R-02/R-03.

---

## 3. Planos de resposta

### R-01 · Instabilidade da API do PEP — *Mitigar + Transferir* — **Crítico**

**Ações de mitigação**
- Criar uma **camada anticorrupção** (adapter) isolando todo o projeto do contrato do fornecedor: uma mudança externa passa a afetar um único módulo.
- Implementar **cache local** do último estado de elegibilidade válido, com carimbo de data e aviso ao usuário quando o dado não estiver fresco.
- Adotar **circuit breaker** com fallback: se o PEP estiver indisponível, o agendamento é concluído em estado "pendente de validação clínica" e reconciliado depois por fila assíncrona.
- Escrever **testes de contrato automatizados** executados diariamente contra o ambiente de homologação do fornecedor, para detectar mudanças antes de elas chegarem à produção.

**Ações de transferência**
- Formalizar **SLA contratual** com o fornecedor: disponibilidade mínima, prazo de aviso de mudança de contrato (mínimo 30 dias) e canal técnico dedicado.

**Plano de contingência (se o risco se materializar)**
- Ativar modo degradado documentado, comunicar a recepção da clínica em até 15 minutos e acionar o canal de escalonamento do fornecedor.

**Risco residual esperado:** Médio — a indisponibilidade continua possível, mas deixa de bloquear o agendamento.
**Indicador a instituir desde a Sprint 1:** taxa de sucesso das chamadas ao PEP por semana (meta ≥ 98%).
**Pré-requisito antes do kickoff:** confirmação, ainda que preliminar, de que o fornecedor disponibilizará ambiente de homologação para os testes de contrato.

---

### R-02 · Crescimento de escopo — *Mitigar* — **Alto**

- Instituir **comitê de controle de mudanças** quinzenal: toda nova regra entra como item de backlog com estimativa e é priorizada contra o que já existe, nunca somada ao sprint corrente.
- Congelar a **baseline funcional do MVP** por escrito e assinada pelo patrocinador.
- Aplicar a regra de **troca equivalente**: item novo entra quando item de esforço similar sai.
- Registrar em ata o impacto de prazo de cada solicitação recusada ou adiada — transforma discussão subjetiva em número.

**Risco residual esperado:** Médio · **Indicador a instituir desde a Sprint 1:** número de itens não planejados admitidos por sprint (meta ≤ 1).

---

### R-03 · Estimativas otimistas e sobrecarga — *Mitigar* — **Alto**

- Estimar por **planning poker** com faixas, e calibrar a capacidade do sprint pela velocidade real das últimas três sprints, não pelo desejo de prazo.
- Reservar **20% de folga** por sprint para imprevistos, correções e suporte.
- Monitorar horas extras como métrica de saúde do time, discutida em retrospectiva.
- Reforçar o time com um desenvolvedor adicional na frente de integração, que é a que mais gera variabilidade.

**Risco residual esperado:** Médio · **Indicador a instituir desde a Sprint 1:** desvio entre esforço estimado e realizado (meta ≤ 15%).

---

### R-04 · Não conformidade com a LGPD — *Evitar* — **Alto**

- Executar **privacy by design**: mapear o ciclo de vida de cada dado pessoal antes de codificar o módulo correspondente.
- Implementar tela de **consentimento granular e auditável**, com registro de data, hora e versão do termo.
- Criptografar dados sensíveis em repouso e em trânsito, e proibir dados clínicos em logs.
- Submeter o **Relatório de Impacto à Proteção de Dados (RIPD)** ao DPO como critério obrigatório de saída da fase de desenvolvimento — sem parecer favorável, não há go-live.

**Risco residual esperado:** Baixo · **Indicador a instituir desde a Sprint 1:** itens de checklist LGPD concluídos (meta 100% antes do go-live).

---

### R-10 · Vazamento de dados — *Mitigar* — **Alto**

- Incluir análise estática (SAST) e verificação de dependências na esteira de CI/CD, bloqueando o merge em caso de vulnerabilidade alta.
- Armazenar tokens em Keychain/Keystore, com expiração curta e refresh token rotativo.
- Aplicar limitação de taxa e registro de auditoria em todos os endpoints que expõem dados de paciente.
- Contratar **pentest externo** antes do go-live.

**Risco residual esperado:** Baixo/Médio · **Indicador a instituir desde a Sprint 1:** zero vulnerabilidades críticas abertas no fim de cada sprint.

---

### R-06 · Overbooking na agenda — *Mitigar* — **Médio**

- Aplicar **bloqueio otimista** com verificação transacional no banco e restrição de unicidade por (profissional, data-hora).
- Reservar temporariamente o slot por 5 minutos durante a confirmação.
- Armazenar todos os horários em UTC, convertendo apenas na camada de apresentação.
- Incluir teste de carga com agendamentos simultâneos na definição de pronto do módulo.

**Risco residual esperado:** Baixo · **Indicador a instituir desde a Sprint 1:** ocorrências de duplicidade em produção (meta zero).

---

### R-05 · Falha de notificações — *Mitigar* — **Médio**

- Adotar **estratégia em camadas**: push como canal primário, SMS como fallback e e-mail como último recurso.
- Validar telefone por código no cadastro.
- Registrar confirmação de entrega e exibir painel de taxa de entrega.
- Manter fila com nova tentativa em caso de falha do provedor.

**Risco residual esperado:** Baixo · **Indicador a instituir desde a Sprint 1:** taxa de entrega de lembretes (meta ≥ 95%).

---

### R-09 · Dependência de pessoa-chave — *Mitigar* — **Médio**

- Programação em par rotativa na frente de integração e revisão obrigatória de código por segunda pessoa.
- Documentar decisões arquiteturais em ADRs versionados no repositório.
- Manter matriz de competências com pelo menos duas pessoas por área crítica.

**Risco residual esperado:** Baixo · **Indicador a instituir desde a Sprint 1:** nenhum módulo crítico com autor único.

---

### R-07 · Baixa adoção — *Mitigar* — **Médio**

- Realizar **testes de usabilidade** com pacientes reais de faixas etárias distintas antes do go-live.
- Piloto controlado com duas especialidades antes da abertura geral.
- Treinamento e onboarding assistido para os médicos, com suporte dedicado nas duas primeiras semanas.
- Manter o canal telefônico ativo em paralelo durante a transição.

**Risco residual esperado:** Médio · **Indicador a instituir desde a Sprint 1:** percentual de agendamentos feitos pelo app (meta 40% em 90 dias).

---

### R-08 · Rejeição nas lojas — *Mitigar* — **Médio**

- Submeter uma build de teste às lojas com pelo menos seis semanas de antecedência.
- Publicar política de privacidade e justificar cada permissão solicitada.
- Manter checklist das diretrizes de aplicativos de saúde das duas lojas.

**Risco residual esperado:** Baixo · **Indicador a instituir desde a Sprint 1:** aprovação na primeira submissão.

---

## 4. Riscos aceitos

| ID | Risco | Justificativa |
|---|---|---|
| A-01 | Pequenas variações de layout entre versões de Android | Custo de suporte universal supera o benefício; define-se suporte a partir do Android 10 |
| A-02 | Indisponibilidade planejada de janelas de manutenção do PEP | Impacto absorvido pelo modo degradado já previsto em R-01 |

---

## 5. Reserva de contingência

Recomenda-se que o cronograma inicial já preveja, desde a linha de base, reserva de **15% do esforço total** e **duas semanas de folga**, alocadas prioritariamente à frente de integração (R-01) e à adequação de LGPD (R-04). Como ainda não há cronograma aprovado, esta é uma premissa a ser incorporada ao plano de projeto antes do kickoff.

---

**Responsável pela análise:** Gerente de Projetos · **Status:** análise inicial, fase de planejamento · **Próxima revisão:** ao final da Sprint 1
