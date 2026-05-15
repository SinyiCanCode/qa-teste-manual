# Plano de Teste — TaskFlow v1.0

| Campo | Informação |
|---|---|
| **Aplicação** | TaskFlow — Gerenciador de tarefas |
| **Versão** | 1.0.0 |
| **Autor** | Francisco Lima |
| **Data** | 2026-05-15 |
| **Status** | Aprovado |

---

## 1. Objetivo

Validar as funcionalidades de autenticação (cadastro e login) e gerenciamento de tarefas (CRUD) da aplicação TaskFlow, garantindo conformidade com os requisitos funcionais e identificando defeitos antes do release em produção.

---

## 2. Escopo

### 2.1 Funcionalidades cobertas

- Cadastro de usuário (RF-01)
- Login e logout (RF-02)
- Criação de tarefa (RF-03)
- Listagem de tarefas (RF-04)
- Edição de tarefa (RF-05)
- Exclusão de tarefa (RF-06)

### 2.2 Fora de escopo

- Recuperação de senha (planejado para v1.1)
- Compartilhamento de tarefas entre usuários
- Notificações push
- Testes de performance e carga
- Testes de segurança em profundidade (cobertos por auditoria específica)

---

## 3. Estratégia de teste

### 3.1 Níveis de teste

| Nível | Responsável | Cobertura nesta fase |
|---|---|---|
| Unitário | Desenvolvimento | Não aplicável |
| Integração | Desenvolvimento + QA | Endpoints críticos |
| Sistema | QA | **Foco deste plano** |
| Aceitação | QA + PO | Casos de uso principais |

### 3.2 Tipos de teste aplicados

- **Funcional:** validação de cada requisito conforme especificação
- **Negativo:** comportamento com entradas inválidas
- **Borda:** valores no limite (campos vazios, máximos, caracteres especiais)
- **Usabilidade básica:** mensagens de erro claras, feedback visual

### 3.3 Técnicas

- Partição de equivalência (campos de formulário)
- Análise de valor limite (tamanhos máximos, datas)
- Tabela de decisão (regras de validação compostas)

---

## 4. Ambiente de teste

| Item | Configuração |
|---|---|
| Navegadores | Chrome 124, Firefox 125 |
| Sistema operacional | Windows 11, macOS 14 |
| Resolução | 1920x1080 (desktop) |
| Backend | API REST hospedada em ambiente de staging |
| Banco de dados | PostgreSQL 16 — base de teste isolada |

---

## 5. Critérios

### 5.1 Critérios de entrada

- Build estável disponível em staging
- Documentação de requisitos aprovada
- Casos de teste revisados

### 5.2 Critérios de saída

- 100% dos casos de teste planejados executados
- Zero bugs de severidade crítica em aberto
- Bugs de severidade alta com plano de correção definido
- Relatório final de execução entregue ao PO

---

## 6. Riscos identificados

| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Ambiente de staging instável | Média | Alto | Validar ambiente antes de iniciar ciclo |
| Mudanças de requisito durante o ciclo | Alta | Médio | Versionar casos de teste; replanejar |
| Dados de teste insuficientes | Baixa | Médio | Script de seed do banco preparado |

---

## 7. Entregáveis

- Casos de teste em formato Gherkin
- Bug reports estruturados com evidências
- Matriz de rastreabilidade requisito × caso × resultado
- Relatório consolidado de execução

---

## 8. Cronograma

| Atividade | Período |
|---|---|
| Elaboração do plano | Dia 1 |
| Escrita dos casos de teste | Dias 2-3 |
| Execução do ciclo de teste | Dias 4-6 |
| Reporte de bugs e retest | Dias 7-8 |
| Relatório final | Dia 9 |
