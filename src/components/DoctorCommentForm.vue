<template>
  <h3>Doctor’s comments</h3>
  <form class="review-form" @submit.prevent="onSubmit">
    <label for="comment">Add comment</label>
    <textarea id="comment" v-model="comment"></textarea>
    <input class="button" type="submit" value="Submit" />
  </form>

  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(com, index) in comments" :key="index">
        Comment {{ com.listNumber }}
        <br />
        "{{ com.comment }}"
        <br />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['id', 'event'],
  inject: ['GStore'], //<---Inject the Global Store
  data() {
    return {
      countlist: 0,
      comments: []
    }
  },
  methods: {
    onSubmit() {
      if (this.name === '' || this.review === '' || this.rating === null) {
        alert('Review is incomplete. Please fill out every field.')
        return
      }
      let doccomment = {
        listNumber: (this.countlist += 1),
        comment: this.comment
      }
      this.comments.push(doccomment)
      this.comment = ''
      //Assuming successful API call to register them
      //set a flash message to appear on the next page loaded which says
      //'You are successfully registerd for' +this.event.title
      this.GStore.flashMessage =
        'You are successfully commented for ' + this.event.title
      setTimeout(() => {
        //After 3 seconds remove it
        this.GStore.flashMessage = ''
      }, 3000)
      this.$router.push({
        name: 'EventRegister',
        params: { id: this.event.id }
      })
    }
  }
}
</script>

<style>
.button {
  margin: 30px;
  background-color: #5ae866;
  border-radius: 5px;
  font-size: 18px;
  width: 160px;
  height: 60px;
  color: black;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}
.button:hover {
  color: black;
  margin: 30px;
  background-color: #e85a5f;
  color: black;
  border-radius: 5px;
  font-size: 18px;
  width: 160px;
  height: 60px;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}
.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 0px 0px 0px 525px;
  border: 2px solid #0a0a0a;
  background-color: #a3fca2;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
  color: black;
}
.review-container {
  width: 425px;
  padding: 20px;
  background-color: #a3fca2;
  -webkit-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 20px -12px rgba(0, 0, 0, 0.57);
  margin: 60px 0px 0px 525px;
  border: 2px solid #0a0a0a;
  color: black;
}
.review-container li {
  margin-bottom: 30px;
}
.review-form .button {
  display: block;
  margin: 30px auto;
}
textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}
</style>
