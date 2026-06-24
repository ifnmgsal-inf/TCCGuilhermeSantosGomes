
# Login (Front-end)

#Passou **CT_1: E-mail e Senha Corretos com Usuário Existente**

**Dado:** que o usuário possui cadastro ativo no sistema

**Quando:** o usuário acessa a tela de login, preenche o campo "E-mail do usuário" com `carlos.silva@example.com` e o campo "Senha do usuário" com `senha123`

**E:** clica no botão "Entrar"

**Então:** o sistema autentica o usuário e redireciona para a tela inicial (dashboard)

---

#Passou **CT_2: E-mail com Formato Inválido e Senha Correta**

**Dado:** que o usuário está na tela de login

**Quando:** o usuário preenche o campo "E-mail do usuário" com `carlos.silva` (sem @) e o campo "Senha do usuário" com `senha123`

**E:** clica no botão "Entrar"

**Então:** o sistema exibe mensagem de erro de autenticação e não permite o acesso

---

#Passou **CT_3: E-mail Correto e Senha Incorreta**

**Dado:** que o usuário está na tela de login

**Quando:** o usuário preenche o campo "E-mail do usuário" com `carlos.silva@example.com` e o campo "Senha do usuário" com `senhaerrada`

**E:** clica no botão "Entrar"

**Então:** o sistema exibe mensagem de erro de autenticação e não permite o acesso

---

#Passou **CT_4: E-mail e Senha Ambos em Formato Incorreto**

**Dado:** que o usuário está na tela de login

**Quando:** o usuário preenche o campo "E-mail do usuário" com `usuarioinvalido` e o campo "Senha do usuário" com `123`

**E:** clica no botão "Entrar"

**Então:** o sistema exibe mensagem de erro de autenticação e não permite o acesso

---

#Passou **CT_5: Login com Campo de E-mail Vazio**

**Dado:** que o usuário está na tela de login

**Quando:** o usuário deixa o campo "E-mail do usuário" em branco e preenche a senha com `senha123`

**E:** clica no botão "Entrar"

**Então:** o sistema exibe mensagem de validação indicando que o campo e-mail é obrigatório e não prossegue com o login

---

#Passou **CT_6: Login com Campo de Senha Vazio**

**Dado:** que o usuário está na tela de login

**Quando:** o usuário preenche o campo "E-mail do usuário" com `carlos.silva@example.com` e deixa o campo "Senha do usuário" em branco

**E:** clica no botão "Entrar"

**Então:** o sistema exibe mensagem de validação indicando que o campo senha é obrigatório e não prossegue com o login


---

# Menu (Exploratórios — Frontend)#

#Passou **CT_7: Recolher Menu ao Clicar no Botão**

**Dado:** que o usuário está autenticado e o menu lateral está expandido

**Quando:** o usuário clica no botão de recolher menu

**Então:** os ícones do menu são recolhidos de forma responsiva, sem quebrar o layout

<img width="294" height="637" alt="image" src="https://github.com/user-attachments/assets/2bde1cf2-e905-4e6b-bc0a-e359759e4bc3" />


(Responsivos sem quebrar o layout)

---

#Passou **CT_8: Ícones do Menu São Clicáveis e Navegam para as Telas Corretas**

**Dado:** que o usuário está autenticado e o menu está visível

**Quando:** o usuário clica em cada ícone disponível no menu

**Então:** o sistema redireciona para a respectiva tela de cada ícone sem erros

---

#Passou **CT_9: Clicar no Ícone de Sair Desloga o Usuário**

**Dado:** que o usuário está autenticado e na aplicação

**Quando:** o usuário clica no ícone "Sair" no menu

**Então:** a sessão é encerrada e o usuário é redirecionado para a tela de login

---

#Passou **CT_10: Clicar nos Ícones FADETEC, SIFSOFT e IFNMG Retorna à Tela Inicial**

**Dado:** que o usuário está autenticado em qualquer tela do sistema

**Quando:** o usuário clica nos ícones FADETEC, SIFSOFT ou IFNMG

**Então:** o sistema retorna para a tela inicial (dashboard) da aplicação

---

#Passou**CT_11: Item Clicado no Menu Fica em Destaque**

**Dado:** que o usuário está autenticado e navegando pelo menu

**Quando:** o usuário clica em um item do menu

