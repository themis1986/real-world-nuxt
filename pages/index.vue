<template>
  <div class="">
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from "~/components/EventCard.vue";
export default {
  name: "IndexPage",
  components: { EventCard },
  asyncData({ $axios, error }) {
    return $axios
      .get("http://localhost:3001/events")
      .then((res) => {
        return {
          events: res.data,
        };
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: "Unable to fetch events at this time. Please try again later.",
        });
      });
  },
  head() {
    return {
      title: "Event Listing",
    };
  },
};
</script>
