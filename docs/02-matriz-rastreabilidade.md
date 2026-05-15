# Matriz de Rastreabilidade — TaskFlow v1.0

Mapeamento entre requisitos funcionais, casos de teste e resultados de execução.

---

## Legenda

- ✅ Passou
- ❌ Falhou (bug aberto)
- ⏳ Não executado

---

## Matriz

| Requisito | Descrição | Caso de teste | Resultado | Bug |
|---|---|---|---|---|
| RF-01 | Cadastro de usuário | CT-001.1 — Cadastro com dados válidos | ✅ | — |
| RF-01 | Cadastro de usuário | CT-001.2 — Cadastro com email inválido | ❌ | [BUG-001](../bug-reports/BUG-001-cadastro-email-invalido.md) |
| RF-01 | Cadastro de usuário | CT-001.3 — Cadastro com email duplicado | ✅ | — |
| RF-01 | Cadastro de usuário | CT-001.4 — Cadastro com senha curta | ✅ | — |
| RF-01 | Cadastro de usuário | CT-001.5 — Campos obrigatórios vazios | ✅ | — |
| RF-02 | Login | CT-002.1 — Login com credenciais válidas | ✅ | — |
| RF-02 | Login | CT-002.2 — Login com senha incorreta | ✅ | — |
| RF-02 | Login | CT-002.3 — Login com email inexistente | ✅ | — |
| RF-02 | Login | CT-002.4 — Email com variação de maiúsculas | ❌ | [BUG-002](../bug-reports/BUG-002-login-case-sensitive.md) |
| RF-02 | Login | CT-002.5 — Logout | ✅ | — |
| RF-03 | Criar tarefa | CT-003.1 — Criação com dados válidos | ✅ | — |
| RF-03 | Criar tarefa | CT-003.2 — Título no limite máximo | ❌ | [BUG-003](../bug-reports/BUG-003-task-titulo-longo.md) |
| RF-03 | Criar tarefa | CT-003.3 — Título vazio | ✅ | — |
| RF-04 | Listar tarefas | CT-003.4 — Listagem com tarefas | ✅ | — |
| RF-04 | Listar tarefas | CT-003.5 — Listagem vazia | ✅ | — |
| RF-05 | Editar tarefa | CT-003.6 — Edição de título e status | ✅ | — |
| RF-06 | Excluir tarefa | CT-003.7 — Exclusão com confirmação | ✅ | — |
| RF-06 | Excluir tarefa | CT-003.8 — Cancelar exclusão | ✅ | — |

---

## Resumo de cobertura

| Requisito | Casos planejados | Executados | Passou | Falhou | Cobertura |
|---|---|---|---|---|---|
| RF-01 | 5 | 5 | 4 | 1 | 100% |
| RF-02 | 5 | 5 | 4 | 1 | 100% |
| RF-03 | 3 | 3 | 2 | 1 | 100% |
| RF-04 | 2 | 2 | 2 | 0 | 100% |
| RF-05 | 1 | 1 | 1 | 0 | 100% |
| RF-06 | 2 | 2 | 2 | 0 | 100% |
| **Total** | **18** | **18** | **15** | **3** | **100%** |

---

## Distribuição de bugs por severidade

| Severidade | Quantidade |
|---|---|
| Crítica | 0 |
| Alta | 1 (BUG-002) |
| Média | 1 (BUG-001) |
| Baixa | 1 (BUG-003) |
