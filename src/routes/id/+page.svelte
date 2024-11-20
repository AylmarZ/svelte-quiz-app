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
			text: 'Apa nama tarian tradisional yang berasal dari Bali yang terkenal dengan gerakan tangan yang indah?',
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
			text: 'Pulau apa yang dikenal sebagai "Pulau Seribu Pura" karena banyaknya pura Hindu di sana?',
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
					text: 'Jawa',
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
			text: 'Alat musik tradisional Indonesia yang dimainkan dengan cara dipukul menggunakan stik adalah?',
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
			text: 'Rumah adat dari suku Batak yang terbuat dari kayu dan berbentuk atap yang menjulang tinggi disebut?',
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
			text: 'Batik adalah warisan budaya Indonesia. Dari daerah mana asal batik dengan motif "Mega Mendung"?',
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
			text: 'Tari Caci adalah tarian tradisional yang berasal dari daerah mana?',
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
			text: 'Pulau apa yang dikenal dengan nama "Pulau Komodo" yang merupakan rumah bagi hewan komodo yang langka?',
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
			text: 'Di Nusa Tenggara, terdapat kain tenun tradisional yang disebut Tenun Ikat. Apa yang membedakan kain tenun ikat ini?',
			answers: [
				{
					id: 0,
					text: 'Kain ini dipintal dengan tangan',
					isCorrect: false
				},
				{
					id: 1,
					text: 'Kain ini menggunakan benang yang sudah diberi warna terlebih dahulu sebelum ditenun',
					isCorrect: true
				},
				{
					id: 2,
					text: 'Kain ini terbuat dari bambu',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Kain ini hanya ditemukan di Bali',
					isCorrect: false
				}
			]
		},
		{
			text: 'Apa nama upacara adat yang terkenal di Bali, di mana umat Hindu melakukan persembahan kepada dewa-dewi?',
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
			text: 'Masyarakat Nusa Tenggara Timur terkenal dengan tradisi Upacara Ngaben. Apa yang dilakukan dalam upacara ini?',
			answers: [
				{
					id: 0,
					text: 'Pemakaman dan pembakaran jenazah',
					isCorrect: true
				},
				{
					id: 1,
					text: 'Penyembelihan hewan untuk korban',
					isCorrect: false
				},
				{
					id: 2,
					text: 'Perayaan kelahiran anak pertama',
					isCorrect: false
				},
				{
					id: 3,
					text: 'Penyambutan musim panen',
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
		<h1 class="text-3xl font-bold">Selamat datang di kuis</h1>
		<button
			onclick={() => (startedQuiz = true)}
			class="m-2 rounded bg-blue-600 px-4 py-2 text-white transition-colors duration-300 hover:bg-blue-500"
			>Mulai</button
		>
		<a href="/" class="text-blue-700">English</a>
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
						{quiz.length - 1 === questionNumber ? `Selesai` : `Pertanyaan berikutnya`}
					</button>
					<p>Skor: {score}</p>
				</div>
			</div>
		{/if}
	{:else}
		<h1 class="text-3xl font-bold">Skor akhir: {score} / {quiz.length}</h1>
	{/if}
</div>
