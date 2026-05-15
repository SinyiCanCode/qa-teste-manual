# CT-002 — Login e Logout

| Campo | Informação |
|---|---|
| **Requisito relacionado** | RF-02 |
| **Funcionalidade** | Autenticação |
| **Prioridade** | Alta |
| **Pré-condições** | Usuário "maria.silva@exemplo.com" cadastrado com senha "Senha@2026" |

---

## CT-002.1 — Login com credenciais válidas

**Tipo:** Funcional positivo

```gherkin
Cenário: Login bem-sucedido
  Dado que estou na página de login
  Quando preencho "Email" com "maria.silva@exemplo.com"
  E preencho "Senha" com "Senha@2026"
  E clico em "Entrar"
  Então sou redirecionado para o dashboard
  E vejo a saudação "Olá, Maria"
```

**Resultado:** ✅ Passou

---

## CT-002.2 — Login com senha incorreta

**Tipo:** Funcional negativo

```gherkin
Cenário: Login com senha errada
  Dado que estou na página de login
  Quando preencho "Email" com "maria.silva@exemplo.com"
  E preencho "Senha" com "senhaErrada"
  E clico em "Entrar"
  Então permaneço na página de login
  E vejo a mensagem "Email ou senha incorretos"
```

**Resultado:** ✅ Passou

> **Nota de segurança:** A mensagem não distingue entre "email não existe" e "senha incorreta", evitando enumeração de usuários.

---

## CT-002.3 — Login com email inexistente

**Tipo:** Funcional negativo

```gherkin
Cenário: Login com email não cadastrado
  Dado que estou na página de login
  Quando preencho "Email" com "naoexiste@exemplo.com"
  E preencho "Senha" com "qualquerSenha123"
  E clico em "Entrar"
  Então permaneço na página de login
  E vejo a mensagem "Email ou senha incorretos"
```

**Resultado:** ✅ Passou

---

## CT-002.4 — Email com variação de maiúsculas

**Tipo:** Borda / consistência

```gherkin
Cenário: Login com email cadastrado em variação de caixa
  Dado que o usuário foi cadastrado com email "maria.silva@exemplo.com"
  E estou na página de login
  Quando preencho "Email" com "Maria.Silva@Exemplo.com"
  E preencho "Senha" com "Senha@2026"
  E clico em "Entrar"
  Então sou autenticado com sucesso
```

**Resultado esperado:** Login aceito — emails são case-insensitive por convenção (RFC 5321).

**Resultado obtido:** ❌ Falha — ver [BUG-002](../bug-reports/BUG-002-login-case-sensitive.md).

---

## CT-002.5 — Logout

**Tipo:** Funcional positivo

```gherkin
Cenário: Encerrar sessão
  Dado que estou autenticado no dashboard
  Quando clico no menu do usuário
  E clico em "Sair"
  Então sou redirecionado para a página de login
  E ao tentar acessar /dashboard diretamente sou redirecionado para /login
```

**Resultado:** ✅ Passou
