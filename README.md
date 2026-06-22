# TCCGuilhermeSantosGomes

## Reprodutibilidade e Disponibilização dos Artefatos

Com o objetivo de viabilizar a replicação deste estudo e a continuidade de
pesquisas futuras, todos os artefatos produzidos ao longo da pesquisa foram
organizados e descritos a seguir.

### Repositórios de código-fonte

O sistema FunADM é composto por dois repositórios mantidos pela SIFSoft no
GitHub:

- **Back-end**: <https://github.com/Projetos-SIFSoft/sifsoft-funAdm-server>  
  Contém a API REST desenvolvida em Node.js com TypeScript, Express e
  Prisma ORM, incluindo as *migrations* do banco de dados e a configuração
  do Swagger.

- **Front-end**: <https://github.com/Projetos-SIFSoft/sifsoft-funAdm-web>  
  Contém a interface web construída com React, Vite e TypeScript,
  responsável por consumir a API e gerar o tráfego inspecionado durante a
  pesquisa.

Ambos os repositórios podem ser clonados e executados localmente seguindo as
instruções dos respectivos `README.md`. O back-end depende de um banco de
dados PostgreSQL, cujo esquema é gerenciado pelo Prisma; o front-end requer
a definição das variáveis de ambiente `BASE_URL`, `KEY` e `SECRET_KEY` para
estabelecer a comunicação com a API e a criptografia da sessão.

### Coleção do Insomnia

As requisições utilizadas durante as sessões de teste exploratório foram
organizadas em uma coleção do Insomnia, exportada no formato JSON e
disponibilizada junto com este trabalho (arquivo `Insomnia-TCC`).
A coleção está estruturada por módulo (Autenticação, Contas Bancárias,
Projetos, Movimentações, Investimentos) e inclui as variáveis de ambiente
`base_url` e `token`, de modo que o pesquisador possa reproduzir
imediatamente as chamadas à API. Para utilizar a coleção, basta importá-la
no Insomnia, substituir o valor da variável `base_url` pelo endereço da API
alvo e obter um token JWT válido por meio do *endpoint* de login.

### Documentação da API e registros dos casos de teste

A documentação Swagger da API está disponível na rota `/docs` do back-end.
Os 123 casos de teste, no formato Gherkin, foram consolidados em arquivo PDF
(`CTs-FunADM.pdf`) e anexados a este trabalho. Os registros individuais de
execução, com os status e as observações de cada cenário, foram mantidos no
aplicativo Obsidian.

### Acesso ao sistema e obtenção do token JWT

Os testes foram realizados em dois ambientes fornecidos pela SIFSoft:

- **Ambiente de teste**:
  - Front-end: <https://frontend-teste.up.railway.app>
  - Back-end: <https://cash-management-teste.up.railway.app>

- **Ambiente de produção**:
  - Front-end: <https://funadm.fadetec.org.br/>
  - Back-end: <https://sifsoft-funadm-server-production-a6f3.up.railway.app>

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

### Procedimento de replicação

Para replicar a bateria de testes aqui descrita, um pesquisador deve:

1. Iniciar o front-end e realizar o login para capturar, por meio do
   Chrome DevTools, o token JWT utilizado nas requisições autenticadas.
2. Importar a coleção do Insomnia (arquivo `Insomnia-TCC`),
   ajustar a variável `base_url` e o token JWT.
3. Executar os casos de teste documentados no PDF `CTs-FunADM.pdf`,
   registrando os resultados em planilha ou aplicativo similar.

Esse conjunto de artefatos assegura a transparência e a reprodutibilidade
da pesquisa, permitindo que tanto a equipe da SIFSoft quanto outros
pesquisadores possam dar continuidade à validação da API do FunADM ou
adaptar a metodologia para sistemas semelhantes.
