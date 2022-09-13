<script>
  import Header from '../components/Header.svelte';
  import Main from '../components/Main.svelte';
  import Timeline from '../components/Timeline.svelte';
  import Sidebar from '../components/Sidebar.svelte';
  import { onMount } from 'svelte';
import Card from '../components/Card.svelte';

  let data = {};

  const API = 'https://kittygram-api.vercel.app/';

  onMount(async () => {
    const response = await fetch(API);
    data = await response.json();
    console.log(data);
  });

</script>

<Header />
<Main>
  <Sidebar { ...data.user } />
  <Timeline posts={data.posts} />
</Main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
  :global(body) {
    font-family: "Lato", sans-serif;
    background-color: #fafafa;
    color: rgba(38, 38, 38, 0.7);
    margin: 0;
    padding: 0;
  }
  :global(h1, h2, h3, h4, h5, h6) {
    margin: 0;
    padding: 0;
  }
</style>
