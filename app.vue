<script lang="coffee">
  
  # Import Vue.
  Vue = require 'vue'

  # Instantiate Vue instance.
  app = new Vue({
    el: 'body'
    components:
      mailchimpSubscribe: require('./components/mailchimp-subscribe')
  })

</script>