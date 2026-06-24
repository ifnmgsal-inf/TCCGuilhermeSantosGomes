
# PARTE 2

---

# Movimentações — Saídas — Cadastro (API — POST /expense)

#Passou**CT_71: Cadastro de Movimentação com Todos os Campos Obrigatórios Válidos**

**Dado:** que o usuário está autenticado e existem projeto e conta bancária cadastrados

**Quando:** é enviada uma requisição POST para `/expense` com o body certo

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"` e o `id` da movimentação criada

---

#Sugestão #Passou **CT_72: Cadastro com Título Nulo (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com o campo `title` como `null`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou erro de campo obrigatório

- [ ] (Mostrar onde está o erro)

<img width="1175" height="417" alt="image" src="https://github.com/user-attachments/assets/f19dc194-60f0-4c06-bdcc-94d32316690c" />


---

#Sugestão  #Passou**CT_73: Cadastro com Valor Nulo (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com o campo `value` como `null`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error

- [ ] (Não é mostrado onde está o erro)

<img width="1179" height="404" alt="image" src="https://github.com/user-attachments/assets/1bcb7fe9-ec89-46a8-b746-5cc08a69765a" />


---

#Sugestão  #Passou**CT_74: Cadastro com Data Nula (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com o campo `date` como `null`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error

- [ ] (Não é mostrado onde está o erro)

<img width="1158" height="422" alt="image" src="https://github.com/user-attachments/assets/f5d6337e-786b-44a9-bfcc-c4788dc32470" />


---

#Falhou **CT_75: Cadastro com Valor Negativo**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com `value` = `"-100.00"`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna erro de validação ou HTTP 500 (valor de pagamento não deve ser negativo)

- [ ] (Aceitou o valor negativo)

---

#Sugestão #Passou**CT_76: Cadastro com Valor em Formato Inválido (Letras)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com `value` = `"abc"`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error por tipo de dado inválido

- [ ] (Mostrar onde está o erro)

<img width="1193" height="413" alt="image" src="https://github.com/user-attachments/assets/10d6c22c-fafd-49ee-89bc-ad7559ed5a30" />


---

#Passou**CT_77: Cadastro com Data em Formato Inválido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com `date` = `"32/13/2024"`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou erro de formato de data

---

#Passou **CT_78: Cadastro com Data Contendo Caracteres Especiais**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com `date` = `"@@/##/$$$$"`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error

---

#Sugestão  #Passou**CT_79: Cadastro com bankAccountId Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com `bankAccountId` = `9999`

**E:** os demais campos obrigatórios estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error por violação de chave estrangeira

- [ ] (Mostrar onde foi o erro)

<img width="1180" height="356" alt="image" src="https://github.com/user-attachments/assets/c13e0cdb-1447-4abc-a02c-d3eec97cba6f" />


---

#Passou **CT_80: Cadastro sem Token de Autenticação**

**Dado:** que o usuário não está autenticado

**Quando:** é enviada uma requisição POST para `/expense` com body válido e sem o header `Authorization`

**Então:** o sistema retorna HTTP 401 — Unauthorized

<img width="1054" height="439" alt="image" src="https://github.com/user-attachments/assets/db7447f9-0ac8-4d86-8832-c5aa29619532" />


---

# Movimentações — Saídas — Listagem e Busca (GET /expense e GET /expense/{id})

#Passou **CT_81: Listar Todas as Movimentações com Token Válido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/expense`

**Então:** o sistema retorna HTTP 200 com a lista de despesas cadastradas

<img width="1181" height="568" alt="image" src="https://github.com/user-attachments/assets/f4107d07-a250-4c8f-aa43-f8391645ba23" />


---

#Passou **CT_82: Buscar Movimentação por ID Existente**

**Dado:** que existe uma despesa com `id = 1` e o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/expense/1`

**Então:** o sistema retorna HTTP 200 com os dados completos da despesa

<img width="1179" height="369" alt="image" src="https://github.com/user-attachments/assets/f7596c55-2b10-4bda-a123-c9b7ae3680bd" />


---

#Passou**CT_83: Buscar Movimentação por ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/expense/9999`

**Então:** o sistema retorna HTTP 404 — Not Found

<img width="1018" height="226" alt="image" src="https://github.com/user-attachments/assets/26e154d0-65e9-4c48-9a09-112f243e3b4f" />


---

# Movimentações — Saídas — Edição (PUT /expense/{id})

