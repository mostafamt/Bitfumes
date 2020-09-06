<template>
    <div v-if="question">
        
        <edit-question 
            :data = question
            v-if="editing">
        </edit-question>
        
        <show-question
            v-else
            :data = question
        ></show-question>

        <replies :replies="question.replies" :questionSlug="question.slug" ></replies>

        <new-reply v-if="loggedIn" :questionSlug=question.slug ></new-reply>
        <v-container v-else>
            <router-link to="/login">Login to reply</router-link>
        </v-container>

    </div>
</template>

<script>

import ShowQuestion from './ShowQuestion.vue';
import EditQuestion from './editQuestion';
import Replies from '../reply/replies.vue';
import NewReply from '../reply/newReply.vue';

export default {
    components:{ShowQuestion, EditQuestion, Replies, NewReply},
    data(){
        return{
            question: null,
            editing: false,
        }
    },
    created(){
        this.listen();
        this.getQuestion();
    },
    computed: {
        loggedIn(){
            return User.loggedIn();
        }
    },
    methods: {
        listen(){
            EventBus.$on('startEditing', () => {
                this.editing = true;
            });

            EventBus.$on('cancelEditing', () => {
                this.editing = false ;
            });

        },
        getQuestion(){
            axios.get(`/api/question/${this.$route.params.slug}`)
            .then(res => this.question = res.data.data);
        }
    }
}
</script>