<script>
export default {
  name: "searchbar",
  data: () => ({ term: "" }),
  props: {
    placeholder: String,
    buttonLabel: String,
  },
  emits: ["term-change", "form-submit"],
};
</script>

<template>
  <form @submit.prevent="$emit('form-submit')" class="searchbar">
    <input
      type="text"
      v-model.trim="term"
      @keyup="$emit('term-change', term)"
      :placeholder="placeholder || 'Cerca'"
    />
    <button class="text-light">{{ buttonLabel || "Cerca" }}</button>
  </form>
</template>

<style scoped lang="scss">
button {
  background-color: red;
}
</style>
