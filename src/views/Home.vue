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
                    label="Select"
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
                  :error="item.error"
                />
              </template>
            </v-data-table>
          </v-col>
        </v-row>

        <v-row
          justify="center"
        >
          <v-col class="text-center">
            <v-btn @click="submit">
              Submit
            </v-btn>
          </v-col>
        </v-row>

        <v-row>
          <v-col>
            <div>
              <p>Total: {{ total }}</p>
              <p>Correct: {{ correct }}</p>
              <p>Wrong: {{ mistake }}</p>
              <p>Correct Rate: {{ correctRate }} %</p>
            </div>
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
      correct: 0,
      correctRate: 0,
      mistake: 0,
      headers: [
        { text: 'English', value: 'english' },
        { text: 'Answer', value: 'answer' }
      ],
      desserts: [
        {
          english: 'insects',
          chinese: '昆虫',
          answer: ''
        },
        {
          english: 'enemies',
          chinese: '敌人',
          answer: ''
        },
        {
          english: 'race',
          chinese: '种族',
          answer: ''
        },
        {
          english: 'devour',
          chinese: '吞食',
          answer: ''
        }
      ]
    }
  },
  computed: {
    total () {
      return this.desserts.length > 0 ? this.desserts.length : 0
    }
  },
  watch: {
    showChinese (newValue) {
      if (newValue === false) {
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
    submit () {
      if (this.showChinese === false) {
        this.calclateGrade(this.desserts, 'english')
      }

      this.calclateGrade(this.desserts, 'chinese')
    },
    calclateGrade (wordsArray, language) {
      let correctArr = []
      let mistakeArr = []

      wordsArray.map((value, index) => {
        if (value[language] === value.answer) {
          correctArr.push(value.answer)
          this.$set(this.desserts[index], 'error', false)
        } else {
          mistakeArr.push(value.answer)
          this.$set(this.desserts[index], 'error', true)
        }
      })

      this.correct = correctArr.length
      this.mistake = mistakeArr.length
      this.correctRate = (this.correct / this.total) * 100
    }
  }
}
</script>
