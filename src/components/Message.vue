<template>
  <div class="message_item" @click="favouriteMessage(message.id)">
    <div class="user-profile_message">
      <div class="message-item_user">@{{ username }}
      </div>
      <div class="message_item_content">
        {{message.content}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    username: {
      type: String,
      required: true,
    },
    message: {
      type: Object,
      required: true,
    },
  },
  methods:{
      favouriteMessage(id){
          this.$emit("favourite",id)
      }
  }
};
</script>

<style>
.message_item{
    padding:20px;
    background-color:white;
    border-radius:5px;
    border:1px solid #DFE3E8;
    box-sizing:border-box;
    cursor:pointer;
    transition:all 0.25s ease;
}

.message_item:hover {
    transform:scale(1.1, 1.1)
}

.message-item_user{
    font-weight:bold;
}

</style>
