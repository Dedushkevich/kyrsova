<template>
  <li class="form-categories-item">
    <label
      class="form-categories-label"
      :class="
        checkedCategories.includes(categorie.id)
          ? 'form-filter-checked'
          : 'form-filter-uncheked'
      "
    >
      {{ categorie.type }}

      <input
        type="checkbox"
        :value="categorie.id"
        @change="handleBtnChangeClick"
        :name="categorie.type"
        class="form-filter-input"
    /></label>

    <button
      type="button"
      @click="handleBtnDeleteClick(categorie)"
      class="form-categories-delete-categorie"
    >
      delete
    </button>
  </li>
</template>

<script>
export default {
  props: {
    categorie: {
      type: Object,
      required: true,
    },
  },

  computed: {
    checkedCategories() {
      return this.$store.getters.checkedCategories;
    },
  },

  methods: {
    handleBtnChangeClick(e) {
      if (e.target.checked) {
        this.$store.dispatch("checkCategorie", Number(e.target.value));
      } else this.$store.dispatch("unCheckCategorie", Number(e.target.value));
    },

    handleBtnDeleteClick(data) {
      this.$store.dispatch("deleteCategorie", data);
    },
  },
};
</script>
