<script>
	import Header from "./components/Header.svelte";
	import Footer from "./components/Footer.svelte";

	import CreatePollForm from "./components/CreatePollForm.svelte";
	import PollList from "./components/PollList.svelte";
	import Tabs from "./shared/Tabs.svelte";
	
	// tabs
	let items = ["Current Polls", "Add New Poll"];
	let activeItem = "Current Polls";

	const tabChange = (event) => {
		activeItem = event.detail;
	};

	//polls

	let polls = [
		{
			id: 1,
			question: "Do you like Svelte?",
			answerA: "Yes",
			answerB: "No",
			votesA: 10,
			votesB: 5,
		},
		{
			id: 2,
			question: "Do you like React?",
			answerA: "Yes",
			answerB: "No",
			votesA: 8,
			votesB: 12,
		},
	];

	const handleAdd = (event) => {
		const poll = event.detail;
		polls = [...polls, poll];

		console.log(polls);

		activeItem = "Current Polls";
	};

	const handleVote = (event) => {
		const { id, option } = event.detail;
		let copiedPolls = [...polls];

		const upvotedPoll = copiedPolls.find((poll) => poll.id === id);

		if (option === "a") {
			upvotedPoll.votesA++;
		}

		if (option === "b") {
			upvotedPoll.votesB++;
		}

		polls = copiedPolls;
	};
</script>

<Header />
<main>
	<Tabs {activeItem} {items} on:tabChange={tabChange} />

	{#if activeItem === "Current Polls"}
		<PollList {polls} on:vote={handleVote} />
	{:else if activeItem === "Add New Poll"}
		<CreatePollForm on:add={handleAdd} />
	{/if}
</main>

<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>