**Então:** o item clicado fica visivelmente em destaque (ex: cor diferente, borda ativa), indicando a seleção ativa

---

#Passou **CT_12: Item "Usuário" Exibe Nome e E-mail do Usuário Logado**

**Dado:** que o usuário está autenticado com nome e e-mail longos (ex: "Carlos Alberto de Souza Silva Pereira" / "carlos.alberto.souza.silva.pereira@instituicao.edu.br")

**Quando:** o usuário visualiza o item "Usuário" no menu

**Então:** o sistema exibe o nome e o e-mail completos, sem truncar de forma incorreta ou quebrar o layout do menu

---

# Contas Bancárias — Cadastro (API — POST /bankaccount)

#Passou **CT_13: Cadastro com Todos os Campos Válidos**

**Dado:** que o usuário está autenticado com token válido

**Quando:** é enviada uma requisição POST para `/bankaccount` com o body:

```json
{
  "name": "Banco do Brasil",
  "agency": "1234",
  "numberAccount": "56789-0",
  "owner": "João Silva",
  "value": "1000.50",
  "categoryAux": 1
}
```

**Então:** o sistema retorna HTTP 200 com a mensagem `"Inserido com sucesso!"` e o `id` da conta criada

<img width="1177" height="566" alt="image" src="https://github.com/user-attachments/assets/6ba33f9e-abc6-4bcc-95ba-6d84d020c9da" />


---

#Passou**CT_14: Cadastro com Nome do Banco com 1000 Caracteres (Limite Máximo)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o campo `name` contendo exatamente 1000 caracteres (string "A" repetida 1000 vezes)

**E:** os demais campos estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"`

<img width="1177" height="566" alt="image" src="https://github.com/user-attachments/assets/f3a94a22-62bf-4be2-9a57-07a3cd0b0ea9" />


---

#Falhou**CT_15: Cadastro com Nome do Banco com 1001 Caracteres (Acima do Limite)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o campo `name` contendo 1001 caracteres

**E:** os demais campos estão preenchidos com valores válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou rejeita a entrada com erro de validação

<img width="1174" height="589" alt="image" src="https://github.com/user-attachments/assets/846ec2f1-ca29-4467-b8e2-edc912b66b2d" />


- [ ] (Aceitou a requisição, não está sendo feito o controle de caracteres)


---

#Sugestão #Passou **CT_16: Cadastro com Nome do Banco Nulo (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o body:

```json
{
	"name": null,
	"agency": "1234",
	"numberAccount": "156178110",
	"owner": "Fadetec",
	"value": 1000,
	"categoryAux": 3
}
```

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou mensagem de campo obrigatório

<img width="1176" height="329" alt="image" src="https://github.com/user-attachments/assets/cccd44c1-252d-47ea-8dc5-c4dddc4945cc" />


---

#Falhou **CT_17: Cadastro com Nome do Banco Vazio**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o campo `name` como string vazia `""`

**Então:** o sistema retorna erro indicando que o campo não pode ser vazio

- [ ] (A API aceitou o campo vazio, mesmo sendo um campo obrigatório para preenchimento)

<img width="1191" height="308" alt="image" src="https://github.com/user-attachments/assets/d613320f-6cc2-49f4-a9f5-3142bdf54714" />


---

#Passou**CT_18: Cadastro com Nome do Banco Contendo Apenas Caracteres Especiais**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o body:

```json
{
  "name": "@#$%¨&*()",
  "agency": "1234",
  "numberAccount": "56711",
  "owner": "João Silva",
  "value": "1000.50",
  "categoryAux": 1
}
```

**Então:** o sistema retorna HTTP 200

<img width="953" height="307" alt="image" src="https://github.com/user-attachments/assets/5df096bf-e48d-4d79-b028-b8a9aa8253f1" />


---

#Sugestão #Passou **CT_19: Cadastro com Agência Nula (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o campo `agency` como `null`

**E:** os demais campos estão preenchidos com valores válidos

**Então:** o sistema retorna erro indicando campo obrigatório

<img width="1181" height="351" alt="image" src="https://github.com/user-attachments/assets/38034532-bff6-445b-b54b-24185adf66cb" />


---

#Falhou **CT_20: Cadastro com Agência Vazio**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o campo `agency` como string vazia `""`

**Então:** o sistema retorna erro indicando que o campo não pode ser vazio

