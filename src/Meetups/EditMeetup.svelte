<script>
  import { createEventDispatcher } from "svelte";
  import TextInput from "../UI/TextInput.svelte";
  import Button from "../UI/Button.svelte";
  import Modal from "../UI/Modal.svelte";

  let dispatch = createEventDispatcher();
  let id;
  let title = "";
  let subtitle = "";
  let description = "";
  let imageUrl = "";
  let location = "";
  let contactEmail = "";

  function submitForm() {
    dispatch("addMeetup", {
      title,
      subtitle,
      description,
      imageUrl,
      location,
      contactEmail
    });
  }
</script>

<style>
  form {
    width: 95%;
    margin: 1rem;
  }
</style>

<Modal on:cancel>
  <form on:submit|preventDefault={submitForm}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      on:input={event => (title = event.target.value)} />
    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={event => (subtitle = event.target.value)} />
    <TextInput
      id="description"
      label="Description"
      value={description}
      controlType="textarea"
      rows="4"
      on:input={event => (description = event.target.value)} />
    <TextInput
      id="location"
      label="Location"
      value={location}
      on:input={event => (location = event.target.value)} />
    <TextInput
      id="image"
      label="ImageUrl"
      value={imageUrl}
      on:input={event => (imageUrl = event.target.value)} />
    <TextInput
      id="email"
      type="email"
      label="Contact Email"
      value={contactEmail}
      on:input={event => (contactEmail = event.target.value)} />
  </form>
  <div slot="footer">
    <Button type="button" on:click={submitForm}>Save</Button>
    <Button type="button" mode="outline" on:click={() => dispatch('cancel')}>
      Close
    </Button>
  </div>
</Modal>
