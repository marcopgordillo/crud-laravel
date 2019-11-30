<template>
    <div class="crud row">
        <div class="col-2">
            <img class="img-thumbnail" :src="image"/>
        </div>
        <div class="col-2">
            <h3>Name: {{ name | properCase }}</h3>
            <div class="input-group mb-2">
                <div class="input-group-prepend">
                    <label class="input-group-text" :for="`inputGroupSelect${id}`">Color: </label>
                </div>
                <select class="custom-select" :id="`inputGroupSelect${id}`" @change="update">
                    <option
                        v-for="col in [ 'red', 'green' ]"
                        :value="col"
                        :key="col"
                        :selected="col === color ? 'selected' : ''"
                    >{{ col | properCase }}</option>
                </select>
            </div>
            <button class="btn btn-danger" @click="del">Delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CrudComponent",
        computed: {
            image() {
                return `/images/${this.color}.png`;
            }
        },
        methods: {
            update(val) {
                this.$emit('update', this.id, val.target.selectedOptions[0].value);
            },
            del() {
                this.$emit('delete', this.id);
            }
        },
        props: ['id', 'color', 'name'],
        filters: {
            properCase(string) {
                return string.charAt(0).toUpperCase() + string.slice(1);
            }
        }
    }
</script>

<style scoped>

</style>