- [ ] (A API aceitou o campo vazio, mesmo sendo um campo obrigatório para preenchimento)

<img width="1192" height="318" alt="image" src="https://github.com/user-attachments/assets/3f4feb6e-3844-42a6-93e2-99588e4011a5" />


---

#Falhou **CT_21: Cadastro com Saldo Negativo**

**Dado:** que o usuário está autenticado e o tipo de conta é diferente de "Projeto" (`categoryAux` != código de Projeto)

**Quando:** é enviada uma requisição POST para `/bankaccount` com o body:

```json
{
  "name": "Banco X",
  "agency": "0001",
  "numberAccount": "00001-0",
  "owner": "Maria",
  "value": "-500.00",
  "categoryAux": 2
}
```

**Então:** o sistema valida e retorna erro ou aceita, conforme regra de negócio definida

- [ ] (Não era para o sistema aceitar, pois conforme o front não é deixado digitar caracteres)

<img width="1176" height="348" alt="image" src="https://github.com/user-attachments/assets/2a8cca58-fcf7-4d7c-823e-29105a9dc0ff" />


---

#Falhou **CT_22: Cadastro com Tipo "Projeto" e Saldo Informado**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com `categoryAux` correspondente ao tipo "Projeto" e o campo `value` preenchido com `"100"`

**Então:** o sistema ignora o saldo ou retorna erro, pois o campo não é habilitado para contas do tipo Projeto

- [ ] (Não é feito tratamento dessa condição do campo 'Saldo' não ser preenchido quando o tipo é 'Projeto')

<img width="1182" height="321" alt="image" src="https://github.com/user-attachments/assets/e47693e3-f32e-46b0-8feb-003671fbd123" />


---

#Passou **CT_23: Cadastro com Tipo de Conta Nulo (Campo Obrigatório)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com o body:

```json
{
  "name": "Banco X",
  "agency": "0001",
  "numberAccount": "00001-0",
  "owner": "Maria",
  "value": "100.00",
  "categoryAux": null
}
```

**Então:** o sistema retorna HTTP 500 ou mensagem de campo obrigatório

<img width="1189" height="296" alt="image" src="https://github.com/user-attachments/assets/45d96d88-395a-4038-a06d-5619622a0ef5" />


---

#Passou **CT_24: Cadastro com Saldo Contendo Letras no Valor**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/bankaccount` com `value` = `"abc"`

**E:** os demais campos estão preenchidos com valores válidos

**Então:** o sistema retorna erro de tipo inválido ou HTTP 500

<img width="1187" height="319" alt="image" src="https://github.com/user-attachments/assets/37dcd8de-a160-47c1-b105-e9b8b5f7dddc" />


---

# Contas Bancárias — Listagem (API — GET /bankaccount)

#Passou**CT_25: Listar Todas as Contas Bancárias com Token Válido**

**Dado:** que o usuário está autenticado com token válido

**Quando:** é enviada uma requisição GET para `/bankaccount`

**Então:** o sistema retorna HTTP 200 com a lista de contas bancárias cadastradas

<img width="1178" height="564" alt="image" src="https://github.com/user-attachments/assets/8d5ab6ec-d664-437a-ab6f-634912ab6a86" />


---

#Passou**CT_26: Listar Contas Bancárias sem Token**

**Dado:** que o usuário não está autenticado

**Quando:** é enviada uma requisição GET para `/bankaccount` sem o header `Authorization`

**Então:** o sistema retorna HTTP 401 — Unauthorized

<img width="1192" height="405" alt="image" src="https://github.com/user-attachments/assets/700ff3aa-8876-43b3-ba46-705b37770c03" />


---

#Passou**CT_27: Buscar Conta Bancária por ID Existente (GET /bankaccount/{id})**

**Dado:** que existe uma conta bancária com `id = 51` no sistema e o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/bankaccount/51`

**Então:** o sistema retorna HTTP 200 com os dados da conta correspondente

<img width="1184" height="377" alt="image" src="https://github.com/user-attachments/assets/8cbdbe9a-a802-4fb4-a819-3910c171d52c" />


---

#Passou **CT_28: Buscar Conta Bancária por ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/bankaccount/9999` (ID não cadastrado)

**Então:** o sistema retorna HTTP 404 — `"Conta bancária não encontrada!"`

