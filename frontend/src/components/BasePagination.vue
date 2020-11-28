<template>
  <ul class="pagination" :class="[size && `pagination-${size}`, align && `justify-content-${align}`]">
    <li class="page-item prev-page" :class="{disabled: currentPage === 1}">
      <a class="page-link" aria-label="Previous" @click="prevPage">
        <span aria-hidden="true"><i class="fa fa-angle-left" aria-hidden="true"></i></span>
      </a>
    </li>
    <li :id="'page-item-' + item" class="page-item" :class="{active: currentPage === item}"
        :key="item"
        v-for="item in range(minPage, maxPage)">
      <a class="page-link" @click="changePage(item, $event)">{{item}}</a>
    </li>
    <li class="page-item next-page" :class="{disabled: currentPage === totalPages}">
      <a class="page-link" aria-label="Next" @click="nextPage">
        <span aria-hidden="true"><i class="fa fa-angle-right" aria-hidden="true"></i></span>
      </a>
    </li>
  </ul>
</template>
<script>
export default {
  name: "base-pagination",
  props: {
    pageCount: {
      type: Number,
      default: 0,
      description:
        "Pagination page count. This should be specified in combination with perPage"
    },
    perPage: {
      type: Number,
      default: 1,
      description:
        "Pagination per page. Should be specified with total or pageCount"
    },
    total: {
      type: Number,
      default: 0,
      description:
        "Can be specified instead of pageCount. The page count in this case will be total/perPage"
    },
    size: {
      type: String,
      default: "",
      description: "Pagination size"
    },
    align: {
      type: String,
      default: "",
      description: "Pagination alignment (e.g center|start|end)"
    }
  },
  computed: {
    totalPages() {
      if (this.pageCount > 0) return this.pageCount;
      if (this.total > 0) {
        return Math.ceil(this.total / this.perPage);
      }
      return 1;
    },
    pagesToDisplay() {
      if (this.totalPages > 0 && this.totalPages < this.defaultPagesToDisplay) {
        return this.totalPages;
      }
      return this.defaultPagesToDisplay;
    },
    minPage() {
      if (this.currentPage >= this.pagesToDisplay) {
        const pagesToAdd = Math.floor(this.pagesToDisplay / 2);
        const newMaxPage = pagesToAdd + this.currentPage;
        if (newMaxPage > this.totalPages) {
          return this.totalPages - this.pagesToDisplay + 1;
        }
        return this.currentPage - pagesToAdd;
      } else {
        return 1;
      }
    },
    maxPage() {
      if (this.currentPage >= this.pagesToDisplay) {
        const pagesToAdd = Math.floor(this.pagesToDisplay / 2);
        const newMaxPage = pagesToAdd + this.currentPage;
        if (newMaxPage < this.totalPages) {
          return newMaxPage;
        } else {
          return this.totalPages;
        }
      } else {
        return this.pagesToDisplay;
      }
    }
  },
  data() {
    return {
      defaultPagesToDisplay: 5,
      currentPage: 1
    };
  },
  methods: {
    range(min, max) {
      let arr = [];
      for (let i = min; i <= max; i++) {
        arr.push(i);
      }
      return arr;
    },
    changePage(item, event) {
      let pages = document.getElementsByClassName('page-item');
      pages.forEach(page => {
        page.classList.remove("active");
      });
      event.target.parentNode.classList.add("active");
      this.currentPage = item;
      this.$emit("input", item);
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        let pages = document.getElementsByClassName('page-item');
        pages.forEach(page => {
          page.classList.remove("active");
        });
        this.currentPage++;
        document.getElementById("page-item-" + this.currentPage).classList.add("active");
        this.$emit("input", this.currentPage);
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        let pages = document.getElementsByClassName('page-item');
        pages.forEach(page => {
          page.classList.remove("active");
        });
        this.currentPage--;
        document.getElementById("page-item-" + this.currentPage).classList.add("active");
        this.$emit("input", this.currentPage);
      }
    }
  },
  watch: {
    perPage() {
      this.$emit("input", 1);
    },
    total() {
      this.$emit("input", 1);
    }
  }
};
</script>
