<template>
    <div class="serach">
        <div class="search-position">
            <span class="icon iconfont" :class="[active ? 'icon-zuojiantou' : 'icon-htmal5icon14']"></span>
        </div>
        <div class="search-input border-bottom-1px">
            <input ref="search" id="searchText" :value="searchText" type="text" placeholder="查找">
        </div>
        <div class="serach-button">
            <!-- <button>查找</button> -->
            <router-link to='/searchResult'>
                <cube-button @click.native="search">查找</cube-button>
            </router-link>
        </div>
    </div>
</template>

<script>
    import {mapMutations,mapState} from 'vuex'
    export default {
        data() {
            return {
                active: false,
            }
        },
        computed:{
            ...mapState(['searchText'])
        },
        methods: {
            search() {
                var searchText = this.$refs.search.value
                console.log(searchText)
                this.setSearchText(searchText)
                this.$emit('searchData')
            },
            ...mapMutations({
                setSearchText: 'SET_SEARCHTEXT'
            })
        },
        watch:{
            $route(newValue) {
                newValue.name=='searchResult' ? this.active = true : this.active = false
            }
        }
    }
</script>

<style lang='stylus' scoped>
    .cube-btn
        border-radius 10px
        padding 8px 28px
    .serach
        position absolute
        top 0
        width 100%
        z-index 100
        height 44px
        background #d22e7d
        display flex
        align-items center
        .search-position 
            display flex
            width 20%
            align-items center
            justify-content center
            .icon
                color #ffffff
                font-size 28px
        .search-input
            flex 1
            margin-bottom 10px;
            height 100%
            input 
                background transparent 
                height 100%
                padding-left 10px
                color #fff
                &::placeholder
                    color #ff83c8
        .serach-button
            width 25%
            margin-right 10px
            margin-left 10px
</style>