<img width="1193" height="232" alt="image" src="https://github.com/user-attachments/assets/f36d30a9-396d-4a13-9ca3-82b2fbce9341" />


---

# Contas Bancárias — Edição (API — PUT /bankaccount/{id})

#Passou **CT_29: Editar Nome do Banco com Valor Válido**

**Dado:** que existe uma conta bancária com `id = 50` e o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/bankaccount/50` com o body:

```json
{
  "name": "TESTES API TCC",
  "agency": "0001",
  "numberAccount": "5679989-0",
  "owner": "João Silva TESTE",
  "value": 100,
  "categoryAux": 2
}
```

**Então:** o sistema retorna HTTP 200 e os dados da conta são atualizados

<img width="1189" height="403" alt="image" src="https://github.com/user-attachments/assets/5a77b289-88a4-4393-b2b2-53fdf976d447" />


---

#Passou **CT_30: Tentar Editar Número da Conta**

**Dado:** que existe uma conta bancária com `id = 50` e o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/bankaccount/50` com o campo `numberAccount` alterado para `"99999-9"`

**Então:** o sistema retorna HTTP 200 e os dados da conta são atualizados

<img width="1184" height="410" alt="image" src="https://github.com/user-attachments/assets/a07506f4-20da-4a51-800c-597bc1803af4" />


---

#Passou **CT_31: Editar Conta com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/bankaccount/9999` com body válido
 
**Então:** o sistema retorna HTTP 500 — Internal Server Error ou 404

<img width="1195" height="303" alt="image" src="https://github.com/user-attachments/assets/3fddd79b-a2fa-4c9d-ac51-086f7897bef0" />


---

# Contas Bancárias — Exclusão (API — DELETE /bankaccount/{id})

#Passou**CT_32: Excluir Conta Bancária sem Vínculo**

**Dado:** que existe uma conta bancária com `id = 5` sem vínculo com projetos, investimentos ou despesas

**E:** o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/bankaccount/5`

**Então:** o sistema retorna HTTP 200 — `"Conta bancária excluída com sucesso!"`

<img width="1194" height="225" alt="image" src="https://github.com/user-attachments/assets/bc48d359-63b0-41a7-baeb-8079d7467016" />


---

#Passou **CT_33: Tentar Excluir Conta Bancária Vinculada a um Projeto**

**Dado:** que existe uma conta bancária com `id = 32` vinculada a um projeto ativo

**E:** o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/bankaccount/32`

**Então:** o sistema retorna HTTP 500 com mensagem de erro indicando que a conta está em uso

<img width="536" height="333" alt="image" src="https://github.com/user-attachments/assets/0e2fcb42-db5c-4d2f-b9b6-21c4d289336c" />

<img width="1198" height="347" alt="image" src="https://github.com/user-attachments/assets/259ff255-5e67-48f7-a443-a9ac155a93c3" />

<img width="1185" height="260" alt="image" src="https://github.com/user-attachments/assets/9cb21a5a-cabe-4bb0-830b-429868099c5a" />


---

#Passou**CT_34: Excluir Conta Bancária com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/bankaccount/9999`

**Então:** o sistema retorna HTTP 404 — `"Conta bancária não encontrada!"`

<img width="1192" height="222" alt="image" src="https://github.com/user-attachments/assets/feb5cffb-b177-473f-91af-ad95f079ee0e" />


---

# Contas Bancárias — Tela (Frontend)

#Passou**CT_35: Visualizar Detalhes da Conta com Nome Muito Longo**

**Dado:** que existe uma conta bancária com nome de 1000 caracteres cadastrada

**Quando:** o usuário clica no botão "Visualizar" na listagem de contas

**Então:** a janela flutuante exibe o nome completo sem truncar de forma incorreta, com layout íntegro

<img width="1000" height="744" alt="image" src="https://github.com/user-attachments/assets/1db45696-d150-45d4-b261-69f8ff63e3ef" />


---

#Passou**CT_36: Verificar Máscara do Saldo na Visualização**

**Dado:** que existe uma conta bancária com `value = "100"`

**Quando:** o usuário clica em "Visualizar"

**Então:** o sistema exibe o saldo formatado como `R$ 100.00`

<img width="234" height="518" alt="image" src="https://github.com/user-attachments/assets/9e820f82-97cc-4267-92f7-4528110984ad" />

