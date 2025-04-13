<script>
    import { createEventDispatcher  } from "svelte";
    import Button from "../shared/Button.svelte";

    let dispatch = createEventDispatcher();

    let fields = {
        question: "",
        answerA: "",
        answerB: "",
    };

    let errors = {
        question: '',
        answerA: '',
        answerB: '',
    };

    let valid = false;

    const submitHandler = () => {
        // Handle form submission logic here
       
        valid = true;

        //validate  question
        if (fields.question.trim().length < 5) {
            valid = false;
            errors.question = 'Question must be at least 5 characters long';
        } else {
            errors.question = '';
        }

        //validate  answer A
        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = 'Answer A cannot be empty';
        } else {
            errors.answerA = '';
        }

        //validate  answer B
        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = 'Answer B cannot be empty';
        } else {
            errors.answerB = '';
        }

        const resetForm = () => {
            fields = {
                question: "",
                answerA: "",
                answerB: "",
            };
        };
      

        // Add new poll
        if(valid){
            let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
            dispatch('add', poll);
            resetForm();
            
        }

    };
</script>

<form action="" on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question:</label>
        <input
            type="text"
            id="question"
            bind:value={fields.question}
            placeholder="Enter your question here..."
        />
        {#if errors.question}
            <p class="error">{errors.question}</p>
        {/if}

    </div>

    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" id="answer-a" bind:value={fields.answerA} />
        {#if errors.answerA}
            <p class="error">{errors.answerA}</p>
        {/if}
    </div>

    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" id="answer-b" bind:value={fields.answerB} />
    </div>
    {#if errors.answerB}
        <p class="error">{errors.answerB}</p>
    {/if}

    <Button type="secondary" flat={true}> Add Poll</Button>
    
</form>

<style>
    form {
        width: 400px;
        margin: 0 auto;
        text-align: center;

    }

    .form-field{
        margin: 18px auto;
    }

    input{
        width: 100%;
        border-radius: 6px;
    }

    label{
        margin: 10px auto;
        text-align: left;
    }

    .error {
        color: #d91b42;
        font-size: 0.8em;
        margin-top: 5px;
        font-weight: bold;
    }
</style>
