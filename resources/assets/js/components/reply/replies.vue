<template>
    <v-container>
        <reply v-for="(reply, index) in content" 
        :key="reply.id" :reply=reply :questionSlug="questionSlug" :index="index" ></reply>
    </v-container>
</template>

<script>
import Reply from './reply.vue';
import User from '../../Helpers/User';
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

            Echo.private('App.User.' + User.id())
                .notification((notification) => {
                    this.content.unshift(notification.reply);
                });

            Echo.channel('deleteReplyChannel')
            .listen('DeleteReplyEvent', (e) => {
                console.log(e);
                for(let index = 0 ; index < this.content.length; index++){
                    if(this.content[index].id == e.id){
                        this.content.splice(index, 1);
                    }
                }
            });
        }
    }
}
</script>