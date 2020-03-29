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
          <v-col
            class="text-center"
          >
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
                    v-model="showChinese"
                    label="English / 中文"
                    class="pa-2"
                  />
                  <v-switch
                    v-model="showBoth"
                    label="Both"
                    class="pa-2"
                  />
                </v-row>
              </template>

              <template v-slot:item.answer="{ item }">
                <v-text-field
                  v-model="item.answer"
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
  data () {
    return {
      singleSelect: false,
      showChinese: false,
      showBoth: false,
      selected: [],
      headers: [
        { text: 'English', value: 'english' },
        { text: 'Answer', value: 'answer' }
      ],
      desserts: [
        {
          english: 'hello',
          chinese: '你好',
          answer: ''
        },
        {
          english: 'hello',
          chinese: '你好',
          answer: ''
        },
        {
          english: 'hello',
          chinese: '你好',
          answer: ''
        },
        {
          english: 'hello',
          chinese: '你好',
          answer: ''
        }
      ]
    }
  },
  watch: {
    showChinese (newValue) {
      if (newValue === true) {
        this.headers = [
          { text: 'English', value: 'english' },
          { text: 'Answer', value: 'answer' }
        ]
      } else {
        this.headers = [
          { text: '中文', value: 'chinese' },
          { text: 'Answer', value: 'answer' }
        ]
      }
    },
    showBoth (newValue) {
      if (newValue === true) {
        this.headers = [
          { text: 'English', value: 'english' },
          { text: '中文', value: 'chinese' },
          { text: 'Answer', value: 'answer' }
        ]
      } else if (this.showChinese === true) {
        this.headers = [
          { text: 'English', value: 'english' },
          { text: 'Answer', value: 'answer' }
        ]
      } else {
        this.headers = [
          { text: '中文', value: 'chinese' },
          { text: 'Answer', value: 'answer' }
        ]
      }
    }
  },
  methods: {
    // 自动批改实现方法
  }
}
</script>
