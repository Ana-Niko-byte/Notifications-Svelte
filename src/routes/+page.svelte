<script lang="ts">

interface Detail {
  name: string;
  action: string[];
  active: boolean;
  time: string;
  status: boolean;
  club?: string | null; 
  post?: string;
  message?: string;
}

    let actions = ['reacted to your recent post', 'followed you', 'has joined your group', 'sent you a private message', 'commented on your picture', 'left the group'];
    let unSeen = true;
    let isActive = true;
    let club = 'Chess Club';
    let message = 'Hello, thanks for setting up the Chess Club. I\'ve been a member for a few weeks now and I\'m already having lots of fun and improving my game.'

    let images = [
        '/images/avatar-mark-webber.webp', '/images/avatar-angela-gray.webp', '/images/avatar-jacob-thompson.webp', '/images/avatar-rizky-hasanuddin.webp', '/images/avatar-kimberly-smith.webp', '/images/avatar-nathan-peterson.webp', '/images/avatar-anna-kim.webp'
];
    
    let details: Detail[] = [
        {'name': 'Mark Webber', 'action': [actions[0]], 'active': isActive, 'time': '1min ago', 'status': unSeen, 'post': 'My First Tournament Today!', 'club': getClub(actions[0])},
        {'name': 'Angela Gray', 'action': [actions[1]], 'active': isActive, 'time': '5min ago', 'status': unSeen, 'club': getClub(actions[1])}, 
        {'name': 'Jacob Thompson', 'action': [actions[2]], 'active': isActive, 'time': '1 day ago', 'status': unSeen, 'club': getClub(actions[2])}, 
        {'name': 'Rizky Hasanuddin', 'action': [actions[3]], 'active': false, 'time': '5 days ago', 'status': false, 'message': message, 'club': getClub(actions[3])}, 
        {'name': 'Kimberly Smith', 'action': [actions[4]], 'active': false, 'time': '1 week ago', 'status': false, 'club': getClub(actions[4])}, 
        {'name': 'Nathan Peterson', 'action': [actions[0]], 'active': false, 'time': '2 weeks ago', 'status': false, 'post': '5 end-game strategies to increase your win rate', 'club': getClub(actions[5])}, 
        {'name': 'Anna Kim', 'action': [actions[5]], 'active': false, 'time': '2 weeks ago', 'status': false, 'club': getClub(actions[6])}
    ];

    $: New = details.filter(detail => detail.status).length;

    function getClub(action: string) {
    return (action === actions[2] || action === actions[6]) ? club : null;
}

const markRead = () => {
    details = details.map(detail => ({...detail, status: false}));
}
</script>

<main>
    <div class="container">
        <div class="heading">
            <section>
                <h2>Notifications</h2>
                <div class="box">{New}</div>
            </section>
            <form>
                <button on:click={markRead}>Mark all as read</button>
            </form>
        </div>
        <div class="notifications">
            {#each details as detail, index}
                <div class="wrapper" class:new = {detail.status}>
                    <img src={images[index]} alt="">
                    <div class="main-deets" >
                        <div class="main-wrap">
                            <p><strong>{detail.name}</strong> {detail.action} 
                                {#if detail.club} 
                                <span class="club">{detail.club}</span>
                                {/if}
                                {#if detail.post}
                                <span class="post">{detail.post}</span>
                                {/if}
                            </p>
                            <div class="circle" class:active-status = {detail.active}></div>
                        </div>
                        <h4>{detail.time}</h4>
                        {#if detail.message}
                            <div class="message">
                                <p>{detail.message}</p>
                            </div>
                        {/if}
                    </div>
                </div>
            {/each}
        </div>
    </div>
</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans&display=swap');
    :global(*){
        margin: 0;
        padding: 0;
        font-family: 'Plus Jakarta Sans', sans-serif;
    }

    main{
        background-color: aliceblue;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .container{
        width: 500px;
        padding: 20px;
        background-color: white;
        border-radius: 10px;
        box-shadow: 5px 5px 5px rgb(187, 187, 187);
    }

    .heading{
        display: flex;
        flex-flow: row nowrap;
        justify-content: space-between;
        align-items: center;
    }

    section{
        display: flex;
        flex-flow: row nowrap;
        align-items: center;
        padding: 10px;
    }

    h2{
        font-size: 20px;
    }

    .box{
        background-color: hsl(219, 85%, 26%);
        color: white;
        width: 25px;
        height: 20px;
        margin-left: 10px;
        text-align: center;
        font-size: 15px;
        border-radius: 2px;
    }

    button{
        background-color: transparent;
        font-size: 12px;
        border: 1px solid transparent;
        color: rgb(156, 156, 156);
        font-weight: 500;
    }

    button:hover{
        color: hsl(219, 12%, 42%);
        font-weight: 500;
    }

    .wrapper{
        padding: 10px;
        margin-bottom: 5px;
        border-radius: 5px;
        display: flex;
        flex-flow: row nowrap;
        align-items: flex-start;
    }

    .new{
        background-color: hsl(210, 100%, 97%);
        transition: background-color 0.1s;
    }

    .new:hover{
        background-color: hsl(205, 33%, 90%);
    }

    .main-deets{
        display: flex;
        flex-flow: column wrap;
        align-items: flex-start;
    }

    p{
        font-size: 12px;
        margin-bottom: 5px;
    }

    h4{
        font-size: 10px;
        color: lightgray;
        font-weight: 300;
    }

    img{
        width: 30px;
        margin-right: 10px;
    }

    .main-wrap{
        display: flex;
        flex-flow: row wrap;
        align-items: center;
    }

    .active-status{
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background-color: hsl(1, 90%, 64%);
        margin-left: 10px;
        transform: translateY(-2px);
    }

    span.club{
        font-weight: 800;
        color:hsl(219, 85%, 26%);
    }

    span.post{
        color: rgb(87, 87, 87);
        font-weight: 600;
        transition: color 0.3s ease;
    }

    span.post:hover{
        color:hsl(219, 85%, 26%)
    }

    .message{
        padding: 10px;
        border: 1px solid hsl(211, 68%, 94%);
        background-color: transparent;
        margin-top: 10px;
        transition: background-color 0.1s;
        border-radius: 5px;
    }

    .message:hover{
        background-color:hsl(211, 68%, 94%);
    }
</style>