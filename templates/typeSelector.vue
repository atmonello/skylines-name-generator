<template>
  <section id="typeSelector">
    <panel>
      <h2 slot="content">Definições</h2>
      <fieldset slot="content">
        <legend>Nome simples ou composto</legend>
        <div class="form-group">
          <div class="custom-control custom-radio">
            <input id="simples" v-model="controls.composto" type="radio" name="nomeComposto" class="custom-control-input" value="1">
            <label class="custom-control-label" for="simples">Nome Simples</label>
          </div>
          <div class="custom-control custom-radio">
            <input id="composto" v-model="controls.composto" type="radio" name="nomeComposto" class="custom-control-input" value="2">
            <label class="custom-control-label" for="composto">Nome composto</label>
          </div>
        </div>
      </fieldset>

      <fieldset slot="content">
        <legend>Prefixos e Sufixos</legend>
        <div class="form-group">
          <div class="custom-control custom-checkbox">
            <input id="prefixos" v-model="controls.prefixos" :disabled="controls.composto == 1 || !controls.sufixos || controls.tipo == 1 || controls.tipo == 3 || controls.tipo == 4" type="checkbox" name="prefixos" class="custom-control-input" value="pre">
            <label class="custom-control-label" for="prefixos">Prefixos</label>
          </div>
          <div class="custom-control custom-checkbox">
            <input id="sufixos" v-model="controls.sufixos" :disabled="controls.composto == 1 || !controls.prefixos || controls.tipo == 1" type="checkbox" name="prefixos" class="custom-control-input" value="suf">
            <label class="custom-control-label" for="sufixos">Sufixos</label>
          </div>
        </div>
      </fieldset>

      <fieldset slot="content">
        <legend>Tipo de nome</legend>
        <div class="form-group">
          <div class="custom-control custom-radio">
            <input id="geografico" v-model="controls.tipo" :disabled="controls.composto == 1" type="radio" name="nomeTipo" class="custom-control-input" value="1">
            <label class="custom-control-label" for="geografico">Geográfico</label>
          </div>
          <div class="custom-control custom-radio">
            <input id="indigena" v-model="controls.tipo" :disabled="controls.composto == 2" type="radio" name="nomeTipo" class="custom-control-input" value="2">
            <label class="custom-control-label" for="indigena">Indígena</label>
          </div>
          <div class="custom-control custom-radio">
            <input id="masculino" v-model="controls.tipo" :disabled="controls.composto == 1" type="radio" name="nomeTipo" class="custom-control-input" value="3">
            <label class="custom-control-label" for="masculino">Nome masculino</label>
          </div>
          <div class="custom-control custom-radio">
            <input id="feminino" v-model="controls.tipo" :disabled="controls.composto == 1" type="radio" name="nomeTipo" class="custom-control-input" value="4">
            <label class="custom-control-label" for="feminino">Nome feminino</label>
          </div>
          <div class="custom-control custom-radio">
            <input id="generico" v-model="controls.tipo" type="radio" name="nomeTipo" class="custom-control-input" value="5">
            <label class="custom-control-label" for="generico">Genérico</label>
          </div>
        </div>
      </fieldset>

      <div id="generateButton" slot="content">
        <button :disabled="controls.composto == 1 && controls.tipo == 1 || controls.composto == 2 && controls.tipo == 2 || controls.tipo == 0 || controls.composto == 0" type="button" class="btn btn-primary btn-block" @click="enviarParametros">Gerar nome</button>
      </div>
    </panel>
  </section>
</template>

<script>
import panel from "../components/panel.vue";

export default {
  components: {
    panel,
  },
  data() {
    return {
      controls: {
        composto: 0,
        sufixos: true,
        prefixos: true,
        tipo: 0,
      },
    };
  },
  methods: {
    // envia parâmetros para geração do nome
    enviarParametros() {
      const self = this;

      self.$nuxt.$emit("generate", {
        toggle: true,
        composto: self.controls.composto,
        tipo: self.controls.tipo,
        prefixos: self.controls.prefixos,
        sufixos: self.controls.sufixos,
      });
    },
  },
};
</script>
