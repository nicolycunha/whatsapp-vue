<template>
  <div class="mensagem" :class="{ verde: verde }">
    {{ conteudo }}
    <span>{{ horario }}</span>
  </div>
</template>

<script>
export default {
  name: "MensagemComponent",
  props: ["conteudo", "horario", "verde"],
};
</script>

<style scoped>
.mensagem {
  font-size: 14px;
  box-shadow: rgba(0, 0, 0, 0.13) 0px 1px 0.5px, 0px;
  background: #ffffff;
  margin: 5px 100px;
  padding: 5px 10px;
  border-radius: 8px;
  width: fit-content;
}

.mensagem span {
  margin-left: 25px;
  font-size: 11px;
  color: #808080;
}

.verde {
  background: #dcf8c6;
  align-self: flex-end;
}
</style>
