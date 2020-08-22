<template>
    <v-container>
        <vue-simplemde v-model="body"/>
        <v-btn v-if="create_update" dark color="teal" @click="submit">
            Post
        </v-btn>
        <v-btn v-else dark color="green" @click="update">
            Update
        </v-btn>
    </v-container>
</template>

<script>
import VueSimplemde from 'vue-simplemde';
export default {
    components: {
        VueSimplemde,
    },
    props:['questionSlug'],
    data(){
        return {
            body:null,
            create_update: true,
            reply: null,
        }
    },
    created(){
        this.load();
    },
    methods:{
        load(){
            EventBus.$on('updateReply', (reply) => {
                this.reply = reply;
                this.body = reply.reply;
                window.scrollTo({
                    top: document.body.scrollHeight,
                    behavior: "smooth",
                });
                this.create_update = false ;
            });
        },
        submit(){
            axios.post(`/api/question/${this.questionSlug}/reply`,{body:this.body})
            .then(res => {
                EventBus.$emit('newReply',res.data.reply)
                window.scrollTo(0,0)
            });
            this.body = null;
        },
        update(){
            axios.patch(`/api/question/${this.questionSlug}/reply/${this.reply.id}`, 
            {body: this.body})
            .then(res => {
                window.scrollTo(0,0);
            });
        }
    }
}
</script>

<style>
</style>