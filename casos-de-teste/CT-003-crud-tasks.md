# CT-003 — CRUD de Tarefas

| Campo | Informação |
|---|---|
| **Requisitos relacionados** | RF-03, RF-04, RF-05, RF-06 |
| **Funcionalidade** | Gerenciamento de tarefas |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário autenticado no dashboard |

---

## CT-003.1 — Criação de tarefa com dados válidos

```gherkin
Cenário: Criar nova tarefa
  Dado que estou no dashboard
  Quando clico em "Nova tarefa"
  E preencho "Título" com "Comprar leite"
  E preencho "Descrição" com "Mercado da esquina"
  E seleciono prioridade "Média"
  E clico em "Salvar"
  Então a tarefa aparece na lista
  E vejo o toast "Tarefa criada"
```

**Resultado:** ✅ Passou

---

## CT-003.2 — Título no limite máximo

**Tipo:** Valor limite

```gherkin
Cenário: Criação de tarefa com título no tamanho máximo
  Dado que estou criando uma nova tarefa
  E o limite documentado é 100 caracteres
  Quando preencho "Título" com uma string de exatamente 100 caracteres
  E clico em "Salvar"
  Então a tarefa é criada com sucesso
  E o título exibido na lista preserva os 100 caracteres
```

**Resultado esperado:** Tarefa criada, título preservado.

**Resultado obtido:** ❌ Falha — ver [BUG-003](../bug-reports/BUG-003-task-titulo-longo.md).

---

## CT-003.3 — Título vazio

```gherkin
Cenário: Bloqueio de criação com título vazio
  Dado que estou criando uma nova tarefa
  Quando deixo o campo "Título" vazio
  E clico em "Salvar"
  Então a tarefa não é criada
  E vejo a mensagem "Título é obrigatório"
```

**Resultado:** ✅ Passou

---

## CT-003.4 — Listagem com tarefas

```gherkin
Cenário: Listar tarefas existentes
  Dado que possuo 5 tarefas cadastradas
  Quando acesso o dashboard
  Então vejo as 5 tarefas listadas
  E cada tarefa exibe título, prioridade e status
  E posso ordenar por data de criação
```

**Resultado:** ✅ Passou

---

## CT-003.5 — Estado vazio

```gherkin
Cenário: Listagem sem tarefas
  Dado que não possuo tarefas cadastradas
  Quando acesso o dashboard
  Então vejo a mensagem "Nenhuma tarefa cadastrada"
  E vejo um botão de chamada para "Criar primeira tarefa"
```

**Resultado:** ✅ Passou

---

## CT-003.6 — Edição de tarefa

```gherkin
Cenário: Editar título e status de tarefa
  Dado que tenho uma tarefa com título "Comprar leite" e status "Pendente"
  Quando clico no ícone de edição
  E altero o título para "Comprar leite e pão"
  E altero o status para "Concluída"
  E clico em "Salvar"
  Então as alterações são refletidas na lista
  E o toast "Tarefa atualizada" é exibido
```

**Resultado:** ✅ Passou

---

## CT-003.7 — Exclusão com confirmação

```gherkin
Cenário: Excluir tarefa confirmando a ação
  Dado que tenho uma tarefa cadastrada
  Quando clico no ícone de excluir
  E vejo um modal de confirmação
  E clico em "Excluir"
  Então a tarefa é removida da lista
  E o toast "Tarefa excluída" é exibido
```

**Resultado:** ✅ Passou

---

## CT-003.8 — Cancelar exclusão

```gherkin
Cenário: Cancelar exclusão de tarefa
  Dado que tenho uma tarefa cadastrada
  Quando clico no ícone de excluir
  E no modal de confirmação clico em "Cancelar"
  Então a tarefa permanece na lista
  E nenhum toast é exibido
```

**Resultado:** ✅ Passou
