<template>
    <div class="conspiracy-item" @click="favouriteConspiracy(conspiracy.id)">
        <div class="user-profile__conspiracy">
            <div class="conspiracy-item__user">
                @{{username}}
            </div>
            <div class="conspiracy-item__content">
                {{conspiracy.content}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ConspiracyItem",
    props: {
        username: {
            type: String,
            required: true
        },
        conspiracy:  {
            type: Object,
            required: true
        }
    },
    methods: {
        favouriteConspiracy(id){
            this.$emit('favourite', id)
        }
    }
}
</script>

<style scoped>
.conspiracy-item{
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
    width: 80%;
}

.conspiracy-item:hover{
    transform: scale(1.1, 1.1);
}

.conspiracy-item__user {
    font-weight: bold;
}
</style>