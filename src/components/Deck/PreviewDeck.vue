.slice(5)<template lang='pug'>

.preview(v-if='deck.length > 0')
    .row
      .four.grid
          .bead.redwx(v-for="(b,i) in red", v-if="i < 5"  :b="b", @click='goto(b.taskId)')
      .four.grid
          .bead.greenwx(v-for="(b,i) in green", v-if="i < 5"  :b="b", @click='goto(b.taskId)')
      .four.grid
          .bead.bluewx(v-for="(b,i) in blue", v-if="i < 5"  :b="b", @click='goto(b.taskId)')
    .row
      .two.grid
      .four.grid
          .bead.yellowwx(v-for="(b,i) in yellow", v-if="i < 5"  :b="b", @click='goto(b.taskId)')
      .four.grid
          .bead.purplewx(v-for="(b,i) in purple", v-if="i < 5"  :b="b", @click='goto(b.taskId)')

</template>

<script>

import SharedTitle from '../slotUtils/SharedTitle'
import TaskCreate from '../forms/TaskCreate'

export default {
  props: ['memberId', 'taskId', 'task'],
  methods:{
    getTask(taskId){
        let task
        this.$store.state.tasks.forEach( t => {
            if (taskId === t.taskId) {
                task = t
            }
        })
        return task
    },
    goto(taskId){
        this.$router.push("/task/" + taskId)
    }
  },
  computed: {
      deck(){
          let tasks = []
          if (this.memberId) {
              tasks = this.$store.state.tasks.filter( t => t.deck.indexOf(this.memberId) !== -1 )
          } else if (this.taskId) {
              let subTasks = []
              this.$store.state.tasks.forEach( t => {
                  if (this.taskId === t.taskId){
                      t.subTasks.forEach(t => tasks.push( this.getTask(t)))
                  }
              })
          } else if (this.task && this.task.subTasks) {
              this.task.subTasks.forEach( tId => tasks.push( this.getTask(tId) ))
          }
          return tasks
      },
      red(){
          return this.deck.filter( c => { if(!c) { return false } return c.color === 'red' } )
      },
      yellow(){
          return this.deck.filter( c => { if(!c) { return false } return c.color === 'yellow' } )
      },
      blue(){
          return this.deck.filter( c => { if(!c) { return false } return c.color === 'blue' } )
      },
      purple(){
          return this.deck.filter( c => { if(!c) { return false } return c.color === 'purple' } )
      },
      green(){
          return this.deck.filter( c => { if(!c) { return false } return c.color === 'green' } )
      },
  },
  components:{
      SharedTitle,
      TaskCreate,
  },
}

</script>

<style lang="stylus" scoped>

@import '../../styles/colours'
@import '../../styles/grid'

.preview
    width: 100%
    opacity: 0.5

.bead
    height: 15px
    width: 100%
    border-radius: 50%;
    display: inline-block;
    border-width: 2px
    border-color: white
    border-style: solid


</style>
