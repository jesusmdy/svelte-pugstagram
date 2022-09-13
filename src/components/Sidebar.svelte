<script>
  import Profile from '../components/Sidebar/Profile.svelte';
  import Stories from '../components/Sidebar/Stories.svelte';
  import Footer from '../components/Sidebar/Footer.svelte';
  export let nickname;
  export let name;
</script>

<div class="Sidebar">
  <div class="Sidebar-container">
    <Profile {nickname} {name} />
    <Stories />
    <Footer />
  </div>
</div>

<style>
  .Sidebar {
    position: relative;
    padding: 4.5em 0 0 0;
  }
  .Sidebar-container {
    position: fixed;
  }
</style>
