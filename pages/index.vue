<template>
  <div class="">
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import { mapState } from "vuex";
import EventCard from "~/components/EventCard.vue";

export default {
  name: "IndexPage",
  components: { EventCard },
  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again later.",
      });
    }
  },
  head() {
    return {
      title: "Event Listing",
    };
  },
  computed: {
    ...mapState({
      events: (state) => state.events.events,
    }),
  },
};
</script>
