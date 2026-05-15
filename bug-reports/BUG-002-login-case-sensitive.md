# BUG-002 — Login falha quando email é digitado com variação de maiúsculas

| Campo | Informação |
|---|---|
| **ID** | BUG-002 |
| **Título** | Login não aceita email com variação de maiúsculas/minúsculas |
| **Reportado por** | Francisco Lima |
| **Data** | 2026-05-15 |
| **Versão** | 1.0.0 (build #142) |
| **Ambiente** | Staging — Chrome 124 / Windows 11 |
| **Severidade** | Alta |
| **Prioridade** | Alta |
| **Status** | Aberto |
| **Caso de teste** | [CT-002.4](../casos-de-teste/CT-002-login.md#ct-0024--email-com-variação-de-maiúsculas) |
| **Requisito** | RF-02 |

---

## Resumo

O sistema trata o campo email como **case-sensitive** no login. Um usuário cadastrado como `maria.silva@exemplo.com` não consegue autenticar usando `Maria.Silva@Exemplo.com`, mesmo com a senha correta. Conforme a RFC 5321, a parte do domínio é case-insensitive e a maioria dos provedores trata a parte local da mesma forma.

---

## Passos para reproduzir

**Pré-condição:** existir um usuário cadastrado com email `maria.silva@exemplo.com`.

1. Acessar `https://staging.taskflow.app/login`
2. Preencher os campos:
   - **Email:** `Maria.Silva@Exemplo.com` (note as maiúsculas)
   - **Senha:** `Senha@2026`
3. Clicar em **"Entrar"**

---

## Resultado esperado

- Autenticação bem-sucedida.
- Redirecionamento para `/dashboard`.
- Saudação "Olá, Maria" exibida.

---

## Resultado obtido

- Login **rejeitado**.
- Mensagem exibida: "Email ou senha incorretos".
- Usuário permanece na página de login.

---

## Evidências

- `evidencias/bug-002-tentativa-login.png` — formulário preenchido
- `evidencias/bug-002-mensagem-erro.png` — mensagem de erro exibida
- `evidencias/bug-002-login-funciona-lowercase.png` — mesmo usuário entra com email em minúsculas

---

## Análise de impacto

- **Usabilidade:** usuários frequentemente caem em autocorreção do teclado (especialmente mobile) que capitaliza a primeira letra. Resultado: tentativas legítimas falham.
- **Suporte:** alto volume de tickets esperados ("não consigo entrar").
- **Conversão:** pode aumentar taxa de abandono no login, especialmente em mobile.
- **Segurança:** mascarar a causa real (mensagem genérica "email ou senha incorretos") é correto por princípio, mas o comportamento ainda está errado.

---

## Sugestão de correção

Normalizar o email antes da comparação **em dois pontos**:

1. **No cadastro:** salvar o email já em lowercase no banco.
2. **No login:** converter o input para lowercase antes da consulta.

Exemplo em Python:

```python
email_normalizado = email.strip().lower()
usuario = db.query(User).filter(User.email == email_normalizado).first()
```

**Atenção:** será necessário migrar registros existentes (script de UPDATE com `LOWER(email)`).

---

## Observações

- Reproduzível em todos os navegadores testados (Chrome, Firefox).
- O mesmo problema **não** ocorre na senha — apenas no email (verificado).
- Recomendo revisar também o endpoint de recuperação de senha (provavelmente afetado pelo mesmo padrão).
