<template>
    <div class="body">
        <div class="conteiner">
            <div class="dropZone"
                 @drop="onDrop($event, category.id)"
                 v-for="category in categories"
                 :key="category.id"
                 @dragover.prevent
                 @dragenter.prevent
            ><h4>{{category.title}}</h4>
                <div v-for="item in items.filter(x=>x.categoryId == category.id)" :key="item"
                     @dragstart="onDragStart($event, item)"
                     class="dragEl"
                     draggable="true">
                    <p>{{item.title}}</p>
                </div>
            </div>
        </div>
        <a  class="btnAu" href="https://oauth.vk.com/authorize?client_id=8140334&display=popup&redirect_uri=http://localhost:8080/&scope=friends&response_type=token&v=5.131&state=1"
        >Авторизоваться</a>
        <button @click="getData" id="btn">Вывести в консоль</button>

    </div>

</template>

<script>
    import {ref} from 'vue'

    export default {
        name: 'VkZone',
        setup(){
            const items = ref([
                {
                    id: 0,
                    title: 'Item A',
                    categoryId: 0
                },
                {
                    id: 1,
                    title: 'Item B',
                    categoryId: 0
                },
                {
                    id: 2,
                    title: 'Item C',
                    categoryId: 0
                },
                {
                    id: 3,
                    title: 'Item D',
                    categoryId: 0
                },
                {
                    id: 4,
                    title: 'Item E',
                    categoryId: 0
                },
                {
                    id: 5,
                    title: 'Item F',
                    categoryId: 0
                },
                {
                    id: 6,
                    title: 'Item G',
                    categoryId: 0
                },
                {
                    id: 7,
                    title: 'Item J',
                    categoryId: 0
                },
                {
                    id: 8,
                    title: 'Item K',
                    categoryId: 0
                },
                {
                    id: 9,
                    title: 'Item L',
                    categoryId: 0
                },
                {
                    id: 10,
                    title: 'Item M',
                    categoryId: 0
                },
                {
                    id: 11,
                    title: 'Item N',
                    categoryId: 0
                },
                {
                    id: 12,
                    title: 'Item P',
                    categoryId: 0
                },
            ])
            const categories = ref([
                {
                    id: 0,
                    title: 'Friends'
                },
                {
                    id: 1,
                    title: 'TwoPage'
                }
            ])

            function onDragStart(e, item) {
                e.dataTransfer.dropEffect = 'move'
                e.dataTransfer.effectAllowed = 'move'
                e.dataTransfer.setData('itemId', item.id.toString())
            }
            function onDrop(e, categoryId) {
                const itemId = parseInt(e.dataTransfer.getData('itemId'))
                items.value = items.value.map(x => {
                    if(x.id == itemId)
                        x.categoryId = categoryId
                    return x
                })
            }
            // }
            return{
                items,
                categories,
                onDragStart,
                onDrop
            }
        },
        methods:{
                getData() {
                    if (this.categoryId == 1) {
                        console.log(this.items)
                    }
                    console.log(this.items)
            }

        }

    }

</script>


<style >
    .conteiner{
        display: flex;
        flex-direction: row;
    }
    .body{
        width: 503px;
        padding: 10px;
        background: linear-gradient(179.94deg, #CA6C6C 0.05%, rgba(89, 40, 24, 0.9375) 99.94%, rgba(255, 14, 14, 0) 99.95%);
        text-align: center;
        display: flex;
        flex-flow: row wrap

    }
    .dropZone{
        margin: 30px;
        width: 200px;
        height: 376px;
        background: #c4c4c4;
        border-radius: 26px;
        overflow-x:scroll;
    }

    .dragEl{
        width: 167px;

        text-align: center;
        background: #F5D9D9;
        border-radius: 6px;
        margin-left: 12px;
    }
    #btn{

        width: 200px;
        height: 46px;
        margin-left: 55px;
        background: linear-gradient(180deg, #C0AA70 0%, rgba(255, 233, 36, 0.291667) 100%, rgba(166, 168, 76, 0) 100%);
        border-radius: 6px;
    }
    .btnAu{
        padding-top: 10px;
        width: 200px;
        height: 35px;
        margin-left: 30px;
        text-align: center;
        background: linear-gradient(180deg, #C0AA70 0%, rgba(255, 233, 36, 0.291667) 100%, rgba(166, 168, 76, 0) 100%);
        border-radius: 6px;
    }

</style>
