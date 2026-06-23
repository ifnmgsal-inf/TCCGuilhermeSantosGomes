## Disponibilização da pesquisa

Com o objetivo de viabilizar a replicação deste estudo e a continuidade de
pesquisas futuras, todos os artefatos produzidos ao longo da pesquisa foram
organizados e descritos a seguir.

---

## Arquitetura do sistema

O sistema FunADM é composto por dois repositórios mantidos pela SIFSoft no
GitHub:

- **Back-end**
  Contém a API REST desenvolvida em Node.js com TypeScript, Express e
  Prisma ORM, incluindo as *migrations* do banco de dados e a configuração
  do Swagger.

- **Front-end**
  Contém a interface web construída com React, Vite e TypeScript,
  responsável por consumir a API e gerar o tráfego inspecionado durante a
  pesquisa.

---

## Insomnia e Obsidian

As requisições utilizadas durante as sessões de teste exploratório foram
organizadas em uma coleção do Insomnia, e anotada em formato .md no Obsidian, exportada no formato PDF e disponibilizada junto com este trabalho (arquivo `CTs-TCC.pdf`).
O arquivo está estruturada por módulo (Autenticação, Contas Bancárias,
Projetos, Movimentações, Investimentos). Para utilizar basta seguir os passos da seção ***Procedimento de replicação***.

- **Insomnia**: https://insomnia.rest/download
- **Obsidian**: https://obsidian.md/pt-BR/

---

## Documentação da API e registros dos casos de teste

A documentação Swagger da API está disponível na rota `/docs` do back-end.
Os 123 casos de teste, no formato Gherkin (Dado, Quando, Então), foram consolidados em arquivo PDF (`CTs-TCC.pdf`) e anexados a este trabalho. Os registros individuais de
execução, com os status e as observações de cada cenário, foram mantidos no
aplicativo Obsidian.

---

## Acesso ao sistema e obtenção do token JWT

Os testes foram realizados em dois ambientes fornecidos pela SIFSoft:

- **Ambiente de teste**;
- **Ambiente de produção**.

Em ambos os ambientes, o back-end exige autenticação JWT, retornando erro
`401 Unauthorized` para requisições diretas. Por isso, o acesso inicial foi
feito pelo front-end, utilizando credenciais de um usuário previamente
cadastrado. **Para replicar o estudo, é indispensável dispor de um usuário
válido no sistema** — seja um existente na base, seja um novo usuário
criado por meio do Prisma Studio ou de um *seed* que insira um registro na
tabela `users` com as permissões adequadas.

Uma vez autenticado no front-end, o token JWT foi capturado por meio da aba
**Network** do Chrome DevTools: ao inspecionar qualquer requisição que o
front-end enviava ao back-end, copiou-se o cabeçalho
`Authorization: Bearer <token>`. Esse token foi então inserido na variável
de ambiente `token` da coleção do Insomnia, permitindo que as requisições
fossem reproduzidas diretamente contra a API, sem depender da interface web.
Todo o fluxo — login no front-end, captura do token e importação no Insomnia
— deve ser repetido pelo pesquisador que desejar reproduzir a bateria de
testes, pois o token expira periodicamente e não é armazenado nos artefatos
compartilhados.

---

## Como replicar a pesquisa

Para replicar a bateria de testes aqui descrita, um pesquisador deve:

1. Realize a autenticação com Login e Senha pelo front-end para capturar, por meio do Chrome DevTools pela aba 'Network', o token JWT utilizado nas requisições autenticadas com o back-end.
2. Abra o aplicativo Insomnia, crie uma 'Collection' coloque a URL do back-end, acione a aba 'Headers' e clique no botão '+Add' e no campo 'Accept' coloque o nome 'Authorization' e no campo '*/*' coloque o token JWT que copiou do DevTools.
3. Acesse o swagger da aplicação. Após acessar o sistema coloque no fim da URL /docs e veja quais rotas de APIS o sistema possui.
4. Execute os casos de teste documentados no PDF `CTs-TCC.pdf`, no aplicativo do Insomnia já configurado, após isso registre os resultados no aplicativo Obsidian ou similar.

Esse conjunto de artefatos assegura a transparência e a reprodutibilidade
da pesquisa, permitindo que tanto a equipe da SIFSoft quanto outros
pesquisadores possam dar continuidade à validação da API do FunADM ou
adaptar a metodologia para sistemas semelhantes.
