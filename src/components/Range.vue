<template>
    <div>
        <label>{{customLabel}}</label>
        <input
        type="range"
        :value="value"
        v-bind="$attrs"
        :class="inputClasses"
        @input="atualizar">
    </div>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    value: [Number, String],
    label: String,
    inputClasses: [String, Object, Array],
  },
  data() {
    return {
      valorAtual: this.value || this.$attrs.min,
    };
  },
  computed: {
    customLabel() {
      return `${this.label} (R$ ${this.valorAtual})`;
    },
  },
  methods: {
    atualizar(event) {
      const valor = event.target.value;
      this.$emit('input', valor);
      this.valorAtual = valor;
    },
  },
  created() {
    console.log('Attrs: ', this.$attrs);
  },
};
</script>
