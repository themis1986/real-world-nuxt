<template>
  <div class="">
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventService from "@/services/EventService.js";
import EventCard from "~/components/EventCard.vue";

export default {
  name: "IndexPage",
  components: { EventCard },
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents();
      return {
        events: data,
      };
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
};
</script>
