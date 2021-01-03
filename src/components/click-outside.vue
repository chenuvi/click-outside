<template>
    <div>

    </div>
</template>

<script>
    export default {
        name:'ClickOutside',
        directives:{
            clickoutside:{
                bind(el,binging,vnode){
                    function documentHandler (e){
                        if (el.contains(e.target)){
                            return false
                        }
                        if (binding.expression) {
                            binding.value(e)
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

<style  scoped>

</style>