<template>
  <section>
    <UsuarioForm>
      <button class="btn" @click.prevent="atualizarUsuario">Atualizar Usuário</button>
    </UsuarioForm>
    <ErroNotificacao :erros="erros"/>
  </section>
</template>

<script>
import ErroNotificacao from "@/components/ErroNotificacao.vue";
import UsuarioForm from "@/components/UsuarioForm.vue";
import { api } from "@/services.js";

export default {
  name: "UsuarioEditar",
  components: {
    UsuarioForm,
    ErroNotificacao
},
  data() {
    return {
      erros: []
    }
  },
  methods: {
    atualizarUsuario() {
      this.erros = [];
      api.put("/usuario", this.$store.state.usuario)
        .then(() => {
          this.$store.dispatch("getUsuario");
          this.$store.push({ name: "usuario" });
        })
        .catch(error => {
          this.erros.pus(error.response.data.message);
        });
    },
  },
  created() {
    document.title = "Usuario | Editar";
  }
};
</script>

<style>
</style>