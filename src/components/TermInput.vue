<template>
    <form class="termInput" @submit="search">
        <input type="text" v-model="sTerm" autofocus required placeholder="Search Term">
        <input type="submit" value="Search">
    </form>
</template>

<script>
export default {
    name: "TermInput",
    data() {
        return {
            sTerm: ""
        };
    },
    methods: {
        search(e) {
            e.preventDefault();
            if(this.sTerm) {
                this.$emit('search', this.sTerm);
            }
            
            this.sTerm = "";
        }
    }
}
</script>

<style scoped>
.termInput {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 10px;
}

.termInput input[type="text"] {
    flex: 5;
    margin: 5px;
    padding: 5px;
    outline: none;
    border: none;
    border-bottom: none;
    font-size: 1.1em;
    color: white;
    background-color: slateblue;
}

.termInput input[type="text"]::placeholder {
    color: rgb(212, 212, 212);
}

.termInput input[type="text"]:focus {
    box-shadow: 0 0 8px white;
}

.termInput input[type="submit"] {
    flex: 1;
    margin: 5px;
    padding: 5px;
    background-color: slateblue;
    border: none;
    color: white;
    font-size: 1.1em;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
}

.termInput input[type="submit"]:hover {
    border: none;
    cursor: pointer;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
