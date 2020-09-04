<template>
    <div>
        <v-btn icon @click="likeIt">
            <v-icon color="red">{{iconName}}</v-icon> {{likes_count}}
            <!-- <div v-if="liked">
                <v-icon color="red">favorite</v-icon> {{likes_count}}
            </div>
            <div v-else>
                <v-icon color="black">favorite_border</v-icon> {{likes_count}}
            </div> -->
        </v-btn>
    </div>
</template>


<script>
import User from '../../Helpers/User.js';
export default {
    data(){
        return {
            liked: this.reply.liked,
            likes_count: this.reply.like_count,
        }
    },
    props: ['reply'],
    created(){
        Echo.channel('likeChannel')
        .listen('LikeEvent', (e) => {
            if(this.reply.id == e.id){
                e.type == 1 ? this.likes_count++ : this.likes_count--;
            }
        });
    },
    computed: {
        iconName(){
            return this.liked ? "favorite" : "favorite_border";
        } 
    },
    methods: {
        likeIt(){
            if(User.loggedIn()){
                this.liked ? this.dec() : this.inc();
                this.liked = !this.liked;
            }
        },
        inc(){
            axios.post(`/api/like/${this.reply.id}`)
            .then(res => this.likes_count++ );
        },
        dec(){
            axios.delete(`/api/like/${this.reply.id}`)
            .then(res => this.likes_count-- );
        },
    }
}
</script>