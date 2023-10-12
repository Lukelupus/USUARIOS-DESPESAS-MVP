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

        <q-toolbar-title> Teste Técnico - Onfly </q-toolbar-title>

        <div>
          Técnologias utilizadas: Frontend - PHP v8.2.9 Laravel | Frontend:
          Vue.js | Quasar v{{ $q.version }}
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Essential Links </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
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