#Passou **CT_84: Editar Movimentação com Dados Válidos**

**Dado:** que existe uma despesa com `id = 589` e o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/expense/589` com o body:

```json
{
  "title": "Pagamento Atualizado - Teste TCC",
  "value": "3000.00",
  "date": "2024-07-01T00:00:00Z",
  "bankAccountId": 31,
  "categoryId": null,
  "authorId": 1
}
```

**Então:** o sistema retorna HTTP 200 e os dados da despesa são atualizados

<img width="945" height="380" alt="image" src="https://github.com/user-attachments/assets/a955e14b-efd2-4dec-bd3c-c47235b7f639" />


---

#Sugestão #Passou**CT_85: Editar Movimentação com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/expense/9999` com body válido

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou 404

- [ ] (Mostrar qual o erro)

<img width="1182" height="300" alt="image" src="https://github.com/user-attachments/assets/536bd564-9e1f-4832-9945-0d9ff6ba931d" />


---

# Movimentações — Saídas — Exclusão (DELETE /expense/{id})

#Passou**CT_86: Excluir Movimentação Existente**

**Dado:** que existe uma despesa com `id = 592` e o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/expense/592`

**Então:** o sistema retorna HTTP 200 com mensagem de sucesso

<img width="948" height="223" alt="image" src="https://github.com/user-attachments/assets/3db76fdf-91e9-4fd6-b965-e4a5ed8ec491" />


---

#Sugestão #Passou**CT_87: Excluir Movimentação com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/expense/9999`

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou 404

- [ ] (Mostrar o erro)

<img width="1052" height="217" alt="image" src="https://github.com/user-attachments/assets/0c22a1ba-fdd8-46d4-ad5a-49f8ac7016a1" />


---

# Movimentações — Saídas — Tela (Frontend)

#Passou**CT_88: Verificar Máscara do Campo "Data" no Formulário (dd/mm/aaaa)**

**Dado:** que o usuário está no formulário de cadastro de movimentação de saída

**Quando:** o usuário digita uma data no campo "Data"

**Então:** o sistema aplica a máscara `dd/mm/aaaa` automaticamente

<img width="239" height="78" alt="image" src="https://github.com/user-attachments/assets/13a36add-5f14-44dc-bf30-34ca97b43165" />


---

#Passou **CT_89: Selecionar Projeto Atualiza Automaticamente o Campo "Conta Debitada"**

**Dado:** que o usuário está no formulário de cadastro de movimentação de saída

**E:** existe um projeto com conta bancária vinculada

**Quando:** o usuário seleciona um projeto no campo "Projeto"

**Então:** o campo "Conta Debitada" é atualizado automaticamente para refletir a conta vinculada ao projeto escolhido

<img width="986" height="401" alt="image" src="https://github.com/user-attachments/assets/daecfcf3-6bc8-4a49-8454-7005d9f09da4" />

<img width="975" height="390" alt="image" src="https://github.com/user-attachments/assets/c34c791a-8a65-4f12-9143-36d4ecfc5a24" />


---

#Passou **CT_90: Botão 'Limpar' Esvazia Todos os Campos do Formulário de Movimentação**

**Dado:** que o usuário preencheu todos os campos do formulário de movimentação de saída

**Quando:** o usuário clica no botão "Limpar"

**Então:** todos os campos do formulário são redefinidos ao estado inicial

<img width="973" height="396" alt="image" src="https://github.com/user-attachments/assets/61e698db-b111-4732-8e35-ecd6469f0638" />

<img width="990" height="398" alt="image" src="https://github.com/user-attachments/assets/6a10d09d-c23e-41ce-a660-2820e68bd630" />


---

#Passou**CT_91: Botão 'Cadastrar' Registra Movimentação com Campos Obrigatórios Válidos**

**Dado:** que o usuário preencheu corretamente os campos obrigatórios (Título, Projeto, Valor e Data)

**Quando:** o usuário clica no botão "Cadastrar"

**Então:** o sistema registra a movimentação e exibe mensagem de sucesso


---

#Passou**CT_92: Tentar Cadastrar Movimentação sem Preencher Campos Obrigatórios**

**Dado:** que o usuário está no formulário de cadastro de movimentação de saída com campos obrigatórios vazios

**Quando:** o usuário clica no botão "Cadastrar"

**Então:** o sistema exibe mensagem de validação indicando campos obrigatórios não preenchidos e não prossegue com o cadastro

