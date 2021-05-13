<template>
  <header>
        <h1 class="brand">
            <a href="#">
              <img src="https://fontmeme.com/permalink/210512/c072857f28ffed69c9266a55183f4c20.png" alt="boolflix">
            </a>
        </h1>
      <form>
          <input type="text" v-model.trim="keyword" >
          <button type="submit" @click.prevent="$emit('searchKeyword', keyword)"><i class="fas fa-search"></i></button>
      </form>
  </header>
</template>

<script>
export default {
    name: 'Header',

    data() {
        return {
            keyword: '',
        }
    }
}
</script>

<style lang="scss" scoped>
    
    @import '@/assets/style/vars.scss';
    @import '@/assets/style/mixins.scss';

    header {
        @include flex-center('vertical');
        justify-content: space-between;
        padding-right: 10px; // test
        height: 90px;
        .brand {
            img {
                display: block;
            }


        }
    }
</style>