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
import EventService from "@/services/EventServices.js";
import { mapState } from "vuex";

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
  /*
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
  */
  /*
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get("http://localhost:3000/events");
      // console.log(events);
      return {
        events: data,
      };
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again.",
      });
    }
  },
  */
  /*
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents();
      return {
        events: data,
      };
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again.",
      });
    }
  },
  */
  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again.",
      });
    }
  },
  computed: mapState({
    events: (state) => state.events.events,
  }),
};
</script>
