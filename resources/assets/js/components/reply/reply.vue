<template>
    <div class="mt-4">
        <v-card>
            <v-card-title>
                <div class="headline">{{reply.user}} </div>
                <div class="ml-2"> said {{reply.created_at}}</div>
                <v-spacer></v-spacer>
                <like :reply="reply"></like>
            </v-card-title>
            <v-divider></v-divider>

            <edit-reply :reply="reply" v-if="editing"></edit-reply>
            <v-card-text v-else v-html="parsed_reply"></v-card-text>

            <v-divider></v-divider>
            <div v-if="!editing">
                <v-card-actions v-if="own">
                    <v-btn icon small @click="edit">
                        <v-icon color="orange">edit</v-icon>
                    </v-btn>
                    <v-btn icon small @click="remove">
                        <v-icon color="red">delete</v-icon>
                    </v-btn>
                </v-card-actions>
            </div>
            
        </v-card>
    </div>
</template>


<script>
import md from 'marked';
import EditReply from './editReply.vue';
import Like from '../likes/like.vue';

export default {
    props: ['reply', 'questionSlug', 'index'],
    data(){
        return {
            editing: false ,
        }
    },
    components: {
        EditReply, Like,
    },
    computed: {
        own(){
            return User.own(this.reply.user_id);
        },
        parsed_reply(){
            return md.parse(this.reply.reply);
        }
    },
    created(){
        this.listen();
    },
    methods: {
        remove(){
            axios.delete(`/api/question/${this.questionSlug}/reply/${this.reply.id}`)
            .then(res => {
                EventBus.$emit('deleteReply', this.index);
            });
        },
        edit(){
            this.editing = true;
        },
        listen(){
            EventBus.$on('cancelEditing', () => {
                this.editing = false ;
            });
        }
    }
}
</script>