<img width="1181" height="344" alt="image" src="https://github.com/user-attachments/assets/52a7459f-7028-4cb7-adbf-efbf416581ce" />


---

#Passou**CT_37: Botão Editar Redireciona para o Formulário de Edição**

**Dado:** que o usuário está na listagem de contas bancárias

**Quando:** o usuário clica no botão "Editar" de uma conta

**Então:** o sistema redireciona imediatamente para o formulário de edição com os dados da conta preenchidos

<img width="976" height="401" alt="image" src="https://github.com/user-attachments/assets/0d204591-aa76-4a33-9743-db00a4bfa3a2" />


---

#Passou**CT_38: Saldo Não Editável no Formulário de Edição**

**Dado:** que o usuário está no formulário de edição de uma conta bancária

**Quando:** o usuário tenta editar o campo "Saldo da Conta"

**Então:** o campo está desabilitado e não permite alteração

<img width="976" height="401" alt="image" src="https://github.com/user-attachments/assets/44e486f1-c596-4016-901f-48f6fc37a6cc" />


---

#FalhouGrave #Falhou **CT_39: Botão Limpar no Formulário de Cadastro de Conta**

**Dado:** que o usuário preencheu todos os campos do formulário de cadastro de conta bancária

**Quando:** o usuário clica no botão "Limpar"

**Então:** todos os campos do formulário são esvaziados/redefinidos ao estado inicial

- [ ] (O botão 'Limpar' apaga todos os campos, porém quando o 'Tipo' está assinalado como 'Investimento' e você clica no botão 'Limpar' é redirecionado para o 'Tipo' 'Projeto' e assim o campo 'Saldo da conta' fica disponível para edição).


<img width="998" height="453" alt="image" src="https://github.com/user-attachments/assets/992311be-f438-4160-a25e-f6f298f96b8a" />


---

#Sugestão #Passou**CT_40: Botão Cadastrar com Campos Obrigatórios Preenchidos**

**Dado:** que o usuário preencheu todos os campos obrigatórios do formulário de conta bancária

**Quando:** o usuário clica no botão "Cadastrar"

**Então:** o sistema registra a conta e exibe mensagem de sucesso

- [ ] (A mensagem de sucesso aparece no canto esquerdo abaixo na tela, o que dificulta a visualização)

<img width="321" height="62" alt="image" src="https://github.com/user-attachments/assets/e4ea1e8d-f71d-4fdf-9366-ae78c8e29e72" />


---

#Passou**CT_41: Campo "Saldo da Conta" Desabilitado ao Selecionar Tipo "Projeto"**

**Dado:** que o usuário está no formulário de cadastro de conta bancária

**Quando:** o usuário seleciona o tipo "Projeto" no campo "Tipo de Conta Bancária"

**Então:** o campo "Saldo da Conta" é automaticamente desabilitado na interface

<img width="688" height="283" alt="image" src="https://github.com/user-attachments/assets/a748ef0c-3864-4b8b-aea0-9c7d794a876a" />


---

#Passou**CT_42: Preencher Saldo e Depois Mudar Tipo para "Projeto"**

**Dado:** que o usuário preencheu o campo "Saldo da Conta" com um valor válido com tipo 'Investimento'

**Quando:** o usuário altera o "Tipo de Conta Bancária" para "Projeto"

**Então:** o campo "Saldo da Conta" é desabilitado e o valor preenchido é limpo

<img width="688" height="164" alt="image" src="https://github.com/user-attachments/assets/6543b556-5fd8-40aa-b41e-f959c67e363b" />

<img width="652" height="164" alt="image" src="https://github.com/user-attachments/assets/ab8033c8-9cfc-4751-a96b-04916b9aba3e" />


---

# Projetos — Cadastro (API — POST /project)

#Passou**CT_43: Cadastro de Projeto com Todos os Campos Válidos**

**Dado:** que o usuário está autenticado e existe uma conta bancária, categoria, status e tipo de trabalho cadastrados

**Quando:** é enviada uma requisição POST para `/project` com o body:

