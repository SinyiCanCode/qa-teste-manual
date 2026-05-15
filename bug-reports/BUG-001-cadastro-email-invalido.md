# BUG-001 — Cadastro aceita email sem domínio completo

| Campo | Informação |
|---|---|
| **ID** | BUG-001 |
| **Título** | Sistema permite cadastro com email em formato inválido (sem TLD) |
| **Reportado por** | Francisco Lima |
| **Data** | 2026-05-15 |
| **Versão** | 1.0.0 (build #142) |
| **Ambiente** | Staging — Chrome 124 / Windows 11 |
| **Severidade** | Média |
| **Prioridade** | Alta |
| **Status** | Aberto |
| **Caso de teste** | [CT-001.2](../casos-de-teste/CT-001-cadastro.md#ct-0012--cadastro-com-email-inválido) |
| **Requisito** | RF-01 |

---

## Resumo

O formulário de cadastro aceita endereços de email sem domínio de topo (ex: `joao@email`), permitindo a criação de contas com emails que não poderão receber comunicações do sistema (recuperação de senha, notificações, etc.).

---

## Passos para reproduzir

1. Acessar `https://staging.taskflow.app/cadastro`
2. Preencher os campos com os seguintes dados:
   - **Nome:** João Souza
   - **Email:** `joao@email`
   - **Senha:** `Senha@2026`
   - **Confirmar senha:** `Senha@2026`
3. Clicar no botão **"Criar conta"**

---

## Resultado esperado

- O sistema deve **bloquear** a submissão.
- Mensagem exibida abaixo do campo email: **"Formato de email inválido"**.
- O foco deve retornar ao campo email.

---

## Resultado obtido

- A conta é **criada com sucesso**.
- Usuário é redirecionado para a tela de login.
- A mensagem "Conta criada com sucesso" é exibida.
- Verificado no banco de dados (tabela `users`): registro persistido com `email = 'joao@email'`.

---

## Evidências

- `evidencias/bug-001-formulario-submetido.png` — formulário aceitando o email inválido
- `evidencias/bug-001-redirecionamento-login.png` — tela de sucesso pós-submissão
- `evidencias/bug-001-registro-db.png` — registro persistido no banco

---

## Análise de impacto

- **Usuário final:** não conseguirá recuperar senha nem receber notificações.
- **Negócio:** dados sujos na base; potencial impacto em métricas de ativação.
- **Segurança:** indicador de validação fraca; pode haver outros campos com problema similar.

---

## Sugestão de correção

Aplicar validação de email no **frontend** (regex/HTML5 `type="email"`) **e** no **backend** (validador como `email-validator` em Python ou `validator.js` em Node). Validação dupla é boa prática — frontend para UX, backend para garantia.

Sugestão de regex mínima (RFC 5322 simplificada):

```
^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$
```

---

## Observações

- Reproduzido também no Firefox 125 — mesmo comportamento.
- Outros formatos inválidos também aceitos: `joao@`, `@email.com`, `joao email.com`.
- Recomendo criar casos de teste adicionais para cada variação após a correção.
