<template>
  <div>
    <h1>Events</h1>
      <EventCard
        v-for="(event, index) in events"
        :key="index"
        :event="event"
        :data-index="index"
      />
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Event Listing",
    };
  },
  // asyncData(context) {
  //   return context.$axios
  //     .get("http://localhost:3000/events")
  //     .then((response) => {
  //       return {
  //         events: response.data,
  //       };
  //     });
  // },
  // ES6 Destructuring
  asyncData({ $axios, error }) {
    return $axios
      .get("http://localhost:3000/events")
      .then((response) => {
        return {
          // this object gets merged with our component data
          // so there is no need to declare data()
          // since what is returned here is the component data
          events: response.data,
        };
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: "Unable to fetch events at this time. Please try again.",
        });
      });
  },
};
</script>

<style scoped>
</style>