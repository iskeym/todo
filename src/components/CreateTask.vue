<template>
<div class="dialog" @click.stop="hideDialog" v-show="show">
    <form @submit.prevent>
        <div class="dialog__content" @click.stop>
            <input type="text" placeholder="Выслушать кота" v-model="task.text">
            <button @click="createTask">Создать задачу</button>
        </div>
    </form>
</div>
</template>

<script>
export default {
    data() {
        return {
            task: {
                text: '',
                done: false
            }
        }
    },
    props: {
        show: {
            type: Boolean,
            default: false
        },
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false)
        },
        createTask() {
            this.task.id = Date.now()
            this.$emit('create', this.task)
            this.task = {
                text: '',
                done: false
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.dialog{
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.519);
    display: flex;
    justify-content: center;
    form{
        width: 70%;
        height: 80px;
    }
    &__content{
        margin-top: 200px;
        padding: 30px;
        background-color: white;

        display: flex;
        flex-direction: column;
        border-radius: 20px;
        box-shadow: 0px 0px 10px 8px rgba(0, 0, 0, 0.48);
        input{
            text-align: center;
            height: 40px;
            font-size: 20px;
            border-radius: 10px;
        }
        button{
            margin-top: 20px;
            width: 150px;
            height: 40px;
            background: white;
            border: 2px solid black;
            border-radius: 10px;
            align-self: center;
            transition-property: all;
	        transition-duration: 0.3s;
            cursor: pointer;
            &:hover{
                background: rgb(210, 210, 210)
            }
        }
    }
}
</style>