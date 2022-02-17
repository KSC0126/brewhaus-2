<template>
  <nav aria-label="Page navigation">
    <ul class="inline-flex space-x-2">
      <li>
        <button
          class="flex items-center justify-center w-10 h-10 text-indigo-600 transition-colors duration-150 rounded-full focus:shadow-outline hover:bg-indigo-100"
          @click="arrowButtonSelection('previous')"
        >
          <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20">
            <path
              d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
              clip-rule="evenodd"
              fill-rule="evenodd"
            ></path>
          </svg>
        </button>
      </li>
      <li v-for="page in pageNumbers" :key="page">
        <button
          class="w-10 h-10 text-indigo-600 transition-colors duration-150 rounded-full focus:shadow-outline hover:bg-indigo-100"
          @click="pageSelection(page)"
        >
          {{ page }}
        </button>
      </li>
      <li>
        <button
          class="flex items-center justify-center w-10 h-10 text-indigo-600 transition-colors duration-150 bg-white rounded-full focus:shadow-outline hover:bg-indigo-100"
          @click="arrowButtonSelection('next')"
        >
          <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20">
            <path
              d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
              fill-rule="evenodd"
            ></path>
          </svg>
        </button>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {},
  data() {
    return {
      pageNumbers: [1, 2],
      currentPageNumber: 1,
    };
  },
  methods: {
    pageSelection(pageNumber) {
      this.currentPageNumber = pageNumber;
      pageNumber;
      const isNewPageNumberRequired =
        pageNumber >= this.pageNumbers.length && pageNumber < 5;
      if (isNewPageNumberRequired) {
        this.pageNumbers.push(this.pageNumbers.length + 1);
      }
      if (pageNumber < 6) {
        this.$emit("updatePageNumber", this.currentPageNumber);
      }
    },
    arrowButtonSelection(direction) {
      if (
        direction.toLowerCase() === "previous" &&
        this.currentPageNumber !== 1
      ) {
        this.currentPageNumber = this.currentPageNumber - 1;
      }
      if (direction.toLowerCase() === "next" && this.currentPageNumber < 5) {
        this.currentPageNumber = this.currentPageNumber + 1;
      }
      this.pageSelection(this.currentPageNumber);
    },
  },
};
</script>