```json
{
	"title": "TESTES API - TCC",
	"description": "FOI INSERIDO VIA API - TESTES",
	"value": 10,
	"startDate": "2024-01-01T00:00:00Z",
	"endDate": "2025-01-01T00:00:00Z",
	"instrumentValue": 1,
	"reservefundValue": 1,
	"doaValue": 1,
	"coordinatorName": "TEESTES API",
	"coordinatorEmail": "TESTES.API@gmail.br",
	"bankAccountId": 52,
	"categoryId": 9,
	"statusId": 3,
	"projectTypeWorkId": 4,
	"authorId": 2,
	"projectNumber": 150000000
}
```

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"` e o `id` do projeto criado

<img width="1192" height="506" alt="image" src="https://github.com/user-attachments/assets/26d516f5-a070-4e3a-adba-93889426b5cf" />

---

#Passou**CT_44: Cadastro de Projeto com Título de 500 Caracteres (Limite Máximo — char(500))**

**Dado:** que o usuário está autenticado e os campos relacionais estão válidos

**Quando:** é enviada uma requisição POST para `/project` com o campo `title` contendo exatamente 500 caracteres

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"`

<img width="1195" height="611" alt="image" src="https://github.com/user-attachments/assets/2968806b-5542-4656-9bdd-3db5e6bbd61b" />

---

#Sugestão #Passou**CT_45: Cadastro de Projeto com Título de 501 Caracteres (Acima do Limite)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com o campo `title` contendo 501 caracteres

**Então:** o sistema retorna HTTP 500 — Internal Server Error ou erro de validação

- [ ] (Aparecer onde o erro ocorreu)

<img width="1170" height="600" alt="image" src="https://github.com/user-attachments/assets/77964686-c9dd-43f5-b372-eff2b5394726" />


---

#Sugestão #Passou **CT_46: Cadastro de Projeto com Título Nulo**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com o campo `title` como `null`

**Então:** o sistema retorna HTTP 500 — Internal Server Error

- [ ] (Aparecer onde ocorreu o erro)

<img width="1178" height="490" alt="image" src="https://github.com/user-attachments/assets/303240c1-522f-4ae2-8df9-e0cc9e82a699" />


---

#Passou**CT_47: Cadastro de Projeto com Título Contendo Caracteres Especiais**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com o campo `title` = `"Projeto @#$% 2024!"`

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"` (caracteres especiais devem ser aceitos em campo TEXT)

<img width="1069" height="587" alt="image" src="https://github.com/user-attachments/assets/1fa742e8-978f-4308-9cd8-8199de718950" />


---

#FalhouGrave #Falhou **CT_48: Cadastro com Data de Término Menor que Data de Início**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com:

```json
{
  "startDate": "2025-06-01T00:00:00Z",
  "endDate": "2024-01-01T00:00:00Z"
}
```

**E:** os demais campos estão válidos

**Então:** o sistema retorna erro de validação indicando que a data de término deve ser maior que a data de início

- [ ] (Não retornou erro e aceitou a requisição da 'Data de encerramento' ser antes da 'Data de Inicio')

<img width="1189" height="605" alt="image" src="https://github.com/user-attachments/assets/89ee75c1-7277-41e2-aa87-6f0fee15fa53" />


---

#Passou **CT_49: Cadastro com Data de Início Igual à Data de Término**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `startDate` igual a `endDate`

**E:** os demais campos estão válidos

**Então:** o sistema valida e aceita, conforme regra de negócio

<img width="1186" height="576" alt="image" src="https://github.com/user-attachments/assets/ca8f7957-6d53-4029-9f33-667445db1723" />


---

#Passou**CT_50: Cadastro com Valor do Instrumento Grande (NUMERIC 16,2)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `instrumentValue` = `"99999999999999.99"` (14 dígitos inteiros, 2 decimais)

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"`

<img width="1189" height="617" alt="image" src="https://github.com/user-attachments/assets/84d79ff2-3390-4279-8dd6-94ae0aaca203" />


---

#Sugestão #Passou**CT_51: Cadastro com Valor do Instrumento Nulo**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `instrumentValue` = `null`

**Então:** o sistema retorna HTTP 500 ou erro de validação de campo obrigatório

- [ ] (Mostrar qual erro ocorreu)

<img width="1198" height="509" alt="image" src="https://github.com/user-attachments/assets/2df8d50a-3e47-4dab-8c7f-c63203bb6f33" />


---

#Falhou**CT_52: Cadastro com E-mail do Coordenador Sem Formato Válido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `coordinatorEmail` = `"emailinvalido"`

