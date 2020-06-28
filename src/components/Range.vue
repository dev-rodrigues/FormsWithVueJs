<template>
    <div>
        <label>{{customLabel}}</label>
        <input
        type="range"
        :value="valor"
        v-bind="$attrs"
        :class="inputClasses"
        @input="atualizar">
    </div>
</template>

<script>
export default {
  inheritAttrs: false,
  model: {
    prop: 'valor',
  },
  props: {
    valor: [Number, String],
    label: String,
    inputClasses: [String, Object, Array],
  },
  data() {
    return {
      valorAtual: this.valor || this.$attrs.min,
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
