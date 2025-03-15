<script lang="ts">
    import FlashCard from "./lib/FlashCard.svelte";

    // Define flash cards data structure
    const flashCards = [
        // Présent
        { id: 1, question: "je donne", answer: "ik geef" },
        { id: 2, question: "tu donnes", answer: "jij geeft" },
        { id: 3, question: "il/elle donne", answer: "hij/zij geeft" },
        { id: 4, question: "on donne", answer: "wij geven" },
        { id: 5, question: "nous donnons", answer: "wij geven" },
        { id: 6, question: "vous donnez", answer: "jullie geven" },
        { id: 7, question: "ils/elles donnent", answer: "zij geven" },
        {
            id: 8,
            question: "eerste persoon enkelvoud je eindigt op?",
            answer: "e",
        },
        {
            id: 9,
            question: "tweede persoon enkelvoud tu eindigt op?",
            answer: "es",
        },
        {
            id: 10,
            question: "derde persoon enkelvoud il/elle eindigt op?",
            answer: "e",
        },
        {
            id: 11,
            question: "eerste persoon meervoud on eindigt op?",
            answer: "e",
        },
        {
            id: 12,
            question: "eerste persoon meervoud nous eindigt op?",
            answer: "ons",
        },
        {
            id: 13,
            question: "tweede persoon meervoud vous eindigt op?",
            answer: "ez",
        },
        {
            id: 14,
            question: "derde persoon meervoud ils/elles eindigt op?",
            answer: "ent",
        },
        // passé composé
        { id: 15, question: "j'ai regardé", answer: "ik heb gekeken" },
        { id: 16, question: "tu as regardé", answer: "jij hebt gekeken" },
        {
            id: 17,
            question: "il/els a regardé",
            answer: "hij/zij heeft gekeken",
        },
        { id: 18, question: "on a regardé", answer: "wij hebben gekeken" },
        {
            id: 19,
            question: "nous avons regardé",
            answer: "wij hebben gekeken",
        },
        {
            id: 20,
            question: "vous avez regardé",
            answer: "jullie hebben gekeken",
        },
        {
            id: 21,
            question: "ils/elles ont regardé",
            answer: "zij hebben gekekken",
        },
        // aller
        { id: 22, question: "je vais", answer: "ik ga" },
        { id: 23, question: "tu vas", answer: "jij gaat" },
        { id: 24, question: "il/elle va", answer: "hij/zij gaat" },
        { id: 25, question: "on va", answer: "wij gaan" },
        { id: 26, question: "nous allons", answer: "wij gaan" },
        { id: 27, question: "vous allez", answer: "jullie gaan" },
        { id: 28, question: "ils/elles vont", answer: "zij gaan" },
        // avoir
        { id: 29, question: "j'ai", answer: "ik heb" },
        { id: 30, question: "tu as", answer: "jij hebt" },
        { id: 31, question: "il/elle a", answer: "hij/zij heeft" },
        { id: 32, question: "on a", answer: "wij hebben" },
        { id: 33, question: "nous avond", answer: "wij hebben" },
        { id: 34, question: "vous avez", answer: "jullie hebben" },
        { id: 35, question: "ils/elles ont", answer: "zij hebben" },
        // être
        { id: 36, question: "je suis", answer: "ik ben" },
        { id: 37, question: "tu es", answer: "jij bent" },
        { id: 38, question: "il/elle est", answer: "hij/zij is" },
        { id: 39, question: "on est", answer: "wij zijn" },
        { id: 40, question: "nous sommes", answer: "wij zijn" },
        { id: 41, question: "vous êtes", answer: "jullie zijn" },
        { id: 42, question: "ils/elles sont", answer: "zij zijn" },
        // avoir
        { id: 43, question: "je fais", answer: "ik doe" },
        { id: 44, question: "tu fais", answer: "jij doet" },
        { id: 45, question: "il/elle fait", answer: "hij/zij doet" },
        { id: 46, question: "on fait", answer: "wij doen" },
        { id: 47, question: "nous faisons", answer: "wij doen" },
        { id: 48, question: "vous faites", answer: "jullie doen" },
        { id: 49, question: "ils/elles font", answer: "zij doen" },
    ];

    // Create a shuffled version of the flashcards
    let shuffledCards = [];

    // Fisher-Yates shuffle algorithm function
    function shuffleArray(array: any) {
        // Create a copy of the original array to avoid modifying it
        const arrayCopy = [...array];
        // Start from the last element and swap it with a randomly selected element
        for (let i = arrayCopy.length - 1; i > 0; i--) {
            // Pick a random index from 0 to i
            const j = Math.floor(Math.random() * (i + 1));
            // Swap elements at i and j
            [arrayCopy[i], arrayCopy[j]] = [arrayCopy[j], arrayCopy[i]];
        }
        return arrayCopy;
    }

    // Initialize shuffled cards when component loads
    shuffledCards = shuffleArray(flashCards);

    // Keep track of the current card index
    let currentCardIndex = 0;

    // State for tracking points system
    let points = 0;
    let attempted = 0;

    // Function to go to the next card
    // Function to go to the next card
    function nextCard() {
        if (currentCardIndex < shuffledCards.length - 1) {
            currentCardIndex++;
        }
    }

    // Function to go to the previous card
    function prevCard() {
        if (currentCardIndex > 0) {
            currentCardIndex--;
        }
    }
    // Function to update points when an answer is submitted
    function handleAnswerSubmit(event: any) {
        const isCorrect = event.detail.isCorrect;
        attempted++;

        if (isCorrect) {
            points++; // Add 1 point for correct answer

            // Set a 2-second delay for correct answers before moving to the next card
            if (currentCardIndex < shuffledCards.length - 1) {
                setTimeout(() => {
                    nextCard();
                }, 2000);
            }
        } else {
            // No point deduction for incorrect answers

            // Set a 5-second delay for incorrect answers before moving to the next card
            if (currentCardIndex < shuffledCards.length - 1) {
                setTimeout(() => {
                    nextCard();
                }, 5000);
            }
        }
    }