- [ ] (O ideal é a mensagem estar presente em todos os campos obrigatórios, preenchendo apenas os campos em que aparecem a mensagem quando você vai 'Cadastrar' novamente o sistema não mostra nenhum tipo de erro e não cadastra, a tela fica sem ação).

<img width="962" height="489" alt="image" src="https://github.com/user-attachments/assets/94762e6f-bb16-4983-a2cf-58e74ed37c1a" />

<img width="968" height="440" alt="image" src="https://github.com/user-attachments/assets/c9abf58d-943f-4db7-bcd1-360bf05d6c48" />


---

#Passou**CT_93: Botão Voltar na Edição Retorna sem Salvar**

**Dado:** que o usuário está no formulário de edição de uma movimentação com alterações não salvas

**Quando:** o usuário clica no botão "Voltar"

**Então:** o sistema retorna à página anterior sem salvar as alterações realizadas

<img width="985" height="393" alt="image" src="https://github.com/user-attachments/assets/f8d0aece-731f-49ab-ad1c-21871de762ba" />

<img width="742" height="57" alt="image" src="https://github.com/user-attachments/assets/bf302369-f128-43d7-b5a8-4e570dc48c66" />


---

#Passou **CT_94: Relatório de Movimentações — Pesquisa pelo Título**

**Dado:** que o usuário está na tela de relatórios de movimentações com registros cadastrados

**Quando:** o usuário digita um título no campo de pesquisa

**Então:** o sistema filtra e exibe apenas as movimentações cujo título corresponde ao texto buscado

<img width="678" height="395" alt="image" src="https://github.com/user-attachments/assets/61875263-3323-4b4f-a895-cd0e4aedae99" />


---

#Passou**CT_95: Relatório de Movimentações — Download em .xlsx Sem Itens Selecionados**

**Dado:** que o usuário está na tela de relatórios de movimentações com registros cadastrados e nenhum item selecionado

**Quando:** o usuário clica no botão de download `.xlsx`

**Então:** o sistema exporta todos os registros de movimentações no arquivo `.xlsx`

<img width="191" height="61" alt="image" src="https://github.com/user-attachments/assets/a8d3481f-8ad6-4c72-a257-367e21abd39f" />


---

#Falhou**CT_96: Relatório de Movimentações — Download em .xlsx com Itens Selecionados**

**Dado:** que o usuário está na tela de relatórios de movimentações e selecionou 2 movimentações

**Quando:** o usuário clica no botão de download `.xlsx`

**Então:** o sistema exporta apenas os 2 registros selecionados no arquivo `.xlsx`

- [ ] (Mesmo selecionando as movimentações, é feita o download de todos as movimentações e não somente as que selecionei)

<img width="1001" height="461" alt="image" src="https://github.com/user-attachments/assets/31abda16-6fbd-43cd-87a9-e31a2b40dd7d" />


---

#Passou**CT_97: Visualizar Detalhes de uma Movimentação pelo Botão Visualizar**

**Dado:** que o usuário está na tela de relatórios de movimentações

**Quando:** o usuário clica no botão "Visualizar" de uma movimentação

**Então:** o sistema exibe uma janela flutuante com todos os detalhes da movimentação e do projeto vinculado (descrição, saldo anterior, valor, saldo atual, data, conta bancária, nome e e-mail do coordenador)

<img width="715" height="924" alt="image" src="https://github.com/user-attachments/assets/7067e820-8787-4806-b6db-93635e48593d" />


---

#Passou**CT_98: Excluir Movimentação pelo Botão Excluir — Feedback de Sucesso**

**Dado:** que o usuário está na tela de relatórios de movimentações

**Quando:** o usuário clica no botão "Excluir" de uma movimentação existente

**Então:** o sistema exclui a movimentação e exibe feedback visual de sucesso

(O feedback de sucesso ou erro aparece no final esquerdo da página, fica confuso a leitura talvez seja melhor um moodal centralizado com essa informação)

<img width="243" height="163" alt="image" src="https://github.com/user-attachments/assets/753bd8cd-daa7-42b0-891d-860809baa612" />

<img width="327" height="119" alt="image" src="https://github.com/user-attachments/assets/bf9f61ea-6d7b-4f46-bdbf-7c4792fbca58" />


---

# Investimentos — Cadastro (API — POST /investment)

#Passou**CT_99: Cadastro de Investimento com Todos os Campos Válidos**

**Dado:** que o usuário está autenticado e existem uma conta de débito (não investimento) e uma conta de investimento cadastradas

