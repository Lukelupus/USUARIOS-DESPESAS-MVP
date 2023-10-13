<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title style="margin-left: 2rem">
          Teste Técnico - Onfly
        </q-toolbar-title>

        <div>
          Técnologias utilizadas: Frontend - PHP v8.2.9 Laravel | Frontend:
          Vue.js | Quasar v{{ $q.version }}
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Links de Contato </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <div class="q-pa-md" style="margin: 2em; align-items: center">
        <h2 style="margin-left: 2rem; display: flex; justify-content: center">
          Desafio FullStack
        </h2>
        <p
          style="
            font-size: 1.5em;
            margin: 2rem;
            display: flex;
            justify-content: center;
          "
        >
          Esta é a representação da página Vue.js da Parte 2 do desafio.
        </p>
        <p
          style="
            font-size: 1.5em;
            margin: 3rem;
            display: flex;
            justify-content: center;
            width: 70%;
            position: relative;
            left: 18%;
          "
        >
          "Faça em Vue.js uma tela de gestão de usuários (CRUD) utilizando sua
          API. Para facilitar o desenvolvimento, deve-se usar UI framework
          baseado em Vue.js: Quasar"
        </p>

        <!-- Botões para navegar -->
        <div
          style="
            display: flex;
            flex-direction: row;
            justify-content: space-evenly;
          "
        >
          <q-btn @click="navigateToDespesas" label="Despesas" color="primary" />
          <q-btn
            @click="navigateToUsuarios"
            label="Parte 2: Usuários"
            color="primary"
          />
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Oi, eu sou o Lucas!",
    caption: "Desenvolvedor FullStack",
    icon: "record_voice_over",
    link: "https://www.linkedin.com/in/lucas-moreira-botelho-18298715b/",
  },
  {
    title: "Home",
    caption: "Ir para a página incial",
    icon: "home",
    link: "/",
  },
  {
    title: "Github",
    caption: "github.com/Lukelupus",
    icon: "code",
    link: "https://github.com/Lukelupus",
  },
  {
    title: "Obrigado pela Avaliação!",
    caption: "Espero que goste!",
    icon: "favorite",
    link: "",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },
  methods: {
    navigateToDespesas() {
      this.$router.push("/despesas");
    },
    navigateToUsuarios() {
      this.$router.push("/usuarios");
    },
  },
  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