</script>

<main>
    <div class="container">
        <h1>Frans grammatica</h1>

        <div class="score-container">
            <p>Points: {points} (Attempted: {attempted})</p>
        </div>

        <div class="card-container">
            <FlashCard
                flashCard={shuffledCards[currentCardIndex]}
                on:answerSubmitted={handleAnswerSubmit}
            />
        </div>

        <div class="navigation">
            <button on:click={prevCard} disabled={currentCardIndex === 0}
                >Previous</button
            >
            <span class="card-counter"
                >{currentCardIndex + 1} / {shuffledCards.length}</span
            >
            <button
                on:click={nextCard}
                disabled={currentCardIndex === shuffledCards.length - 1}
                >Next</button
            >
        </div>
    </div>
</main>

<style>
    :global(body) {
        background-color: #10abb4;
        color: #004c50;
        margin: 0;
        padding: 0;
        font-family:
            -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans,
            Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
    }

    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
        background-color: white;
        border-radius: 12px;
        box-shadow: 0 4px 12px rgba(0, 76, 80, 0.1);
    }

    h1 {
        color: #004c50;
        margin-bottom: 20px;
        font-weight: 700;
        text-align: center;
    }

    .score-container {
        margin-bottom: 20px;
        font-size: 1.2rem;
        font-weight: bold;
        color: #004c50;
        background-color: rgba(16, 171, 180, 0.1);
        padding: 8px 16px;
        border-radius: 8px;
    }

    .card-container {
        width: 100%;
        margin-bottom: 20px;
    }

    .navigation {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        max-width: 400px;
        padding: 10px;
        background-color: rgba(0, 147, 156, 0.05);
        border-radius: 8px;
    }

    button {
        background-color: #00939c;
        color: white;
        border: none;
        padding: 10px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 4px 2px;
        cursor: pointer;
        border-radius: 4px;
        transition: all 0.3s ease;
        font-weight: 500;
        box-shadow: 0 2px 4px rgba(0, 76, 80, 0.2);
    }

    button:hover {
        background-color: #10abb4;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 76, 80, 0.3);
    }

    button:disabled {
        background-color: rgba(0, 147, 156, 0.3);
        cursor: not-allowed;
        box-shadow: none;
        transform: none;
    }

    .card-counter {
        font-size: 1rem;
        color: #502000;
        font-weight: 600;
        background-color: rgba(156, 62, 0, 0.1);
        padding: 4px 10px;
        border-radius: 4px;
    }
</style>
