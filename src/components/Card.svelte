<script>
  import Comments from './Comments.svelte';
  import Modal from './Modal.svelte';
  import Share from './Share.svelte';
  import { blur } from 'svelte/transition';
  import { likeCount } from '../store/store';

  export let username;
  export let avatar;
  export let location;
  export let photo;
  export let postComment;
  export let comments = [];
  let like = false;
  let bookmark = false;

  let isModal = false;

  const handleModal = () => {
    isModal = !isModal;
  };

  const handleLike = () => {
    like = !like;
    likeCount.update((n) => (like ? n + 1 : n - 1));
  };

</script>

<div class="Card">

  {#if isModal}
    <div transition:blur>
      <Modal>
        <Share on:click={handleModal}/>
      </Modal>
    </div>
  {/if}

  <div class="Card-container">
    <div class="Card-Header">
      <div class="Card-user">
        <img src={avatar} alt={username} />
        <h2>
          {username}
          <span>{location}</span>
        </h2>
      </div>
      <div class="Card-settings">
        <i class="fa fa-ellipsis-h"></i>
      </div>
    </div>
    <div class="Card-photo">
      <figure on:dblclick={handleLike}>
        <img src={photo} alt={username} />
      </figure>
    </div>
    <div class="Card-icons">
      <div class="Card-icons-first">
        <button on:click={handleLike}>
          <i class:active-like={like} class="fa fa-heart"></i>
        </button>
        <button on:click={handleModal}>
          <i class="fa fa-paper-plane"></i>
        </button>
      </div>
      <div class="Card-icon-second">
        <button on:click={() => (bookmark = !bookmark)}>
          <i class:active-bookmark={bookmark} class="fa fa-bookmark"></i>
        </button>
      </div>
    </div>
    <div class="Card-description">
      <h3>
        {username}
        <span>{postComment}</span>
      </h3>
    </div>
    <Comments {comments} />
  </div>
</div>

<style>
  .Card {
    box-shadow: rgba(0, 0, 0, 0.1) 0px 0px 5px 0px, rgba(0, 0, 0, 0.1) 0px 0px 1px 0px;
    border-radius: 10px;
    background-color: white;
    margin: 0 0 2em 0;
  }
  .Card-Header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1em;
  }
  .Card-user {
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .Card-user img {
    width: 32px;
    height: 32px;
    border-radius: 50%;
  }
  .Card-user h2 {
    margin: 0;
    padding: 0;
    font-size: 14px;
    font-weight: 600;
    margin: 0 0 0 1em;
    color: black;
  }
  .Card-user h2 span {
    display: block;
    font-size: 12px;
    font-weight: normal;
    color: rgba(38, 38, 38, 0.7);
  }
  .Card-photo {
    padding: 0;
    margin: 0;
  }
  .Card-photo img {
    width: 100%;
    height: auto;
  }
  .Card-photo figure {
    margin: 0;
    padding: 0;
    cursor: pointer;
  }
  .Card-settings i {
    cursor: pointer;
  }
  .Card-icons {
    padding: 1em;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .Card-icons i {
    margin: 0 1em 0 0;
    cursor: pointer;
    font-size: 20px;
  }
  .Card-icons button {
    border: none;
    background: none;
  }
  .Card-icons i:last-child {
    margin: 0;
  }
  .Card-description {
    padding: 0 1em 1em 1em;
  }
  .Card-description h3 {
    font-size: 14px;
    font-weight: bold;
    color: black;
  }
  .Card-description span {
    font-size: 14px;
  }
  .active-like {
    color: #bc1888;
    animation: bounce linear 0.8s;
    animation-iteration-count: 1;
    transform-origin: 20% 20%;
  }
  .active-bookmark {
    color: #f09433;
  }

  @keyframes bounce {
    0% {
      transform: translate(0px, 0px);
    }
    15% {
      transform: translate(0px, -25px);
    }
    30% {
      transform: translate(0px, 0px);
    }
    45% {
      transform: translate(0px, -15px);
    }
    60% {
      transform: translate(0px, 0px);
    }
    75% {
      transform: translate(0px, -5px);
    }
    100% {
      transform: translate(0px, 0px);
    }
  }
</style>
