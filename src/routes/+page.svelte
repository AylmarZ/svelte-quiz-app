<script lang="ts">
	type question = {
		text: string;
		answers: {
			id: number;
			text: string;
			isCorrect: boolean;
		}[];
	};

	let startedQuiz: boolean = $state(false);
	const quiz: question[] = [
		{
			text: 'What is the name of the traditional dance from Bali known for its beautiful hand movements?',
			answers: [
				{
					id: 0,
					text: 'Tari Pendet',
					isCorrect: true
				},
				{
					id: 1,
					text: 'Tari Saman',
					isCorrect: false
				},
				{
					id: 2,
					text: 'Tari Jaipong',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Tari Kekak',
					isCorrect: false
				}
			]
		},
		{
			text: 'Which island is known as the "Island of a Thousand Temples" due to the numerous Hindu temples found there?',
			answers: [
				{
					id: 0,
					text: 'Sumatra',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Bali',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Java',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Kalimantan',
					isCorrect: false
				}
			]
		},
		{
			text: 'Which traditional Indonesian musical instrument is played by striking it with a stick?',
			answers: [
				{
					id: 0,
					text: 'Gamelan',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Kendang',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Tifa',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Kulintang',
					isCorrect: false
				}
			]
		},
		{
			text: 'What is the name of the traditional house from the Batak tribe made of wood with a tall, pointed roof?',
			answers: [
				{
					id: 0,
					text: 'Rumah Gadang',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Rumah Tongkonan',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Rumah Joglo',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Rumah Banjar',
					isCorrect: false
				}
			]
		},
		{
			text: 'Batik is one of Indonesia\'s cultural heritages. From which region does batik with the "Mega Mendung" motif originate?',
			answers: [
				{
					id: 0,
					text: 'Yogyakarta',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Solo',
					isCorrect: false
				},
				{
					id: 2,
					text: 'Pekalongan',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Cirebon',
					isCorrect: true
				}
			]
		},
		{
			text: 'Tari Caci is a traditional dance that originates from which area?',
			answers: [
				{
					id: 0,
					text: 'Bali',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Sumba',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Flores',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Lombok',
					isCorrect: false
				}
			]
		},
		{
			text: 'Which island is known as "Komodo Island" and is home to the rare Komodo dragon?',
			answers: [
				{
					id: 0,
					text: 'Sumatra',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Bali',
					isCorrect: false
				},
				{
					id: 2,
					text: 'Nusa Tenggara',
					isCorrect: true
				},
				{
					id: 3,
					text: 'Papua',
					isCorrect: false
				}
			]
		},
		{
			text: 'In Nusa Tenggara, there is a traditional woven cloth called Tenun Ikat. What makes this fabric unique?',
			answers: [
				{
					id: 0,
					text: 'This cloth is handspun',
					isCorrect: false
				},
				{
					id: 1,
					text: 'This fabric uses yarn that is dyed before being woven',
					isCorrect: true
				},
				{
					id: 2,
					text: 'This cloth is made of bamboo',
					isCorrect: false
				},
				{
					id: 3,
					text: 'This cloth is only found in Bali',
					isCorrect: false
				}
			]
		},
		{
			text: 'What is the name of the traditional ceremony in Bali, where Hindus make offerings to the gods and goddesses?',
			answers: [
				{
					id: 0,
					text: 'Ngaben',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Galungan',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Nyepi',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Melasti',
					isCorrect: false
				}
			]
		},
		{
			text: 'The people of East Nusa Tenggara are known for the Ngaben ceremony. What happens during this ceremony?',
			answers: [
				{
					id: 0,
					text: 'Burial and cremation of the deceased',
					isCorrect: true
				},
				{
					id: 1,
					text: 'Animal sacrifice for offerings',
					isCorrect: false
				},
				{
					id: 2,
					text: 'Celebration of the birth of the first child',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Welcoming the harvest season',
					isCorrect: false
				}
			]
		}
	];
	let questionNumber: number = $state(0);
	let score: number = $state(0);

	let showCorrect: boolean = $state(false);
	let finishedQuiz: boolean = $state(false);

	const handleChooseAnswer = (isCorrect: boolean) => {
		if (showCorrect) return;
		showCorrect = true;
		if (isCorrect) {
			score++;
		}
	};
	const handleNextQuestion = () => {
		if (quiz.length - 1 === questionNumber) {
			return (finishedQuiz = true);
		}
		showCorrect = false;
		questionNumber++;
	};
</script>

<svelte:head>
	<title>Quiz</title>
</svelte:head>

<div class="flex h-screen flex-col items-center justify-center text-center">
	{#if !startedQuiz}
		<h1 class="text-3xl font-bold">Welcome to the quiz</h1>
		<button
			onclick={() => (startedQuiz = true)}
			class="m-2 rounded bg-blue-600 px-4 py-2 text-white transition-colors duration-300 hover:bg-blue-500"
			>Start</button
		>
		<a href="/id" class="text-blue-700">Bahasa Indonesia</a>
	{:else if !finishedQuiz}
		<h1 class="p-4 text-2xl font-bold">{quiz[questionNumber].text}</h1>
		<div class="relative flex w-3/5 flex-col items-center justify-center">
			{#each quiz[questionNumber].answers as answer}
				<button
					onclick={() => handleChooseAnswer(answer.isCorrect)}
					class="m-1.5 w-full cursor-pointer rounded bg-gray-200 p-2 transition-colors duration-300 hover:bg-gray-300 {showCorrect &&
						(answer.isCorrect ? `bg-green-200 hover:bg-green-200` : `bg-red-200 hover:bg-red-200`)}"
				>
					{String.fromCodePoint(answer?.id + 65)}.
					{answer?.text}
				</button>
			{/each}
		</div>
		{#if showCorrect}
			<div class="relative flex w-full justify-center">
				<div class="absolute">
					<button
						onclick={() => handleNextQuestion()}
						class="rounded bg-blue-600 px-3 py-2 text-white transition-colors duration-300 hover:bg-blue-500"
					>
						{quiz.length - 1 === questionNumber ? `Finish` : `Next question`}
					</button>
					<p>Score: {score}</p>
				</div>
			</div>
		{/if}
	{:else}
		<h1 class="text-3xl font-bold">Your final score is: {score} / {quiz.length}</h1>
	{/if}
</div>