**Quando:** é enviada uma requisição POST para `/investment` com o body:

```json
{
  "value": "5000.00",
  "date": "2024-06-01T00:00:00Z",
  "description": "Investimento em cursos on-line",
  "bankAccountId": 1,
  "bankInvestmentId": 2
}
```

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"` e o `id` do investimento criado


<img width="1178" height="395" alt="image" src="https://github.com/user-attachments/assets/335cd5d3-a9a9-453d-92ac-41aefd20468e" />


---

#Falhou **CT_100: Cadastro de Investimento com Conta de Débito do Tipo "Investimento" (Regra de Negócio)**

**Dado:** que o usuário está autenticado e a conta com `bankAccountId = 3` é do tipo "Investimento"

**Quando:** é enviada uma requisição POST para `/investment` com `bankAccountId` = `3` (conta investimento como débito)

**E:** os demais campos estão válidos

**Então:** o sistema retorna erro bloqueando a operação, pois não é permitido debitar de uma conta do tipo Investimento

<img width="1024" height="296" alt="image" src="https://github.com/user-attachments/assets/80a895a1-d53b-4f90-ae27-6bf58b130ce1" />


---

#Falhou **CT_101: Cadastro de Investimento com Conta de Débito Igual à Conta de Investimento**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `bankAccountId` = `2` e `bankInvestmentId` = `2` (mesma conta)

**E:** os demais campos estão válidos

**Então:** o sistema retorna erro bloqueando a operação (conta de débito e conta de investimento não podem ser a mesma)

<img width="969" height="304" alt="image" src="https://github.com/user-attachments/assets/44ffe1dc-4abd-4d90-9dee-af520b46049e" />


---

#Passou**CT_102: Cadastro de Investimento com Valor Nulo**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `value` = `null`

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error

<img width="1122" height="301" alt="image" src="https://github.com/user-attachments/assets/b9ea5e20-0464-42d0-b3cd-f0a7651f070a" />


---

#Falhou **CT_103: Cadastro de Investimento com Valor Negativo**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `value` = `"-1000.00"`

**E:** os demais campos estão válidos

**Então:** o sistema retorna erro de validação ou HTTP 500

- [ ] (Pela API não realiza o controle desse valor negativo)
<img width="1183" height="355" alt="image" src="https://github.com/user-attachments/assets/92a5fe61-5ca6-472d-9096-5c67d634cb52" />


---

#Passou**CT_104: Cadastro de Investimento com Valor Grande (NUMERIC 16,2)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `value` = `"99999999999999.99"`

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"`

- [ ] (Aceitou mais caracteres que o NUMERIC(16,2)) e quando isso ocorreu converteu o número.)
<img width="1188" height="351" alt="image" src="https://github.com/user-attachments/assets/b52f8662-0d0d-425c-a14e-67690b2ccac4" />


---

#Passou**CT_105: Cadastro de Investimento com Data em Formato Inválido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `date` = `"data-invalida"`

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error

---

#Passou**CT_106: Cadastro de Investimento com bankAccountId Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com `bankAccountId` = `9999`

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error por violação de chave estrangeira


---

#Passou **CT_107: Cadastro de Investimento sem Token de Autenticação**

**Dado:** que o usuário não está autenticado

**Quando:** é enviada uma requisição POST para `/investment` com body válido e sem o header `Authorization`

**Então:** o sistema retorna HTTP 401 — Unauthorized


---

# Investimentos — Listagem e Busca (GET /investment e GET /investment/{id})

#Passou **CT_108: Listar Todos os Investimentos com Token Válido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/investment`

**Então:** o sistema retorna HTTP 200 com a lista de investimentos cadastrados


---

#Passou **CT_109: Buscar Investimento por ID Existente**

**Dado:** que existe um investimento com `id = 13` e o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/investment/13`

**Então:** o sistema retorna HTTP 200 com os dados completos do investimento


---

#Passou **CT_110: Buscar Investimento por ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/investment/9999`

**Então:** o sistema retorna HTTP 404 — Not Found


---

# Investimentos — Edição (PUT /investment/{id})

#Passou **CT_111: Editar Valor e Descrição do Investimento com Dados Válidos**

