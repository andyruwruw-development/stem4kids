<template>
  <div class="lesson">
    <PreviousLesson id="top"/>
    <div id="lesson-div">
      <h1 id="title">{{lesson.chapter}}.{{lesson.section}} {{lesson.title}}</h1>
      <div v-for="item in lesson.data" v-bind:key="item.index">
        <SubTitle v-if="item.type == 'subtitle'" v-bind:data="item.data" />
        <Paragraph v-if="item.type == 'paragraph'" v-bind:data="item.data" />
        <RenderedText v-if="item.type == 'text'" v-bind:text="item.data" />
      </div>
    </div>
    <NextLesson id="bottom"/>
  </div>
</template>

<script>
import PreviousLesson from '@/components/Lessons/PreviousLesson.vue'
import NextLesson from '@/components/Lessons/NextLesson.vue'

import SubTitle from '@/components/Lessons/SubTitle.vue'
import Paragraph from '@/components/Lessons/Paragraph.vue'
import RenderedText from '@/components/Lessons/Text.vue'

export default {
  name: 'lesson',
  components: {
    PreviousLesson,
    NextLesson,
    SubTitle,
    Paragraph,
    RenderedText
  },
  data() {
      return {
          
      }
  },
  methods: {

  },
  computed: {
    lesson() {
      return this.$store.state.lesson;
    },
  },
  async created() {
    await this.$store.dispatch("pathReset");

    let payload = {path: {name: "Courses", path: "/"}}
    await this.$store.dispatch("pathPush", payload);

    payload = {path: {name: this.$route.params.course, path: "/course/" + this.$route.params.course}};
    await this.$store.dispatch("pathPush", payload);

    payload = {course: this.$route.params.course, chapter: this.$route.params.chapter, section: this.$route.params.section};
    await this.$store.dispatch("getLesson", payload);

    payload = {path: {name: this.lesson.chapter + "." + this.lesson.section + " " + this.lesson.title, path: "/" + this.$route.params.course + "/lesson/" }};
    await this.$store.dispatch("pathPush", payload);

    console.log(this.lesson.data[0]);

  }
}
</script>

<style scoped>
/* Course Details */
.lesson {
  position: relative;
  display: block;
  width: 95%;
  max-width: 1100px;
  min-height: 500px;
  margin: 0 auto;
}

.top {
  position: absolute;
  top: 0px;
}

.bottom {
  position: absolute;
  bottom: 0px;
}

#lesson-div {
  display: block;
  margin: 50px 0px;
  padding: 50px;
  min-height: 500px;
  border-radius: 5px;
  background-color: white;
  box-shadow: 3px 3px 3px rgba(190, 190, 190, .8);
}

#title {
  text-align: left;
  font-weight: bolder;
  margin: 0;
  margin-bottom: 35px;
}
</style>