<script>
  // import { onMount } from "svelte";
  import Header from "../components/Header.svelte";
  import Main from "../components/Main.svelte";
  import Sidebar from "../components/Sidebar.svelte";
  import TimeLine from "../components/TimeLine.svelte";

  let info = [];
  const API = "https://kittygram-api.vercel.app/";

  const getData = () => {
    return fetch(API)
      .then(response => response.json())
      // .then(data => info = data);
  }

</script>

<Header />
<Main>
  {#await getData()}
    <h2>Loading...</h2>
  {:then info}
    <TimeLine posts={info.posts}/>
    <Sidebar {...info.user.name} {...info.user.nickname} />
  {:catch error}
    {error}
  {/await}
</Main> 

<style>
  @import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
  :global(body) {
    background-color: #fafafa;
    color: rgba(38, 38, 38, 0.7);
    font-family: "Lato", sans-serif;
    margin: 0;
    padding: 0;
  }
  :global(h1, h2, h3){
    margin: 0;
    padding: 0;
  }
</style>
