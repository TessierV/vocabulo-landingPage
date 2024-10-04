<script>
    import { onMount } from "svelte";
    import { browser } from "$app/environment";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { isQuizMode } from "./quizStore.js";

    gsap.registerPlugin(ScrollTrigger);

    let sectionElement;
    let cardElements = [];
    let featureText1, featureText2, featureDescription;
    let bgImage1, bgImage2;

    // Reactive statement to define cards based on quiz mode
    $: cards = [
        {
            id: 1,
            title: $isQuizMode ? "Personnalisé" : "Appareil photo",
            subtitle: $isQuizMode
                ? "Apprentissage personnalisé"
                : "Appareil photo intégré",
            description: $isQuizMode
                ? "Le système analyse ton parcours d'apprentissage pour adapter les questions à ton niveau."
                : "Utilisation de l'appreil photo directement dans l'application, en mode portrait ou paysage.",
            color: "red",
            bgImage: $isQuizMode
                ? "assets/features/phone1.png"
                : "assets/features/phone1Kid.png",
            icon: `<svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M19.2101 15.74L15.67 19.2801C15.53 19.4201 15.4 19.68 15.37 19.87L15.18 21.22C15.11 21.71 15.45 22.05 15.94 21.98L17.29 21.79C17.48 21.76 17.75 21.63 17.88 21.49L21.42 17.95C22.03 17.34 22.32 16.63 21.42 15.73C20.53 14.84 19.8201 15.13 19.2101 15.74Z" stroke="#FFF" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12.1601 10.87C12.0601 10.86 11.9401 10.86 11.8301 10.87C9.45006 10.79 7.56006 8.84 7.56006 6.44C7.56006 3.99 9.54006 2 12.0001 2C14.4501 2 16.4401 3.99 16.4401 6.44C16.4301 8.84 14.5401 10.79 12.1601 10.87Z" stroke="#FFF" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12 21.8101C10.18 21.8101 8.37005 21.3501 6.99005 20.4301C4.57005 18.8101 4.57005 16.1701 6.99005 14.5601C9.74005 12.7201 14.25 12.7201 17 14.5601" stroke="#FFF" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`,
        },
        {
            id: 2,
            title: $isQuizMode ? "Recommandations" : "Utilisation simple",
            subtitle: $isQuizMode
                ? "Recommandations contextuelles"
                : "Capture du texte guidée",
            description: $isQuizMode
                ? "Les questions proposées changent selon le moment de la journée, la semaine, et la saison."
                : "Un cadre guide l'enfant pour l'utilisation de l'appareil photo sur le texte du livre",
            color: "green",
            icon: `<svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 18.5C15.5899 18.5 18.5 15.5899 18.5 12C18.5 8.41015 15.5899 5.5 12 5.5C8.41015 5.5 5.5 8.41015 5.5 12C5.5 15.5899 8.41015 18.5 12 18.5Z" stroke="#FFF" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M19.14 19.14L19.01 19.01M19.01 4.99L19.14 4.86L19.01 4.99ZM4.86 19.14L4.99 19.01L4.86 19.14ZM12 2.08V2V2.08ZM12 22V21.92V22ZM2.08 12H2H2.08ZM22 12H21.92H22ZM4.99 4.99L4.86 4.86L4.99 4.99Z" stroke="#FFF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`,
        },
        {
            id: 3,
            title: $isQuizMode ? "Équilibre" : "Catégories Grammaticales",
            subtitle: $isQuizMode
                ? "Équilibre de difficulté"
                : "Code couleur",
            description: $isQuizMode
                ? "Chaque question est choisie pour être suffisamment stimulante, sans être trop difficile."
                : "Chaque catégorie grammaticale est associée avec une couleur, la légende est disponible d'un simple clic.",
            color: "red",
            bgImage: $isQuizMode
                ? "assets/features/phone2.png"
                : "assets/features/phone2Kid.png",
            icon: `<svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M2 2V19C2 20.66 3.34 22 5 22H22" stroke="#FFF" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M5 17L9.59 11.64C10.35 10.76 11.7 10.7 12.52 11.53L13.47 12.48C14.29 13.3 15.64 13.25 16.4 12.37L21 7" stroke="#FFF" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`,
        },
        {
            id: 4,
            title: $isQuizMode ? "Révision" : "Personnalisation",
            subtitle: $isQuizMode
                ? "Questions nouvelles et révision"
                : "Chacun son dictionnaire",
            description: $isQuizMode
                ? "Le quiz introduit des questions nouvelles tout en renforçant celles que tu as déjà apprises."
                : "Chaque enfant peut stocker les cartes des mots qu'il a déjà rencontré dans son dictionnaire pour y revenir plus tard.",
            color: "green",
            icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" /></svg>`,
        },
        {
            id: 5,
            title: $isQuizMode ? "Feedback" : "Accessibilité",
            subtitle: $isQuizMode
                ? "Feedback en temps réel"
                : "Clavier en LSF",
            description: $isQuizMode
                ? "Tes retours aident à affiner les recommandations futures pour les questions."
                : "Possiblité de chercher les mots directement en utilisant un clavier en LSF.",
            color: "red",
            bgImage: $isQuizMode
                ? "assets/features/phone3.png"
                : "assets/features/phone3Kid.png",
            icon: `<svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M7.48 18.35L10.58 20.75C10.98 21.15 11.88 21.35 12.48 21.35H16.28C17.48 21.35 18.78 20.45 19.08 19.25L21.48 11.95C21.98 10.55 21.08 9.35003 19.58 9.35003H15.58C14.98 9.35003 14.48 8.85003 14.58 8.15003L15.08 4.95003C15.28 4.05003 14.68 3.05003 13.78 2.75003C12.98 2.45003 11.98 2.85003 11.58 3.45003L7.48 9.55003" stroke="#FFF" stroke-width="1.5" stroke-miterlimit="10"/>
            <path d="M2.38 18.35V8.55002C2.38 7.15002 2.98 6.65002 4.38 6.65002H5.38C6.78 6.65002 7.38 7.15002 7.38 8.55002V18.35C7.38 19.75 6.78 20.25 5.38 20.25H4.38C2.98 20.25 2.38 19.75 2.38 18.35Z" stroke="#FFF" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`,
        },
        {
            id: 6,
            title: $isQuizMode ? "Optimisation" : "Analyse grammaticale",
            subtitle: $isQuizMode
                ? "Optimisation continue"
                : "Connaissance linguistique",
            description: $isQuizMode
                ? "Le système est régulièrement amélioré pour mieux suivre tes progrès dans les quiz et te faire progresser."
                : "L'implémentation des informations grammaticale encourage l'enfant à percer la conception des phrases en français écrit.",
            color: "green",
            icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>`,
        },
    ];

    // Reactive statements to set images and texts based on quiz mode
    $: quizImage1 = $isQuizMode
        ? "/assets/features/titleQuiz.png"
        : "/assets/features/pictureKid.png";

    $: quizImage2 = $isQuizMode
        ? "/assets/features/pictureQuiz.png"
        : "/assets/features/titleKid.png";

    $: boxTitle1 = $isQuizMode
        ? "Découvrez le Quiz Hybride,"
        : "Reconnaissance de caractères";
    $: boxTitle2 = $isQuizMode
        ? "conçu pour enrichir votre vocabulaire."
        : "Traitement Automatique du Langage Naturel";
    $: boxDescription = $isQuizMode
        ? "Le Quiz Hybride utilise des techniques d'intelligence artificielle pour personnaliser chaque session. Le système ajuste les questions ou mots en fonction de votre progression. Grâce à des recommandations contextuelles et un équilibre de difficulté, vous êtes constamment stimulé sans être surchargé. Le quiz introduit de nouveaux contenus tout en renforçant ceux déjà appris, et votre feedback améliore en continu les recommandations futures."
        : "Après avoir identifié les caractères dans l'image et reconstitué les mots, le modèle va analyser chacun pour déterminer la meilleure définition présente dans le dictionnaire de signes, tentant d'éviter les soucis de polysémie du français.";

    // Function to handle interaction start (mouse over or focus)
    function handleInteractionStart(event) {
        gsap.to(event.currentTarget, { scale: 0.95, duration: 0.3 });
    }

    // Function to handle interaction end (mouse leave or blur)
    function handleInteractionEnd(event) {
        gsap.to(event.currentTarget, { scale: 1, duration: 0.3 });
    }

    // Function to handle keydown events for accessibility
    function handleKeyDown(event) {
        if (event.key === "Enter" || event.key === " ") {
            event.preventDefault();
            console.log(
                "Card activated:",
                event.currentTarget.querySelector("h3").textContent,
            );
        }
    }

    // Set up animations when component mounts
    onMount(() => {
        if (browser) {
            cardElements.forEach((card, index) => {
                gsap.fromTo(
                    card,
                    { y: 100, opacity: 0 },
                    {
                        y: 0,
                        opacity: 1,
                        duration: 0.5,
                        scrollTrigger: {
                            trigger: card,
                            start: "top bottom-=50",
                            end: "top center",
                            toggleActions: "play reverse play reverse",
                            scrub: true,
                        },
                    },
                );
            });

            gsap.fromTo(
                featureText1,
                { x: -100, opacity: 0 },
                {
                    x: 0,
                    opacity: 1,
                    duration: 1,
                    scrollTrigger: {
                        trigger: featureText1,
                        start: "top bottom",
                        end: "center center",
                        toggleActions: "play reverse play reverse",
                        scrub: true,
                    },
                },
            );

            gsap.fromTo(
                featureText2,
                { x: 100, opacity: 0 },
                {
                    x: 0,
                    opacity: 1,
                    duration: 1,
                    scrollTrigger: {
                        trigger: featureText2,
                        start: "top bottom",
                        end: "center center",
                        toggleActions: "play reverse play reverse",
                        scrub: true,
                    },
                },
            );

            gsap.fromTo(
                featureDescription,
                { y: 100, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1,
                    scrollTrigger: {
                        trigger: featureDescription,
                        start: "top bottom",
                        end: "center center",
                        toggleActions: "play reverse play reverse",
                        scrub: true,
                    },
                },
            );
        }
    });
</script>

<section
    bind:this={sectionElement}
    style="border-radius: 42px"
    class="py-20 bg-gray-100"
>
    <div class="container mx-auto w-full sm:w-5/6 px-4">
        <h2 class="text-4xl font-bold text-center mb-12">Hybride Quiz</h2>
        <!-- Section -->
        <div class="w-full sm:w-5/6 text-center mx-auto mt-20">
            <div
                bind:this={featureText1}
                class="feature-text-1 gap-8 mb-2 items-center justify-center flex text-black relative"
            >
                <div
                    bind:this={bgImage1}
                    class="bg-image"
                    style="background-image: url({quizImage1});"
                ></div>
                <h1 class="text-4xl font-bold text-left relative z-10">
                    {boxTitle1}
                </h1>
            </div>
            <!-- Feature text 2 with background image -->
            <div
                bind:this={featureText2}
                class="feature-text-2 gap-8 flex items-center justify-center text-black relative"
            >
                <h1 class="text-4xl text-right font-bold relative z-10">
                    {boxTitle2}
                </h1>
                <div
                    bind:this={bgImage2}
                    class="bg-image"
                    style="background-image: url({quizImage2});"
                ></div>
            </div>
            <!-- Feature description -->
            <div
                bind:this={featureDescription}
                class="feature-description text-black p-10"
            >
                <p>{boxDescription}</p>
            </div>
        </div>

        <!-- Grid of feature cards -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 py-20">
            {#each cards as card (card.id)}
                <div
                    bind:this={cardElements[card.id - 1]}
                    class="group card text-white rounded-lg justify-between p-2 transform transition-all duration-300 flex flex-col cursor-pointer"
                    style={card.color === "red"
                        ? `background-image: url(${card.bgImage}); background-size: cover; background-position: center;`
                        : "background-color: #212937;"}
                    on:mouseover={handleInteractionStart}
                    on:mouseleave={handleInteractionEnd}
                    on:focus={handleInteractionStart}
                    on:blur={handleInteractionEnd}
                    on:keydown={handleKeyDown}
                    role="button"
                    tabindex="0"
                >
                    <!-- Card content -->
                    <div class="flex items-center justify-end mb-4">
                        <div class="text-12px flex-shrink-0 bg-black">
                            <div class="flex items-center justify-center">
                                {@html card.icon}
                            </div>
                        </div>
                        <p class="px-5 text-12px bg-black">{card.title}</p>
                    </div>
                    <div class="p-5">
                        <p
                            class={`font-semibold mb-2 ${card.color === "red" ? "opacity-0 group-hover:opacity-100 focus-within:opacity-100 transition-opacity duration-300" : "block"}`}
                        >
                            {card.subtitle}
                        </p>
                        <p
                            style="font-size: 12px"
                            class={card.color === "red"
                                ? "opacity-0 group-hover:opacity-100 focus-within:opacity-100 transition-opacity duration-300"
                                : "block"}
                        >
                            {card.description}
                        </p>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .card {
        min-height: 200px;
    }

    :global(.card) {
        transition: transform 0.3s ease-in-out;
    }

    :global(.card:hover) {
        transform: translateY(-5px);
    }

    /* Improve text readability on background image */
    :global(.card[style*="background-image"]) {
        text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.8);
    }

    /* Apply before effect only on hover or focus */
    :global(.card:hover[style*="background-image"]::before),
    :global(.card:focus-within[style*="background-image"]::before) {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.6);
        border-radius: 0.5rem;
        z-index: 1;
    }

    /* Apply internal card elements when before effect is active */
    :global(.card:hover[style*="background-image"] > *),
    :global(.card:focus-within[style*="background-image"] > *) {
        position: relative;
        z-index: 2;
    }

    :global(.card[style*="background-image"] > *) {
        position: relative;
        z-index: 2;
    }

    :global(.card svg) {
        width: 12px;
        height: 12px;
    }

    .text-12px {
        font-size: 12px;
        min-height: 30px;
        min-width: 30px;
        line-height: 1;
        align-items: center;
        align-content: center;
        border-radius: 25px;
    }

    .feature-text-1,
    .feature-text-2 {
        position: relative;
    }

    .bg-image {
        width: 120px;
        height: 50px;
        border-radius: 50px;
        background-size: cover;
        background-position: center;
        position: relative;
        overflow: hidden;
    }

    .bg-image::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: inherit;
        background-size: cover;
        background-position: center;
        background-attachment: local;
    }
</style>
