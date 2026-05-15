# QA Teste Manual — TaskFlow

Documentação completa de teste manual aplicada à aplicação fictícia **TaskFlow** (gerenciador de tarefas com cadastro, login e CRUD de tasks). Demonstra o ciclo completo: planejamento, execução, reporte e rastreabilidade.

> **Nota:** TaskFlow é uma aplicação fictícia criada para fins de portfolio. Os bugs reportados ilustram raciocínio de QA e padrão de documentação.

---

## Estrutura do repositório

```
qa-teste-manual/
├── docs/
│   ├── 01-plano-de-teste.md
│   └── 02-matriz-rastreabilidade.md
├── casos-de-teste/
│   ├── CT-001-cadastro.md
│   ├── CT-002-login.md
│   └── CT-003-crud-tasks.md
├── bug-reports/
│   ├── BUG-001-cadastro-email-invalido.md
│   ├── BUG-002-login-case-sensitive.md
│   └── BUG-003-task-titulo-longo.md
└── evidencias/
    └── (screenshots dos bugs)
```

---

## Como navegar

1. Comece pelo [**Plano de Teste**](docs/01-plano-de-teste.md) — visão estratégica
2. Veja os [**Casos de Teste**](casos-de-teste/) — execução planejada
3. Consulte os [**Bug Reports**](bug-reports/) — defeitos encontrados
4. Confira a [**Matriz de Rastreabilidade**](docs/02-matriz-rastreabilidade.md) — cobertura por requisito

---

## Resumo da execução

| Métrica | Valor |
|---|---|
| Casos de teste planejados | 18 |
| Casos executados | 18 |
| Casos passados | 15 |
| Casos falhos | 3 |
| Bugs reportados | 3 (1 alta, 1 média, 1 baixa) |
| Cobertura de requisitos | 100% |

---

## Sobre o autor

Francisco Lima — QA em formação. Portfolio: [github.com/SEU_USUARIO](https://github.com/SEU_USUARIO)