**E:** os demais campos estão válidos

**Então:** o sistema retorna erro de validação de formato de e-mail

- [ ] (Pela API foi aceito o campo coordinatorEmail sem a formatação ideal)

<img width="1189" height="591" alt="image" src="https://github.com/user-attachments/assets/5b9cab7c-4a3c-4295-9db3-beae106b9cb7" />


---

#FalhouGrave #Falhou  **CT_53: Cadastro com Conta Bancária Inexistente (bankAccountId inválido)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `bankAccountId` = `9999` (não existente)

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 500 — Internal Server Error por violação de chave estrangeira

- [ ] (Não existe esse bankAccountID e a API aceitou essa notificação)

<img width="1206" height="261" alt="image" src="https://github.com/user-attachments/assets/385bff10-d8aa-441b-b106-428c4140df1e" />


---

#Passou**CT_54: Cadastro com Porcentagem DOA Zerada (0,00)**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `doaValue` = `"0.00"`

**E:** os demais campos estão válidos

**Então:** o sistema retorna HTTP 200 com `"Inserido com sucesso!"

<img width="1194" height="594" alt="image" src="https://github.com/user-attachments/assets/97817025-d283-4576-9119-e386da0cb275" />


---

#Sugestão #Passou **CT_55: Cadastro com Porcentagem DOA Nula**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição POST para `/project` com `doaValue` = `null`

**Então:** o sistema retorna HTTP 500 ou erro de validação

- [ ] (Mostrar onde ocorreu o erro)

<img width="1163" height="508" alt="image" src="https://github.com/user-attachments/assets/a788f317-9598-4acf-891c-69130e34e09d" />


---

# Projetos — Listagem e Busca (API — GET /project e GET /project/{id})

#Passou**CT_56: Listar Todos os Projetos com Token Válido**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/project`

**Então:** o sistema retorna HTTP 200 com a lista de projetos cadastrados

<img width="1175" height="537" alt="image" src="https://github.com/user-attachments/assets/28564027-82b8-4103-9de6-07bb6f2be7d1" />


---

#Passou**CT_57: Buscar Projeto por ID Existente**

**Dado:** que existe um projeto com `id = 35' e o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/project/35`

**Então:** o sistema retorna HTTP 200 com os dados completos do projeto

<img width="1082" height="546" alt="image" src="https://github.com/user-attachments/assets/eb715767-1a6a-40e7-8b74-6bddae6a55a0" />


---

#Passou **CT_58: Buscar Projeto por ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição GET para `/project/9999`

**Então:** o sistema retorna HTTP 404 — Not Found

<img width="1176" height="226" alt="image" src="https://github.com/user-attachments/assets/a1c27155-7db8-4283-89f3-3f7fa4e0fb76" />


---

# Projetos — Edição (API — PUT /project/{id})

#Passou**CT_59: Editar Campos Editáveis do Projeto com Dados Válidos**

**Dado:** que existe um projeto com `id = 35` e o usuário está autenticado

**Quando:** é enviada uma requisição PUT para `/project/35` com o body:

**Então:** o sistema retorna HTTP 200 e os dados são atualizados

<img width="1195" height="611" alt="image" src="https://github.com/user-attachments/assets/ef1f584b-a467-40ae-8d28-2db4adeb09d9" />


---

# Projetos — Exclusão (API — DELETE /project/{id})

#Passou**CT_60: Excluir Projeto Existente sem Dependências**

