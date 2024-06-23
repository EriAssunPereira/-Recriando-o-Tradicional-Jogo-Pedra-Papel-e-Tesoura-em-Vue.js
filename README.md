# Recriando-o-Tradicional-Jogo-Pedra-Papel-e-Tesoura-em-Vue.js

Para criar o jogo Pedra, Papel e Tesoura em Vue.js de maneira organizada e utilizando boas práticas de desenvolvimento, vamos estruturar o projeto em módulos distintos. Vamos utilizar Vue Router para a navegação entre páginas e Vuex para gerenciar o estado da aplicação. Além disso, vamos armazenar dados no `localStorage` para persistência local e garantir que a aplicação seja responsiva utilizando SASS, Flexbox e CSS Grid para o layout.

### Passos para criar o projeto

#### 1. Configuração inicial do projeto

Certifique-se de ter o Vue CLI instalado globalmente:

```bash
npm install -g @vue/cli
```

Crie um novo projeto Vue com Vue CLI:

```bash
vue create pedra-papel-tesoura
```

Selecione as opções padrão ou escolha as que preferir (por exemplo, com TypeScript ou JavaScript puro).

#### 2. Instalação de dependências adicionais

Vamos instalar as dependências necessárias:

```bash
cd pedra-papel-tesoura

# Instalar Vue Router
npm install vue-router

# Instalar Vuex
npm install vuex
```

#### 3. Estrutura do projeto

Organizaremos o projeto da seguinte forma:

```
pedra-papel-tesoura/
├── src/
│   ├── assets/
│   │   └── styles/
│   │       ├── main.scss    # Arquivo principal de estilos SASS
│   ├── components/
│   │   ├── Game.vue         # Componente principal do jogo
│   │   ├── Home.vue         # Página inicial
│   │   ├── Result.vue       # Componente para exibir resultado do jogo
│   │   └── ...
│   ├── router/
│   │   └── index.js         # Configuração do Vue Router
│   ├── store/
│   │   ├── modules/
│   │   │   └── game.js      # Módulo Vuex para gerenciamento do jogo
│   │   └── index.js         # Configuração do Vuex
│   └── App.vue              # Componente raiz da aplicação
└── ...
```

#### 4. Implementação dos componentes e funcionalidades

Vamos detalhar os principais pontos da implementação:

##### `router/index.js`

```javascript
import Vue from 'vue';
import VueRouter from 'vue-router';
import Home from '../components/Home.vue';
import Game from '../components/Game.vue';

Vue.use(VueRouter);

const routes = [
  { path: '/', component: Home },
  { path: '/game', component: Game },
];

const router = new VueRouter({
  routes,
});

export default router;
```

##### `store/index.js`

```javascript
import Vue from 'vue';
import Vuex from 'vuex';
import game from './modules/game';

Vue.use(Vuex);

export default new Vuex.Store({
  modules: {
    game,
  },
});
```

##### `store/modules/game.js`

```javascript
const state = {
  choices: ['rock', 'paper', 'scissors'],
  playerChoice: null,
  computerChoice: null,
  result: null,
};

const mutations = {
  setPlayerChoice(state, choice) {
    state.playerChoice = choice;
  },
  setComputerChoice(state, choice) {
    state.computerChoice = choice;
  },
  setResult(state, result) {
    state.result = result;
  },
};

const actions = {
  playRound({ commit, state }, playerChoice) {
    // Lógica para calcular escolha do computador e resultado do jogo
    const computerChoice = state.choices[Math.floor(Math.random() * 3)];
    commit('setPlayerChoice', playerChoice);
    commit('setComputerChoice', computerChoice);

    // Lógica para determinar o resultado (você pode implementar aqui)
    let result = ''; // Implemente a lógica para definir o resultado

    commit('setResult', result);
  },
};

export default {
  state,
  mutations,
  actions,
};
```

##### Exemplo básico dos componentes `Game.vue` e `Home.vue`

`Game.vue`:

```vue
<template>
  <div>
    <h1>Game Page</h1>
    <!-- Componente para mostrar resultado do jogo -->
    <Result v-if="result !== null" :result="result" />
    <button @click="play('rock')">Rock</button>
    <button @click="play('paper')">Paper</button>
    <button @click="play('scissors')">Scissors</button>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex';
import Result from './Result.vue';

export default {
  components: {
    Result,
  },
  methods: {
    ...mapActions(['playRound']),
    play(choice) {
      this.playRound(choice);
    },
  },
  computed: {
    ...mapState({
      result: (state) => state.game.result,
    }),
  },
};
</script>
```

`Home.vue`:

```vue
<template>
  <div>
    <h1>Welcome to Rock Paper Scissors!</h1>
    <router-link to="/game">Start Game</router-link>
  </div>
</template>

<script>
export default {};
</script>
```

#### 5. Estilos responsivos com SASS

Utilize o arquivo `src/assets/styles/main.scss` para aplicar estilos utilizando SASS, Flexbox e CSS Grid conforme necessário para tornar a aplicação responsiva.

#### 6. Integração com `localStorage`

Para integrar com `localStorage`, você pode adicionar lógica no Vuex (`store/modules/game.js`) para salvar e carregar dados conforme necessário.

#### 7. Conclusão

Este projeto utiliza Vue.js com Vue Router e Vuex para criar um jogo simples de Pedra, Papel e Tesoura, aplicando conceitos de componentização, gerenciamento de estado centralizado, estilos responsivos e integração com `localStorage`. Certifique-se de adaptar e expandir conforme necessário para atender aos requisitos específicos do seu projeto.
