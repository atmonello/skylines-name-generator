<template>
  <section id="nameGenerator">
    <panel>
      <!-- <fieldset id="debug" slot="content">
        <legend>Debug - APAGAR</legend>
        <p>Nome composto? {{ controls.composto }}</p>
        <p>Tipo de nome? {{ controls.tipo }}</p>
        <p>Prefixos? {{ controls.prefixos }}</p>
        <p>Sufixos? {{ controls.sufixos }}</p>
      </fieldset> -->
      <div id="generate" slot="content">
        <h2>Nome gerado</h2>
        <p v-show="controls.toggle">{{ content.generated.trim() }}</p>
      </div>
      <ul slot="content" class="list-group">
        <li v-for="(name, index) in content.previousNames" :key="index" class="list-group-item">{{ name }}</li>
      </ul>
    </panel>
  </section>
</template>

<style lang="less">
@import "../assets/main.less";
#nameGenerator {
  #generate {
    text-align: center;
  }
}
</style>


<script>
/* eslint-disable no-undef */
/* eslint-disable default-case */
/* eslint-disable no-unused-vars */
/* eslint-disable eqeqeq */

import panel from "../components/panel.vue";

export default {
  components: {
    panel,
  },
  data() {
    return {
      controls: {
        toggle: false,
        composto: 1,
        tipo: 1,
      },
      content: {
        generated: " ",
        previousNames: [],
        nomes: {
          comumSimples: ["Centro", "República", "Luz", "Santana", "Pinheiros", "Freguesia", "Lapa"],
          comumComposto: ["Santana", "Ipiranga", "Engenho", "Itaim"],
          indigena: ["Anhangabaú", "Anhanguera", "Piratininga", "Guaporé", "Anhembi", "Ibirapuera", "Iguatemi"],
          masculino: ["João", "José", "Paulo", "Carlos", "André", "Lucas", "Mateus"],
          feminino: ["Maria", "Luzia", "Bárbara", "Rita"],
        },
        prefixos: {
          geo: ["Vila Velha", "Vila Rica", "Vila Nova", "Vila", "Rio", "Rio Grande", "Riacho", "Córrego", "Vale", "Vargem", "Várzea", "Campo", "Cachoeira", "Planalto", "Lagoa "],
          masculino: ["São", "Santo"],
          feminino: ["Santa"],
        },
        sufixos: {
          comum: ["do Sul", "do Norte", "do Oeste", "do Leste", ""],
        },
      },
    };
  },
  created() {
    const self = this;

    self.$nuxt.$on("generate", (data) => {
      // console.log("Generate name");
      self.controls.toggle = data.toggle;
      self.controls.composto = data.composto;
      self.controls.tipo = data.tipo;
      self.controls.prefixos = data.prefixos;
      self.controls.sufixos = data.sufixos;

      if (self.controls.composto == 1) {
        if (self.controls.tipo == 2) {
          self.content.generated = self.content.nomes.indigena[Math.floor(Math.random() * self.content.nomes.indigena.length)];
          // console.log(self.content.generated);
        } else if (self.controls.tipo == 3) {
          self.content.generated = self.content.nomes.masculino[Math.floor(Math.random() * self.content.nomes.masculino.length)];
        } else if (self.controls.tipo == 4) {
          self.content.generated = self.content.nomes.feminino[Math.floor(Math.random() * self.content.nomes.feminino.length)];
        } else if (self.controls.tipo == 5) {
          self.content.generated = self.content.nomes.comumSimples[Math.floor(Math.random() * self.content.nomes.comumSimples.length)];
        }
      } else if (self.controls.composto == 2) {
        if (self.controls.tipo == 1) {
          self.content.generated = `${self.content.prefixos.geo[Math.floor(Math.random() * self.content.prefixos.geo.length)]} ${self.content.sufixos.comum[Math.floor(Math.random() * self.content.sufixos.comum.length)]}`;
        } else if (self.controls.tipo == 3) {
          if (self.controls.sufixos == false) {
            self.content.generated = `${self.content.prefixos.masculino[Math.floor(Math.random() * self.content.prefixos.masculino.length)]} ${self.content.nomes.masculino[Math.floor(Math.random() * self.content.nomes.masculino.length)]}`;
          } else {
            self.content.generated = `${self.content.prefixos.masculino[Math.floor(Math.random() * self.content.prefixos.masculino.length)]} ${self.content.nomes.masculino[Math.floor(Math.random() * self.content.nomes.masculino.length)]} ${self.content.sufixos.comum[Math.floor(Math.random() * self.content.sufixos.comum.length)]}`;
          }
        } else if (self.controls.tipo == 4) {
          if (self.controls.sufixos == false) {
            self.content.generated = `${self.content.prefixos.feminino[Math.floor(Math.random() * self.content.prefixos.feminino.length)]} ${self.content.nomes.feminino[Math.floor(Math.random() * self.content.nomes.feminino.length)]}`;
          } else {
            self.content.generated = `${self.content.prefixos.feminino[Math.floor(Math.random() * self.content.prefixos.feminino.length)]} ${self.content.nomes.feminino[Math.floor(Math.random() * self.content.nomes.feminino.length)]} ${self.content.sufixos.comum[Math.floor(Math.random() * self.content.sufixos.comum.length)]}`;
          }
        } else if (self.controls.tipo == 5) {
          if (self.controls.prefixos == false) {
            self.content.generated = `${self.content.nomes.comumComposto[Math.floor(Math.random() * self.content.nomes.comumComposto.length)]} ${self.content.sufixos.comum[Math.floor(Math.random() * self.content.sufixos.comum.length)]}`;
          } else if (self.controls.sufixos == false) {
            self.content.generated = `${self.content.prefixos.geo[Math.floor(Math.random() * self.content.prefixos.geo.length)]} ${self.content.nomes.comumComposto[Math.floor(Math.random() * self.content.nomes.comumComposto.length)]}`;
          } else {
            self.content.generated = `${self.content.prefixos.geo[Math.floor(Math.random() * self.content.prefixos.geo.length)]} ${self.content.nomes.comumComposto[Math.floor(Math.random() * self.content.nomes.comumComposto.length)]} ${self.content.sufixos.comum[Math.floor(Math.random() * self.content.sufixos.comum.length)]}`;
          }
        }
      }

      self.content.previousNames.unshift(self.content.generated.trim());
    });
  },
};
</script>
