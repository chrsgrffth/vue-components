<script lang="coffee">
# To get the `action` prop:
#
# 1. Go to your dashboard on mailchimp.com and navigate 
#    to Lists > Signup Forms > Embedded Forms.
#
# 2. Copy the `<form>` action from the generated HTML code.
#
# 3. Pass that into the component via the prop, like so:
#
#      <mailchimp-subscribe 
#          action="//yourname.us10.list-manage.com/subscribe/post?u=012345678910&id=ab12345
#      ></mailchimp subscribe>

module.exports =
  name: "MailchimpSubscribe"

  props:
    action:
      required: true
      type: String

  data: ->
    email: ''
    response: {}
    errorMessage: null
    successMessage: null

  ready: ->
    # We need to receive jsonp from Mailchimp. So we update the 
    # action string.
    @action = @action.replace('/post?', '/post-json?').concat('&c=?')

  methods:
    subscribe: (e) ->
      params = $(e.currentTarget).serialize()

      $.ajax(
        type: 'POST'
        url: @action
        data: params
        dataType: 'jsonp'
        success: (res) =>
          if res.result == 'success'
            @successMessage = res.msg
          else
            @errorMessage = res.msg
            
            # Mailchimp returns error messages prefixed with numbers (ie "0 - Message"), so we'll
            # strip that out for the end user.
            @errorMessage = @errorMessage.substring(@errorMessage.indexOf('-')+1, @errorMessage.length)
      )
</script>

<template>
  <form v-if="!successMessage" @submit.prevent="subscribe($event)">
    <input v-model="email" name="EMAIL" type="text" placeholder="Email" id="email" />
    <input type="submit" />
  </form>
  <p v-if="errorMessage && !successMessage">{{ errorMessage }}</p>
  <p v-if="successMessage">{{ successMessage }}</p>
</template>
