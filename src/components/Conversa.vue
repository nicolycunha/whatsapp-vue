<template>
  <div class="item">
    <img class="usuario" src="../assets/user.png" alt="conversa.usuario" />
    <div class="informacoes">
      <div class="title is-6">
        {{ conversa.usuario }}
      </div>
      <div class="subtitle is-6">Última mensagem...</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ConversasComponent",
  props: ["conversa"],
};
</script>

<style scoped>
.item {
  border-bottom: 1px solid #f2f2f2;
  padding: 15px;
  margin-bottom: 0 !important;
  display: flex;
  gap: 15px;
}

.item:hover {
  background: #f5f5f5;
  cursor: pointer;
}

.usuario {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}

.subtitle {
  color: #808080;
}
</style>