**Dado:** que existe um investimento com `id = 12` e o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/investment/12` com o body:

```json
{
  "value": "8000.00",
  "date": "2024-08-01T00:00:00Z",
  "description": "Atualização do investimento",
  "bankAccountId": 1,
  "bankInvestmentId": 2
}
```

**Então:** o sistema retorna HTTP 200 e os dados do investimento são atualizados


---
# Investimentos — Exclusão (DELETE /investment/{id})

#Passou **CT_112: Excluir Investimento Existente**

**Dado:** que existe um investimento com `id = 10` e o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/investment/10`

**Então:** o sistema retorna HTTP 200 com mensagem de sucesso


---

#Passou **CT_113: Excluir Investimento com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/investment/9999`

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou 404


---

# Investimentos — Tela (Frontend)

#Passou**CT_114: Campo "Conta para Débito" Não Lista Contas do Tipo Investimento**

**Dado:** que o usuário está no formulário de cadastro de investimento

**Quando:** o usuário acessa o campo "Selecione a conta para o débito"

**Então:** contas do tipo "Investimento" não aparecem como opção de débito



---

#Passou**CT_115: Verificar Exibição do Saldo da Conta Debitada ao Selecionar a Conta**

**Dado:** que o usuário está no formulário de cadastro de investimento

**Quando:** o usuário seleciona uma conta no campo "Selecione a conta para o débito"

**Então:** o sistema exibe o saldo atual da conta selecionada no campo "Saldo da conta bancária debitada"



---

#Passou**CT_116: Verificar Máscara do Campo "Data" no Formulário de Investimento (dd/mm/aaaa)**

**Dado:** que o usuário está no formulário de cadastro de investimento

**Quando:** o usuário digita uma data no campo "Data"

**Então:** o sistema aplica a máscara `dd/mm/aaaa` automaticamente



---

#Passou **CT_117: Botão Limpar Esvazia Todos os Campos do Formulário de Investimento**

**Dado:** que o usuário preencheu os campos do formulário de cadastro de investimento

**Quando:** o usuário clica no botão "Limpar"

**Então:** todos os campos são redefinidos ao estado inicial


---

#Passou **CT_118: Botão Cadastrar Registra Investimento com Campos Válidos**

**Dado:** que o usuário preencheu corretamente todos os campos do formulário de investimento

**Quando:** o usuário clica no botão "Cadastrar"

**Então:** o sistema registra o investimento e exibe mensagem de sucesso

- [ ] (A mensagem de sucesso aparece no fim da página, o interessante seria algo como uma moodal central com essa informação)


---

#Passou **CT_119: Relatório de Investimentos — Pesquisa pela Descrição**

**Dado:** que o usuário está na tela de relatórios de investimentos com registros cadastrados

**Quando:** o usuário digita uma descrição no campo de pesquisa

**Então:** o sistema filtra e exibe apenas os investimentos cuja descrição corresponde ao texto buscado


---

#Passou **CT_120: Relatório de Investimentos — Download em .xlsx Sem Itens Selecionados**

**Dado:** que o usuário está na tela de relatórios de investimentos com registros cadastrados e nenhum item selecionado

**Quando:** o usuário clica no botão de download `.xlsx`

**Então:** o sistema exporta todos os registros de investimentos no arquivo `.xlsx`


---

#Falhou  **CT_121: Relatório de Investimentos — Download em .xlsx com Itens Selecionados**

**Dado:** que o usuário está na tela de relatórios de investimentos e selecionou 1 investimento

**Quando:** o usuário clica no botão de download `.xlsx`

**Então:** o sistema exporta apenas o registro selecionado no arquivo `.xlsx`

- [ ] (Mesmo selecionando, o arquivo baixado vem o geral)



---

#Passou**CT_122: Visualizar Detalhes de um Investimento pelo Botão Visualizar**

**Dado:** que o usuário está na tela de relatórios de investimentos

**Quando:** o usuário clica no botão "Visualizar" de um investimento

**Então:** o sistema exibe uma janela flutuante com todos os detalhes: descrição, valor, data, conta bancária debitada (nome, agência, número, titular, saldo, tipo) e conta bancária investida (nome, agência, número, titular, saldo, tipo)

---

#Passou **CT_123: Excluir Investimento pelo Botão Excluir na Tela de Relatórios**

**Dado:** que o usuário está na tela de relatórios de investimentos

**Quando:** o usuário seleciona um investimento e clica no botão "Excluir"

**Então:** o sistema exclui o investimento e exibe feedback visual de sucesso

- [ ] (O modal fica perto da linha esquerda, a visualização fica defasada, ideal seria centralização)



---
