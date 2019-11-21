<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import EditMeetup from "./Meetups/EditMeetup.svelte";
  import Button from "./UI/Button.svelte";

  let editMode = null;

  export let meetups = [
    {
      id: "326723",
      title: "Sunday Code and Coffee",
      subtitle: "Get together with other coders",
      description: "At this meetup we get together to discuss javascript",
      imageUrl:
        "https://images.unsplash.com/photo-1556745753-b2904692b3cd?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60",
      location: "Catford Mews SE6",
      contactEmail: "code@webnostix.co.uk",
      isFavorite: false
    },
    {
      id: "326724",
      title: "Sunday Code and Coffee",
      subtitle: "Get together with other coders",
      description: "At this meetup we get together to discuss javascript",
      imageUrl:
        "https://images.unsplash.com/photo-1497515114629-f71d768fd07c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60",
      location: "Catford Mews SE6",
      contactEmail: "code@webnostix.co.uk",
      isFavorite: false
    }
  ];

  function addMeetup(event) {
    const newMeetup = {
      id: Math.random().toString(),
      title: event.detail.title,
      subtitle: event.detail.subtitle,
      description: event.detail.description,
      imageUrl: event.detail.imageUrl,
      location: event.detail.location,
      contactEmail: event.detail.contactEmail
    };
    meetups = [newMeetup, ...meetups];
    editMode = null;
  }

  function toggleFavorite(event) {
    console.log("toggle");
    const id = event.detail;
    const updatedMeetup = { ...meetups.find(m => m.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
    const meetupIndex = meetups.findIndex(m => m.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;
    meetups = updatedMeetups;
    console.log(meetups);
  }
</script>

<style>
  main {
    margin-top: 5rem;
  }
  .meetup-controls {
    margin: 1rem;
  }
</style>

<Header />

<main>
  <div class="meetup-controls">
    <Button on:click={() => (editMode = true)}>New Meetup</Button>
  </div>
  {#if editMode}
    <EditMeetup on:addMeetup={addMeetup} on:cancel={() => (editMode = false)} />
  {/if}
  <MeetupGrid {meetups} on:togglefavorite={toggleFavorite} />
</main>
