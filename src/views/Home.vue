<template>
  <v-app class="home">
    <navbar />

    <v-content>
      <v-container
        fluid
      >
        <v-row
          justify="center"
          align="center"
        >
          <v-col class="text-center">
            <v-data-table
              v-model="selected"
              :headers="headers"
              :items="desserts"
              :single-select="singleSelect"
              item-key="index"
              show-select
              class="elevation-1"
            >
              <template v-slot:top>
                <v-row class="mx-2">
                  <v-switch
                    v-model="singleSelect"
                    label="Single select"
                    class="pa-2"
                  />
                  <v-switch
                    v-model="english"
                    label="English / 中文"
                    class="pa-2"
                  />
                  <!-- <v-switch
                    v-model="chinese"
                    label="中文"
                    class="pa-2"
                  /> -->
                </v-row>
              </template>

              <template v-slot:item.englishAnswer="{ item }">
                <v-text-field
                  v-model="item.englishAnswer"
                />
              </template>

              <template v-slot:item.chineseAnswer="{ item }">
                <v-text-field
                  v-model="item.chineseAnswer"
                />
              </template>
            </v-data-table>
          </v-col>
        </v-row>
      </v-container>

      <v-footer
        color="indigo"
        app
      >
        <v-row justify="center">
          <span class="text-center white--text">&copy; new concept english</span>
        </v-row>
      </v-footer>
    </v-content>
  </v-app>
</template>

<script>
import Navbar from '@/components/navbar'

export default {
  name: 'Home',
  components: {
    Navbar
  },
  props: {
    source: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      singleSelect: false,
      english: false,
      chinese: false,
      selected: [],
      headers: [
        { text: 'English', value: 'english' },
        // { text: 'English answer', value: 'englishAnswer' },
        // { text: '中文答案', value: 'chineseAnswer' },
        { text: '中文', value: 'chinese' }
      ],
      desserts: [
        {
          english: 'hello',
          englishAnswer: 'hello',
          chineseAnswer: '你好',
          chinese: '你好'
        },
        {
          english: 'hello',
          englishAnswer: 'hello',
          chineseAnswer: '你好',
          chinese: '你好'
        },
        {
          english: 'hello',
          englishAnswer: 'hello',
          chineseAnswer: '你好',
          chinese: '你好'
        },
        {
          english: 'hello',
          englishAnswer: 'hello',
          chineseAnswer: '你好',
          chinese: '你好'
        }
      ]
    }
  },
  watch: {
    english (newValue) {
      if (newValue === true) {
        this.headers = [
          { text: 'English', value: 'english' },
          { text: '你的答案', value: 'chineseAnswer' }
        ]
      } else {
        this.headers = [
          { text: '中文', value: 'chinese' },
          { text: 'Your answer', value: 'englishAnswer' }
        ]
      }
    }
  },
  methods: {
    showEnglish () {
      this.english = !this.english
    },
    showChinese () {
      this.chinese = !this.chinese
    }
  }
}
</script>
