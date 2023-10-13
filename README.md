# Quasar App (despesas-mvp-front)

'Onfly technical test'

# Este é um MVP de Despesas - Teste Técnico para Onfly

Este é o frontend de um teste técnico FullStack. Os dois passos do teste, assim como requisitados são:

[Parte1] (https://github.com/Lukelupus/DESPESAS-MVP): Desenvolver uma API REST com Laravel, implementando:

        - Autenticação de usuário.

        - CRUD de despesas.

        - Restrição de acesso.

        - CRUD deve estar protegido pela autenticação.



    Na entidade despesas, deverá conter:


           - Id

           - Descrição (descrição da despesa)

           - Data (data de quando ocorreu a despesa)

           - Usuário (usuário dono da despesa, um relacionamento com a tabela de Usuários)

           - Valor (valor em reais da despesa)

    Dada a natureza deste repositório, a parte 2 representa o front da aplicação. Para testar o aplicativo completo, clone também o backend.

[Parte2]

Faça em Vue.js uma tela de gestão de usuários (CRUD) utilizando sua API. Para facilitar o desenvolvimento, deve-se usar UI framework baseado em Vue.js: Quasar

## Install the dependencies

```bash
yarn
# or
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)

```bash
quasar dev
```

### Lint the files

```bash
yarn lint
# or
npm run lint
```

### Format the files

```bash
yarn format
# or
npm run format
```

### Build the app for production

```bash
quasar build
```

### Customize the configuration

See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).
