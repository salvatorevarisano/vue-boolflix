<template>
  <header>
        <div>
            <h1 class="brand">
                <a href="#">
                  <img src="https://fontmeme.com/permalink/210512/c072857f28ffed69c9266a55183f4c20.png" alt="boolflix">
                </a>
            </h1>
        </div>
        <div>
          <form>
              <input type="text" placeholder="searh" v-model.trim="keyword" >
              <button type="submit" @click.prevent="$emit('searchKeyword', keyword)"><i class="fas fa-search"></i></button>
          </form>
          <a href="#">
              <img class="avatar" src="@/assets/img/Netflix-avatar.png" alt="user">
          </a>
        </div>
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
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        @include flex-center('vertical');
        justify-content: space-between;
        padding-right: 10px; // test
        height: 90px;
        z-index: 10;
        background-color: $bg-color;
        .brand {
            img {
                display: block;
            }
        }
          
        & > div:last-of-type {
          
            @include flex-center('vertical');


            form {          
                & > * {
                    color: $text-color;
                    margin-right: 10px;
                    background-color: transparent;
                    border: none;
                    outline: none;
                    &:focus {
                        transform: scale(1.5);
                    }
                }
                & > button {
                    font-size: 1.2rem;
    
                }
            }
            .avatar {
                width: 30px;
            }
        }
    }
</style>