<template>
    <v-container>
        <reply v-for="(reply, index) in content" 
        :key="reply.id" :reply=reply :questionSlug="questionSlug" :index="index" ></reply>
    </v-container>
</template>

<script>
import Reply from './reply.vue';
export default {
    props: ['replies', 'questionSlug'],
    data(){
        return {
            content: this.replies,
        }
    },
    components: {
        Reply,
    },
    created(){
        this.listen();
    },
    methods: {
        listen() {
            EventBus.$on('newReply', (reply) => {
                this.content.unshift(reply);
            });

            EventBus.$on('deleteReply', (idx) => {
                this.content.splice(idx,1);
            });
        }
    }
}
</script>