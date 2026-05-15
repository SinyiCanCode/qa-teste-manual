# BUG-003 — Título de tarefa é truncado silenciosamente no limite máximo

| Campo | Informação |
|---|---|
| **ID** | BUG-003 |
| **Título** | Título com 100 caracteres é salvo truncado sem aviso ao usuário |
| **Reportado por** | Francisco Lima |
| **Data** | 2026-05-15 |
| **Versão** | 1.0.0 (build #142) |
| **Ambiente** | Staging — Chrome 124 / Windows 11 |
| **Severidade** | Baixa |
| **Prioridade** | Média |
| **Status** | Aberto |
| **Caso de teste** | [CT-003.2](../casos-de-teste/CT-003-crud-tasks.md#ct-0032--título-no-limite-máximo) |
| **Requisito** | RF-03 |

---

## Resumo

A documentação especifica que o título de uma tarefa pode ter até **100 caracteres**. Ao inserir exatamente 100 caracteres, a tarefa é criada, mas o título é **truncado para 95 caracteres** sem qualquer mensagem ao usuário. Há uma divergência entre o limite documentado e o aplicado pelo backend.

---

## Passos para reproduzir

1. Autenticar e acessar o dashboard
2. Clicar em **"Nova tarefa"**
3. No campo **"Título"**, colar a seguinte string de 100 caracteres:

   ```
   Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et
   ```

4. Preencher os demais campos com valores válidos
5. Clicar em **"Salvar"**
6. Localizar a tarefa criada na lista e clicar para abrir os detalhes

---

## Resultado esperado

Uma das duas opções:

- **Opção A:** título salvo com 100 caracteres íntegros (alinhar backend ao documentado).
- **Opção B:** se o limite real é 95, o frontend deve bloquear digitação além desse limite **e** exibir contador "X/95" abaixo do campo.

---

## Resultado obtido

- Tarefa é criada sem erro.
- Título exibido na lista: 95 caracteres (cortado em `... incididunt ut labo`).
- Nenhuma mensagem de aviso é exibida.
- Usuário não percebe a perda de informação.

---

## Evidências

- `evidencias/bug-003-titulo-100-chars.png` — campo preenchido com 100 caracteres
- `evidencias/bug-003-titulo-truncado.png` — título truncado na listagem
- `evidencias/bug-003-detalhe-tarefa.png` — detalhe mostrando 95 caracteres salvos

---

## Análise de impacto

- **Funcional:** perda silenciosa de dados.
- **Confiança:** quebra o contrato implícito de "o que digito é o que salvo".
- **Documentação:** divergência entre spec e implementação — outras divergências similares podem existir.

---

## Sugestão de correção

1. **Decidir o limite real** com o time de produto (100 ou 95).
2. **Alinhar três camadas:**
   - Frontend: atributo `maxLength` no input
   - Backend: validação explícita rejeitando títulos acima do limite
   - Banco de dados: coluna com tamanho compatível
3. **Adicionar contador visual** no campo (ex: `87/100`) para feedback ao usuário.
4. **Adicionar teste automatizado** que verifique o limite após a correção.

---

## Observações

- Comportamento semelhante deve ser verificado no campo "Descrição".
- Sugiro auditar todos os campos de texto da aplicação para identificar truncamentos silenciosos.
