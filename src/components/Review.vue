<template>
  <div class="container">
    <h4 class="uppercase">reviews</h4>
    <div class="review" v-for="review in reviews">
      <p>{{ review.content }}</p>
      <div class="row">
        <div class="columns medium-7">
          <h5>{{ review.reviewer }}</h5>
        </div>
        <div class="columns medium-5">
          <h5 class="pull-right">{{ review.time }}</h5>
        </div>
      </div>
    </div>
    <div class="review-form" v-if="movie">
      <h5>add new review.</h5>
      <form @submit.prevent="addReview">
        <label>
          Review
          <textarea v-model="review.content" cols="30" rows="5"></textarea>
        </label>
        <button
          :disabled="!review.reviewer || !review.content"
          type="submit"
          class="button expanded"
        >
          Submit
        </button>
      </form>
    </div>
  </div>
</template>

<script>
const MOCK_REVIEWS = [
  {
    movie_id: 7128,
    content: "Great show! I loved every single scene.",
    reviewer: "Jane Doe",
    time: newDate().toLocaleDateString()
  }
];
import bus from "../bus";
export default {
  name: "reviews",
  data() {
    return {
      mockReviews: MOCK_REVIEWS,
      movie: null,
      review: {
        content: "",
        reviewer: ""
      }
    };
  },
  created() {
    bus.$on("new_movie", movieId => {
      this.movie = movieId;
    });
  },
  computed: {
    reviews() {
      return this.mockReviews.filter(review => {
        return review.movie_id === this.movie;
      });
    }
  },
  methods: {
    addReview() {
      if (!this.movie || !this.review.reviewer || !this.review.content) {
        alert("please make sure all the fields are not empty");
        return;
      }
      let review = {
        movie_id: this.movie,
        content: this.review.content,
        reviewer: this.review.reviewer,
        time: new Date().toLocaleDateString()
      };
      this.mockReviews.unshift(review);
    }
  }
};
</script>

<style scoped>
.container {
  padding: 0 20px;
}
.review {
  border: 1px solid #ddd;
  font-size: 0.95em;
  padding: 10px;
  margin: 15px 0 5px 0;
}
.review h5 {
  text-transform: uppercase;
  font-weight: bolder;
  font-size: 0.7em;
}

.pull-right {
  float: right;
}

.review-form {
  margin-top: 30px;
  border-top: 1px solid #ddd;
  padding: 15px 0 0 0;
}
</style>
