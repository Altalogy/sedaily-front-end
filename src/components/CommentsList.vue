<template>
  <div>
    <div v-if="loading" class="spinner-holder">
      <spinner :show="loading" />
    </div>
    <div v-else v-for="comment in comments" :key="comment._id">
      <div class='row' :id='comment._id'>
        <div class='col-md-12' >
          <comment-view
            :rootEntityType='rootEntityType'
            :comment='comment'
            :isParentComment="true" />
        </div>
      </div>
        <div class='replies'>
          <div v-for="replyComment in comment.replies" :key="replyComment._id">
            <comment-view
              :rootEntityType='rootEntityType'
              :comment='replyComment' />
          </div>
        </div>
      <br />
    </div>
  </div>
</template>

<script>
import CommentView from 'components/CommentView.vue'
import Spinner from '@/components/Spinner.vue'

export default {
  name: 'comments-list',
  props: {
    comments: {
      type: Array,
      required: true
    },
    rootEntityType: {
      type: String,
      required: false
    },
    loading: {
      type: Boolean,
      required: false,
      default: false
    },
  },
  beforeMount () {},
  components: { CommentView, Spinner },
  computed: {
    emptyComments () {
      if (!this.comments || this.comments.length === 0) {
        return true
      }
      return false
    },

  },
  // mounted () {
  //     let id = this.comments.slice(-1)[0]._id
  //     let scrollToId = document.getElementById(`${id}`)
  //     scrollToId.scrollIntoView({behavior: "smooth", block: "start", inline: "center"})
  //   }
  }
</script>

<style scoped lang="stylus">
.replies
  // margin-top 45px
  padding-left 25px
.no-comments
  padding-top 20px
  color #ccc

.spinner-holder
  width 100%

</style>
