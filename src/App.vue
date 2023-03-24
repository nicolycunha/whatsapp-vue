<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-3 lista-conversas">
          <div class="barra-superior">
            <img
              class="usuario"
              src="./assets/me.png"
              alt="Eu"
            />
          </div>
          <Conversa
            v-for="(conversa, index) in conversas"
            :key="index"
            :conversa="conversa"
            @click="indiceAtivo = index"
          />
        </div>
        <div class="column conversa-ativa">
          <div class="barra-superior">
            <img
              class="usuario"
              src="./assets/user.png"
              alt="conversa.usuario"
            />
            <span>{{ conversas[indiceAtivo].usuario }}</span>
          </div>
          <div class="lista-mensagens">
            <Mensagem
              v-for="(mensagem, index) in conversas[indiceAtivo].mensagens"
              :key="index"
              :conteudo="mensagem.conteudo"
              :horario="mensagem.horario"
              :verde="mensagem.verde"
            />
          </div>
          <div class="barra-inferior">
            <input
              type="text"
              class="input"
              placeholder="Insira sua mensagem"
              v-model="conteudoNovaMensagem"
              @keyup.enter="enviarMensagem"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import conversasIniciais from "./dados";
import Mensagem from "./components/Mensagem";
import Conversa from "./components/Conversa";

export default {
  name: "App",
  data() {
    return {
      conversas: conversasIniciais,
      indiceAtivo: 0,
      conteudoNovaMensagem: "",
    };
  },
  components: {
    Mensagem,
    Conversa,
  },
  methods: {
    enviarMensagem() {
      let horarioAtual = new Date().getHours() + ":" + new Date().getMinutes();

      let novaMensagem = {
        horario: horarioAtual,
        conteudo: this.conteudoNovaMensagem,
        verde: true,
      };

      this.conversas[this.indiceAtivo].mensagens.push(novaMensagem);

      this.conteudoNovaMensagem = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container {
  max-width: 90vw !important;
}

.columns {
  height: 90vh;
  box-shadow: 0 3rem 3rem -1rem rgba(10, 10, 10, 0.2);
}

.column {
  padding: 0;
}

.lista-conversas {
  background: #ffffff;
}

.conversa-ativa {
  background: #e5ddd5;
  display: flex;
  flex-direction: column;
}

.barra-superior {
  margin: 0;
  height: 50px;
  background: #f0f2f5;
  border-right: 1px solid #e1e1e1;
  border-bottom: 1px solid rgb(200, 200, 200);
  display: flex;
  align-items: center;
  padding: 1rem;
  gap: 15px;
}

.barra-superior span {
  line-height: 50px;
  font-weight: 500;
}

.usuario {
  width: 35px;
  height: 35px;
  border-radius: 50%;
}

.lista-mensagens {
  height: 100%;
  display: flex;
  justify-content: flex-end;
  flex-direction: column;
  padding: 1rem 0;
}

.barra-inferior {
  bottom: 0;
  padding: 10px;
  background: #f0f2f5;
}
</style>
