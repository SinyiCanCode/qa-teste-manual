# CT-001 — Cadastro de Usuário

| Campo | Informação |
|---|---|
| **Requisito relacionado** | RF-01 |
| **Funcionalidade** | Cadastro de novo usuário |
| **Prioridade** | Alta |
| **Pré-condições** | Aplicação acessível em staging; usuário não logado |

---

## CT-001.1 — Cadastro com dados válidos

**Tipo:** Funcional positivo

```gherkin
Funcionalidade: Cadastro de usuário
  Como visitante
  Quero criar uma conta
  Para acessar minhas tarefas

Cenário: Cadastro bem-sucedido com dados válidos
  Dado que estou na página de cadastro
  Quando preencho o campo "Nome" com "Maria Silva"
  E preencho o campo "Email" com "maria.silva@exemplo.com"
  E preencho o campo "Senha" com "Senha@2026"
  E preencho o campo "Confirmar senha" com "Senha@2026"
  E clico no botão "Criar conta"
  Então sou redirecionado para a página de login
  E vejo a mensagem "Conta criada com sucesso. Faça login para continuar."
```

**Resultado esperado:** Usuário cadastrado, redirecionamento para login, mensagem de sucesso exibida.

**Resultado obtido:** Conforme esperado. ✅

---

## CT-001.2 — Cadastro com email inválido

**Tipo:** Funcional negativo

```gherkin
Cenário: Tentativa de cadastro com formato de email inválido
  Dado que estou na página de cadastro
  Quando preencho o campo "Nome" com "João Souza"
  E preencho o campo "Email" com "joao@email"
  E preencho o campo "Senha" com "Senha@2026"
  E preencho o campo "Confirmar senha" com "Senha@2026"
  E clico no botão "Criar conta"
  Então a conta NÃO deve ser criada
  E vejo a mensagem "Formato de email inválido"
```

**Resultado esperado:** Cadastro bloqueado, mensagem de erro clara.

**Resultado obtido:** ❌ Falha — ver [BUG-001](../bug-reports/BUG-001-cadastro-email-invalido.md).

---

## CT-001.3 — Cadastro com email já existente

**Tipo:** Funcional negativo

```gherkin
Cenário: Tentativa de cadastro com email já cadastrado
  Dado que existe um usuário com email "maria.silva@exemplo.com"
  E estou na página de cadastro
  Quando preencho os campos com email "maria.silva@exemplo.com"
  E clico no botão "Criar conta"
  Então a conta NÃO deve ser criada
  E vejo a mensagem "Email já cadastrado"
```

**Resultado esperado:** Cadastro bloqueado, mensagem informativa.

**Resultado obtido:** Conforme esperado. ✅

---

## CT-001.4 — Cadastro com senha curta

**Tipo:** Valor limite

```gherkin
Cenário: Tentativa de cadastro com senha abaixo do mínimo
  Dado que estou na página de cadastro
  Quando preencho o campo "Senha" com "abc12" (5 caracteres)
  E preencho os demais campos corretamente
  E clico no botão "Criar conta"
  Então vejo a mensagem "Senha deve ter no mínimo 8 caracteres"
  E o cadastro não é efetivado
```

**Resultado esperado:** Validação de tamanho mínimo aplicada.

**Resultado obtido:** Conforme esperado. ✅

---

## CT-001.5 — Campos obrigatórios vazios

**Tipo:** Funcional negativo

```gherkin
Cenário: Submissão do formulário com campos vazios
  Dado que estou na página de cadastro
  Quando clico no botão "Criar conta" sem preencher os campos
  Então vejo mensagens de erro em cada campo obrigatório:
    | Campo            | Mensagem                       |
    | Nome             | Nome é obrigatório             |
    | Email            | Email é obrigatório            |
    | Senha            | Senha é obrigatória            |
    | Confirmar senha  | Confirmação é obrigatória      |
```

**Resultado esperado:** Mensagens de erro por campo.

**Resultado obtido:** Conforme esperado. ✅
