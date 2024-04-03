<template>
    <div class="task">
        <input type="checkbox" v-model="isChecked" @change="updateDone">
        <p :style="isDone">{{ task }}</p>
        <button @click="$emit('remove', task)"><svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"/></svg></button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isChecked: this.done
        }
    },
    props: {
        task: {
            type: String,
            required: true
        },
        done: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        updateDone() {
            this.$emit('update:done', this.isChecked);
            this.$emit('changeDone', this.done);
        }
    },
    computed: {
        isDone() {
            return this.isChecked ? 'text-decoration: line-through' : 'text-decoration: none';
        }
    }
}
</script>

<style lang="scss" scoped>
.task{
    display: flex;
    margin-top: 30px;
    box-shadow: 0px 0px 15px 4px rgba(0, 0, 0, 0.26);
    border: 3px solid black;
    border-radius: 20px;
    width: 80%;
    align-self: center;
    justify-content: space-between;
    input{
      margin-left: 30px;
    }
    p{
      overflow-wrap: break-word;
      width: 70%;
      text-align: center;
      font-size: 20px;
    }
    button{
      background: white;
      width: 40px;
      height: 40px;
      align-self: center;
      margin-right: 30px;
      border: 0;
      cursor: pointer;
      svg{
        font-size: 40px;
      }
    }
}
</style>