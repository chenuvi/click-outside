<template>
  <div class="app" v-cloak>
      <div class="main" v-clickoutside="handleClose">
        <button @click="show = !show">点击显示下拉菜单</button>
        <div class="dropdown" v-show="show">
          <p>下拉框的内容，点击外面区域可以关闭</p>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      show:false
    }
  },
  methods:{
    handleClose:function () {
      this.show = false
    }
  },
  directives:{
            clickoutside:{
                bind(el,binging,vnode){
                  console.log('el: ', el);
                  console.log('binging: ', binging);
                    function documentHandler (e){
                        if (el.contains(e.target)){
                            return false
                        }
                        if (binging.expression) {
                           binging.value(e)
                           console.log('binging.value: ', binging.value);
                        }
                    }
                    el.__vueClickOutside__ = documentHandler
                    document.addEventListener('click',documentHandler)
                },
                unbind(el,binging){
                    document.removeEventListener('click',el.__vueClickOutside__)
                    delete el.__vueClickOutside__
                }
            }
  }
}
</script>

<style>
  [v-clock] {
    display:none;
  }
</style>
