<template>
    <div>
        <submit-input></submit-input>
        <my-list></my-list>
    </div>
</template>

<script>

import SubmitInput from '../components/submitInput'
import MyList from '../components/list'

export default {
  components: {
    SubmitInput,
    MyList
  },
  mounted(){
      document.title = 'Simple Twitter'
  }
}
</script>