**Dado:** que existe um projeto com `id = 35` sem despesas vinculadas e o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/project/35`

**Então:** o sistema retorna HTTP 200 com mensagem de sucesso

<img width="1186" height="257" alt="image" src="https://github.com/user-attachments/assets/5571dafc-19f8-43f6-a044-96039523ff8b" />



---

#Passou**CT_61: Excluir Projeto com ID Inexistente**

**Dado:** que o usuário está autenticado

**Quando:** é enviada uma requisição DELETE para `/project/9999`

**Então:** o sistema retorna HTTP 404 — Not Found ou HTTP 500

<img width="1185" height="228" alt="image" src="https://github.com/user-attachments/assets/860b45a8-712a-477a-ada5-fc0dd554ae8a" />


---

# Projetos — Tela (Frontend)

#Passou**CT_62: Verificar Conta Bancária Cadastrada Aparece no Select do Formulário**

**Dado:** que existe uma conta bancária cadastrada com tipo diferente de "Projeto"

**E:** o usuário acessa o formulário de cadastro de projeto

**Quando:** o usuário clica no campo "Conta Bancária"

**Então:** a conta bancária cadastrada não aparece como opção disponível no select

(Aparece apenas a conta bancária do tipo 'Projeto')
<img width="439" height="263" alt="image" src="https://github.com/user-attachments/assets/5ef426e5-d043-4e37-8e02-c1b6a9f53455" />



---

#Passou**CT_63: Verificar Máscara do Campo "Valor do Instrumento" (1.000.000,00)**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário digita `1000000` no campo "Valor do Instrumento"

**Então:** o sistema exibe o valor formatado como `1.000.000,00`

<img width="160" height="67" alt="image" src="https://github.com/user-attachments/assets/c56f117a-ca20-432b-86b2-07c9b40eece6" />


---

#Passou **CT_64: Verificar Máscara do Campo "Porcentagem DOA" (10,00)**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário digita `10` no campo "Porcentagem da DOA"

**Então:** o sistema exibe o valor formatado como `10,00`

<img width="132" height="81" alt="image" src="https://github.com/user-attachments/assets/ca81c271-2100-472d-aa58-ec3afbbe5707" />


---

#Passou **CT_65: Verificar Máscara do Campo "Data de Início" (dd/mm/aaaa)**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário digita uma data no campo "Data de Início"

**Então:** o sistema aplica a máscara `dd/mm/aaaa` automaticamente

(A máscara só funciona quando clica na data no calendário, caso digite direto como '17062026' a máscara não é aplicada)
<img width="140" height="72" alt="image" src="https://github.com/user-attachments/assets/fb1ca019-e9f6-44d1-b195-32eb8dd9ed2e" />


---

#Passou **CT_66: Verificar Máscara do Campo "Data de término" (dd/mm/aaaa)**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário digita uma data no campo "Data de término"

**Então:** o sistema aplica a máscara `dd/mm/aaaa` automaticamente

(A máscara só funciona quando clica na data no calendário, caso digite direto como '17062026' a máscara não é aplicada)
<img width="138" height="83" alt="image" src="https://github.com/user-attachments/assets/7f64f539-09b3-40df-b469-9ce81c9ce9ed" />



---

#Passou **CT_67: Status do Projeto Selecionável no Cadastro**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário acessa o campo "Status do Projeto"

**Então:** as opções de status disponíveis são exibidas para seleção

<img width="232" height="328" alt="image" src="https://github.com/user-attachments/assets/0ae54ce9-de0e-481a-9258-ff4ac2ce3048" />

<img width="250" height="244" alt="image" src="https://github.com/user-attachments/assets/8e8bdabc-ea51-48e9-9ebe-034d68a06ed7" />


---

#Falhou **CT_68: Botão Limpar no Formulário de Cadastro de Projeto**

**Dado:** que o usuário preencheu todos os campos do formulário de cadastro de projeto

**Quando:** o usuário clica no botão "Limpar"

**Então:** todos os campos são redefinidos ao estado inicial


- [ ] (O botão 'Limpar' não apaga as Datas)

<img width="992" height="637" alt="image" src="https://github.com/user-attachments/assets/fd0e1345-c7a2-4c3f-a401-10a263de215f" />


---

#Passou **CT_69: Nome do Coordenador com Acentos e Caracteres Especiais**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário preenche o campo "Nome do Coordenador" com `"José Ântônio Çoão"`

**Então:** o sistema aceita o valor e exibe corretamente em tela

<img width="195" height="71" alt="image" src="https://github.com/user-attachments/assets/a6055f12-44a6-4f8e-b773-e4ec66f8d8b6" />


---

#Passou**CT_70: E-mail do Coordenador com Formato Inválido na Tela**

**Dado:** que o usuário está no formulário de cadastro de projeto

**Quando:** o usuário preenche o campo "E-mail do Coordenador" com `"email_invalido"`

**E:** clica em "Cadastrar"

**Então:** o sistema exibe mensagem de validação indicando formato de e-mail inválido e não prossegue com o cadastro

<img width="567" height="131" alt="image" src="https://github.com/user-attachments/assets/9a239c3a-ca54-4f9c-ada5-355cb4255cea" />

---

