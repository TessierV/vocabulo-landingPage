<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/environment';

    // Array of question objects
    export let questions = [
        { id: 1, title: "Question 1", answer: "Réponse à la question 1", isOpen: false },
        { id: 2, title: "Question 2", answer: "Réponse à la question 2", isOpen: false },
        { id: 3, title: "Question 3", answer: "Réponse à la question 3", isOpen: false },
        { id: 4, title: "Question 4", answer: "Réponse à la question 4", isOpen: false },
        { id: 5, title: "Question 5", answer: "Réponse à la question 5", isOpen: false },
    ];

    // Function to toggle the answer visibility
    const toggleAnswer = (id) => {
        questions = questions.map(q => q.id === id ? { ...q, isOpen: !q.isOpen } : q);
    };

    let gsap;
    let ScrollTrigger;

    // onMount lifecycle function
    onMount(async () => {
        if (browser) {
            // Dynamically import GSAP and ScrollTrigger
            gsap = (await import('gsap')).default;
            ScrollTrigger = (await import('gsap/ScrollTrigger')).default;
            gsap.registerPlugin(ScrollTrigger);

            const questionElements = document.querySelectorAll('.question');

            // Set initial state of question elements
            gsap.set(questionElements, { autoAlpha: 0, y: 50 });

            // Animate each question element
            questionElements.forEach((question, index) => {
                gsap.to(question, {
                    duration: 0.5,
                    autoAlpha: 1,
                    y: 0,
                    scrollTrigger: {
                        trigger: question,
                        start: "top 80%",
                        end: "bottom 20%",
                        toggleActions: "play none none reverse"
                    },
                    delay: index * 0.1
                });
            });
        }
    });
</script>

<!-- FAQ Section -->
<section class="w-full sm:w-5/6 mx-auto px-5 py-20">
    <h2 class="text-3xl uppercase font-bold mb-6">Questions Fréquentes</h2>
    <div class="questions-container py-20">
        {#each questions as question (question.id)}
            <div class="question mb-4 bg-gray-100 rounded-lg">
                <button
                    class="w-full p-4 text-left flex justify-between items-center focus:outline-none"
                    on:click={() => toggleAnswer(question.id)}
                    aria-expanded={question.isOpen}
                    aria-controls="answer-{question.id}"
                >
                    <h3 class="text-lg font-semibold">{question.title}</h3>
                    <svg class="w-6 h-6 transition-transform duration-300 {question.isOpen ? 'transform rotate-180' : ''}" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                </button>
                {#if question.isOpen}
                    <div id="answer-{question.id}" class="p-4 border-t border-gray-200">
                        <p class="text-gray-700">{question.answer}</p>
                    </div>
                {/if}
            </div>
        {/each}
    </div>
</section>

<style>
    .question {
        transition: all 0.3s ease;
    }

    .question:hover {
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    .question button:focus {
        outline: none;
    }

    .question button:focus-visible {
        outline: 1px solid #212937;
        outline-offset: 2px;
    }
</style>
