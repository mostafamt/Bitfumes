<template>
  <v-card class="mt-2">
    <v-card-title primary-title>
      <div>
        <h3 class="headline mb-0">
            <router-link :to="question.path">
                {{question.title}}
            </router-link>
        </h3>
        <div class="grey--text">
            {{question.user}} said {{question.created_at}}
        </div>
      </div>
    </v-card-title>
    <v-card-text v-html="parsed_question"></v-card-text>
  </v-card>
</template>

<script>
import md from 'marked';
export default {
    props:['question'],
    computed: {
      parsed_question(){
        return md.parse(this.question.body);
      }
    }
}
</script>


<style>

</style>