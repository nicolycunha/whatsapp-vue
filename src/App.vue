<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-3 lista-conversas">
          <div class="barra-superior"></div>
          <div
            class="item"
            v-for="(conversa, index) in conversas"
            :key="index"
            @click="indiceAtivo = index"
          >
            <div class="title is-6">
              {{ conversa.usuario }}
            </div>
            <div class="subtitle is-6">Última mensagem...</div>
          </div>
        </div>
        <div class="column conversa-ativa">
          <div class="barra-superior">
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

.columns {
  min-height: 800px;
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
}

.barra-superior {
  margin: 0;
  height: 50px;
  background: #f0f2f5;
  border-right: 1px solid #e1e1e1;
  border-bottom: 1px solid rgb(200, 200, 200);
}

.barra-superior span {
  line-height: 50px;
  margin-left: 25px;
  font-weight: 500;
}

.item {
  border-bottom: 1px solid #f2f2f2;
  padding: 15px 30px;
  margin-bottom: 0 !important;
}

.item:hover {
  background: #f5f5f5;
  cursor: pointer;
}

.subtitle {
  color: #808080;
}

.lista-mensagens {
  height: 85%;
  display: flex;
  justify-content: flex-end;
  flex-direction: column;
}

.barra-inferior {
  bottom: 0;
  width: 77%;
  padding: 10px;
  position: absolute;
  background: #f0f0f0;
}
</style>
