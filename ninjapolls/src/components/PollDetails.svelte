<script>
    import { createEventDispatcher } from "svelte";
    import Card from "../shared/Card.svelte";
    export let poll;

    const dispatch = createEventDispatcher();

    //reactive values
    $: totalVotes = poll.votesA + poll.votesB;

    $: percentA = Math.floor(100/totalVotes * poll.votesA);
    $: percentB = Math.floor(100/totalVotes * poll.votesB);

    const handleVote = (option, id) => {
        dispatch('vote', {
            option,
            id
        });
    }
</script>

<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total votes: {totalVotes}</p>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="answer" on:click={() => handleVote('a', poll.id)}>
            <div class="percent percent-a" style="width: { percentA }%;"></div>
            <span>{poll.answerA} ({poll.votesA})</span>
        </div>
    </div>
    
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => handleVote('b', poll.id)}>
        <div class="percent percent-b" style="width: { percentB }%;"></div>
        <span>{poll.answerB} ({poll.votesB})</span>
    </div>
</Card>

<style>
    h3 {
        margin: 0 auto;
        color: #555;
    }

    p {
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 30px;
    }

    .answer {
        background: #fafafa;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }

    .answer:hover {
        opacity: 0.6;
    }

    span {
        display: inline-block;
        padding: 10px 20px;
    }

    .percent {
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 0;
        transition: width 0.5s ease-in-out;
        box-sizing: border-box;
    }

    .percent-a{
        border-left: 4px solid #d91b42;
        background: rgba(217, 27, 66, 0.2);
       
    }

    .percent-b{
        border-left: 4px solid #45c496;
        background: rgba(69, 196, 150, 0.2);
        
    }
</style>
