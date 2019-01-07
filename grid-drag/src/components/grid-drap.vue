<template>
    <div class="grid-drag" v-on:dragstart="dragstart" v-on:dragover.prevent="dragover" v-on:drop.prevent="drop">
        <slot></slot>
    </div>
</template>
<style scoped>
    .grid-drag{
        display: inline-flex;
        display: -webkit-inline-flex;
        flex-wrap: wrap;
    }
</style>
<script>
export default {
    name: 'grid-drap',
    data(){
        return{
            sourceIndex: -1
        }
    },
    mounted() {
        this.initGridDragItem(this.$children);
    },
    methods: {
        dragstart: function(e){
            console.log('start: ', e)
            this.sourceIndex = Number(e.target.id.match(/\d+/)[0]);
        },
        dragover: function(){},
        drop: function(e){
            console.log('end: ', e)
            let { sourceIndex } = this._data,
                targetIndex = this.getTargetIndex(e.path),
                sourceEl = this.$children[sourceIndex],
                direction = targetIndex - sourceIndex,
                children = [];
                   
            this.$children.forEach((item, index)=>{
                if(targetIndex === index){
                    if(direction < 0) children.push(sourceEl);
                    children.push(item);
                    if(direction > 0) children.push(sourceEl);
                }else if(sourceIndex !== index){
                    children.push(item);
                }
            });
            this.$children = children;
            this.initGridDragItem(this.$children);
        },
        /**
         * 初始化元素的属性
         * @param {Array} children 子元素数组
         *  */
        initGridDragItem: function(children){
            for(var i = 0, len = children.length; i < len; i++){
                children[i].$el.id = `dragItem${i}`;
                children[i].$el.style = `order: ${i}`;
            }
        },
        /**
         * 获取被拖动元素的目标元素的索引
         * @param {Array} path 元素的路径 
         * @returns {Number} index 索引
         * */
        getTargetIndex: function(path){
            for(var i = 0, len = path.length; i < len; i++){
                if(path[i].id && /^dragItem/.test(path[i].id)) 
                    return Number((path[i].id).match(/\d+/)[0]);
            }

            console.error(`请不要给子元素id设置为以dragItem开头`);
            return -1;
        }
    }
}
</script>
