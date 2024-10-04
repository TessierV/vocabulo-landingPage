<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { isQuizMode } from "./quizStore.js";

    // Register ScrollTrigger plugin
    gsap.registerPlugin(ScrollTrigger);

    let infoSection2;
    let bentoItems;
    let switchButton;
    let switchLogo;
    let aboutDescription;

    // Reactive statements for content based on quiz mode
    $: buttonText = $isQuizMode ? "Changer pour Enfant" : "Changer pour Quiz";
    $: logoIcon = $isQuizMode
        ? "/assets/category/logoQuiz.png"
        : "/assets/category/logoKid.png";

    $: boxDescription = $isQuizMode
        ? "Découvrez les fonctionnalités qui rendent notre application incontournable. Grâce à des outils simples et intuitifs, vous pouvez apprendre à votre rythme, découvrir de nouveaux mots, et améliorer votre vocabulaire. Chaque fonctionnalité est pensée pour vous offrir une expérience pratique, adaptée à vos besoins et facile à utiliser au quotidien."
        : "Découvrez les fonctionnalités qui vont rendre la littérature jeunesse accessible et ouvrir un monde d'histoires aux enfants sourds. Grâce à utilisation simple et intuitive, les textes deviennent augmentés de leur signe en LSF, leur définition. Sans compter la mise en avant des catégories et fonctions grammaticales. N'ayez plus peur du français écrit.";

    // Reactive background images
    $: bgImage1 = $isQuizMode ? "" : "";
    $: bgImage2 = $isQuizMode
        ? "assets/bento/4Quiz.png"
        : "assets/bento/4Quiz.png";
    $: bgImage3 = $isQuizMode
        ? "assets/bento/3Quiz.png"
        : "assets/bento/3Quiz.png";
    $: bgImage5 = $isQuizMode
        ? "assets/bento/5Quiz.png"
        : "assets/bento/5Quiz.png";

    // Reactive SVG icons
    $: icon1 = $isQuizMode
        ? `<svg xmlns="http://www.w3.org/2000/svg" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" width="18" height="18" x="0" y="0" viewBox="0 0 96 96" style="enable-background:new 0 0 512 512" xml:space="preserve" class=""><g><path fill="#efcbbd" d="m43.295 62.332-12.566-8.814a6.388 6.388 0 1 0-7.634 10.244s3.601 3.115 5.048 4.91c5.644 7 19.801 23.42 38.218 14.886 6.271-2.906 11.431-6.857 13.739-12.871 2.309-6.014 2.403-12.937-.41-19.246L71.6 33.696l-.454-.999-5.475-12.28a5.32 5.32 0 0 0-9.716 4.332l7.449 17.221-11.513-25.825a5.021 5.021 0 0 0-6.631-2.541l-.544.243a5.021 5.021 0 0 0-2.541 6.631L52.71 44.064 39.576 14.607a5.021 5.021 0 0 0-6.631-2.541l-.544.243a5.021 5.021 0 0 0-2.541 6.631l2.416 5.418 10.293 22.891-9.491-21.289a5.021 5.021 0 0 0-6.631-2.541l-.544.243a5.021 5.021 0 0 0-2.541 6.631l11.737 26.324z" opacity="0" data-original="#efcbbd" class=""></path><path fill="#ffffff" d="M55.944 87.884c-4.834 0-9.67-1.434-14.465-4.301-6.456-3.859-11.315-9.354-14.827-13.71-1.079-1.338-3.755-3.748-4.762-4.622a8.248 8.248 0 0 1-3.194-5.413 8.245 8.245 0 0 1 1.559-6.16c2.428-3.259 6.808-4.224 10.329-2.486l-8.97-20.119a6.945 6.945 0 0 1 3.511-9.16l.545-.243a6.846 6.846 0 0 1 3.045-.602l-.602-1.35a6.945 6.945 0 0 1 3.51-9.16l.545-.243c3.493-1.557 7.602.017 9.159 3.51l.086.193a6.89 6.89 0 0 1 2.525-1.923l.545-.243c3.493-1.557 7.602.017 9.159 3.51l1.323 2.966a7.19 7.19 0 0 1 2.905-2.355c1.765-.787 3.731-.839 5.535-.148s3.231 2.044 4.018 3.809l5.923 13.267 8.088 17.741c2.917 6.542 3.077 13.898.456 20.726-2.231 5.812-7.047 10.366-14.722 13.922-3.728 1.731-7.475 2.594-11.224 2.594zm-29.04-33.709a4.449 4.449 0 0 0-3.579 1.792c-.714.958-1.012 2.136-.839 3.318s.795 2.226 1.753 2.94c.037.027.074.057.109.087.152.132 3.749 3.25 5.286 5.157 4.5 5.581 18.192 22.565 35.922 14.35 6.727-3.117 10.9-6.983 12.757-11.82 2.254-5.872 2.122-12.187-.371-17.779l-8.538-18.731-5.481-12.292c-.37-.83-1.041-1.467-1.89-1.792s-1.774-.3-2.605.07a3.407 3.407 0 0 0-1.722 4.495l7.458 17.24a1.916 1.916 0 0 1-3.506 1.54L50.142 16.925a3.11 3.11 0 0 0-4.102-1.572l-.545.243a3.113 3.113 0 0 0-1.688 3.802l10.651 23.888a1.916 1.916 0 0 1-3.498 1.561l-.006-.013-10.528-23.576a7.309 7.309 0 0 1-.181-.446l-2.419-5.425a3.11 3.11 0 0 0-4.101-1.572l-.545.243a3.11 3.11 0 0 0-1.572 4.101l2.722 6.1c.186.292.352.599.496.921l9.491 21.288a1.915 1.915 0 0 1-3.496 1.565l-9.844-21.892a3.077 3.077 0 0 0-1.375-1.037 3.093 3.093 0 0 0-2.376.064l-.545.243a3.11 3.11 0 0 0-1.572 4.101L36.61 55.305l7.784 5.459a1.915 1.915 0 0 1-2.195 3.139l-8.196-5.715a1.923 1.923 0 0 1-.254-.213l-4.121-2.89a4.544 4.544 0 0 0-2.724-.91z" opacity="1" data-original="#16191e" class=""></path><path fill="#768dff" d="M77.944 10.031a45.419 45.419 0 0 1 12.14 17.178" opacity="1" data-original="#768dff" class=""></path><path fill="#ffffff" d="M90.085 29.125c-.76 0-1.479-.455-1.779-1.204a43.684 43.684 0 0 0-11.629-16.453 1.915 1.915 0 1 1 2.532-2.874 47.538 47.538 0 0 1 12.652 17.903 1.915 1.915 0 0 1-1.776 2.628z" opacity="1" data-original="#16191e" class=""></path><path fill="#768dff" d="M6.601 50.791a45.102 45.102 0 0 1 2.101-23.506" opacity="1" data-original="#768dff" class=""></path><path fill="#ffffff" d="M6.599 52.706a1.916 1.916 0 0 1-1.884-1.584 47.209 47.209 0 0 1 2.19-24.501 1.915 1.915 0 1 1 3.593 1.327 43.377 43.377 0 0 0-2.011 22.511 1.915 1.915 0 0 1-1.888 2.247z" opacity="1" data-original="#16191e" class=""></path></g></svg>`
        : `<svg>...</svg>`; // Remplace
    $: icon2 = $isQuizMode
        ? `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M22 4.66994V16.74C22 17.7 21.22 18.5999 20.26 18.7199L19.93 18.76C17.75 19.05 14.39 20.1599 12.47 21.2199C12.21 21.3699 11.78 21.3699 11.51 21.2199L11.47 21.2C9.54997 20.15 6.20003 19.05 4.03003 18.76L3.73999 18.7199C2.77999 18.5999 2 17.7 2 16.74V4.65993C2 3.46993 2.96997 2.56994 4.15997 2.66994C6.25997 2.83994 9.43997 3.89997 11.22 5.00997L11.47 5.15993C11.76 5.33994 12.24 5.33994 12.53 5.15993L12.7 5.04995C13.33 4.65995 14.13 4.26994 15 3.91994V7.99996L17 6.66994L19 7.99996V2.77999C19.27 2.72999 19.53 2.69995 19.77 2.67995H19.83C21.02 2.57995 22 3.46994 22 4.66994Z" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12 5.48999V20.49" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M19 2.78003V8L17 6.66998L15 8V3.91998C16.31 3.39998 17.77 2.98003 19 2.78003Z" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`
        : `<svg>...</svg>`;
    $: icon3 = $isQuizMode
        ? `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M2.03009 12.42C2.39009 17.57 6.76009 21.76 11.9901 21.99C15.6801 22.15 18.9801 20.43 20.9601 17.72C21.7801 16.61 21.3401 15.87 19.9701 16.12C19.3001 16.24 18.6101 16.29 17.8901 16.26C13.0001 16.06 9.00009 11.97 8.98009 7.13996C8.97009 5.83996 9.24009 4.60996 9.73009 3.48996C10.2701 2.24996 9.62009 1.65996 8.37009 2.18996C4.41009 3.85996 1.70009 7.84996 2.03009 12.42Z" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`
        : `<svg>...</svg>`;
    $: icon4 = $isQuizMode
        ? `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M22 12C22 17.52 17.52 22 12 22C6.48 22 3.11 16.44 3.11 16.44M3.11 16.44H7.63M3.11 16.44V21.44M2 12C2 6.48 6.44 2 12 2C18.67 2 22 7.56 22 7.56M22 7.56V2.56M22 7.56H17.56" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`
        : `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M22 12C22 17.52 17.52 22 12 22C6.48 22 3.11 16.44 3.11 16.44M3.11 16.44H7.63M3.11 16.44V21.44M2 12C2 6.48 6.44 2 12 2C18.67 2 22 7.56 22 7.56M22 7.56V2.56M22 7.56H17.56" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            `;
    $: icon5 = $isQuizMode
        ? `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M8 2V5" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M16 2V5" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7 13H15" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7 17H12" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M16 3.5C19.33 3.68 21 4.95 21 9.65V15.83C21 19.95 20 22.01 15 22.01H9C4 22.01 3 19.95 3 15.83V9.65C3 4.95 4.67 3.69 8 3.5H16Z" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            `
        : `<svg>...</svg>`;
    $: icon6 = $isQuizMode
        ? `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M8 2V5" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M16 2V5" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M21 8.5V13.63C20.11 12.92 18.98 12.5 17.75 12.5C16.52 12.5 15.37 12.93 14.47 13.66C13.26 14.61 12.5 16.1 12.5 17.75C12.5 18.73 12.78 19.67 13.26 20.45C13.63 21.06 14.11 21.59 14.68 22H8C4.5 22 3 20 3 17V8.5C3 5.5 4.5 3.5 8 3.5H16C19.5 3.5 21 5.5 21 8.5Z" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7 11H13" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7 16H9.62" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M23 17.75C23 18.73 22.72 19.67 22.24 20.45C21.96 20.93 21.61 21.35 21.2 21.69C20.28 22.51 19.08 23 17.75 23C16.6 23 15.54 22.63 14.68 22C14.11 21.59 13.63 21.06 13.26 20.45C12.78 19.67 12.5 18.73 12.5 17.75C12.5 16.1 13.26 14.61 14.47 13.66C15.37 12.93 16.52 12.5 17.75 12.5C18.98 12.5 20.11 12.92 21 13.63C22.22 14.59 23 16.08 23 17.75Z" stroke="white" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M17.75 20.25C17.75 18.87 18.87 17.75 20.25 17.75C18.87 17.75 17.75 16.63 17.75 15.25C17.75 16.63 16.63 17.75 15.25 17.75C16.63 17.75 17.75 18.87 17.75 20.25Z" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>`
        : `<svg>...</svg>`;

    // Title
    $: title1 = $isQuizMode ? "Clavier LSF" : "Clavier LSF (enfant)";
    $: title2 = $isQuizMode ? "Dictionnaire" : "Dictionnaire personnalisé";
    $: title3 = $isQuizMode
        ? "Thème clair et foncé"
        : "Thème clair et foncé (enfant)";
    $: title5 = $isQuizMode ? "Quiz" : "Recherche";
    $: title6 = $isQuizMode ? "Quiz Hybride" : "Grammaire";

    // Descriptions
    $: desc1 = $isQuizMode
        ? "Profitez de notre clavier interactif qui vous permet de basculer facilement entre un clavier traditionnel et un clavier en pictogrammes de lettres LSF. Idéal pour apprendre et pratiquer l'alphabet en langue des signes française à votre rythme !"
        : "Profitez de notre clavier interactif qui vous permet de basculer facilement entre un clavier traditionnel et un clavier en pictogrammes de lettres LSF. Idéal pour apprendre et pratiquer l'alphabet en langue des signes française à votre rythme !";
    $: desc2 = $isQuizMode
        ? "Découvrez notre dictionnaire enrichi avec des vidéos pour chaque mot et définition. Consultez non seulement la signification des mots, mais aussi leur interprétation en vidéo pour une expérience d'apprentissage interactive et visuelle !"
        : "Stockez dans votre dictionnaire, les mots que vous avez déjà rencontré. Accédez à leur définition, leur signe, leur catégorie grammaticale en un clin d'oeil.";
    $: desc3 = $isQuizMode
        ? "Personnalisez votre expérience en passant facilement du thème clair au thème sombre dans les paramètres. Choisissez l'option qui vous convient le mieux pour une lecture confortable à tout moment de la journée !"
        : "Personnalisez votre expérience en passant facilement du thème clair au thème sombre dans les paramètres. Choisissez l'option qui vous convient le mieux.";
    $: desc4 = $isQuizMode
        ? "Basculer entre le mode Quiz et le mode Enfant"
        : "Basculer entre le mode Quiz et le mode Enfant";
    $: desc5 = $isQuizMode
        ? "Notre quiz vous permet de tester vos connaissances avec des questions aléatoires ou triées par thèmes et catégories. Découvrez de nouveaux mots avec des supports visuels tels que des vidéos ou des images, disponibles pour enrichir votre apprentissage !"
        : "Recherchez par catégorie grammaticale, ou en tapant les lettres ou leur signe avec le clavier en LSF.";
    $: desc6 = $isQuizMode
        ? "Le Quiz Hybride utilise le machine learning pour faciliter la maîtrise du vocabulaire français, spécialement conçu pour les personnes sourdes. Avec des quiz interactifs quotidiens et thématiques, vous pratiquez et découvrez de nouveaux mots adaptés à votre niveau, pour un apprentissage toujours personnalisé."
        : "En un coup d'oeil, identifiez la catégorie grammaticale d'un mot.";

    function toggleMode() {
        isQuizMode.update((mode) => !mode);

        // Animation for all cards
        gsap.to(bentoItems.querySelectorAll(".bento-item"), {
            scale: 0.95,
            opacity: 0.8,
            duration: 0.3,
            stagger: 0.05,
            ease: "power2.inOut",
            onComplete: () => {
                gsap.to(bentoItems.querySelectorAll(".bento-item"), {
                    scale: 1,
                    opacity: 1,
                    duration: 0.3,
                    stagger: 0.05,
                    ease: "power2.inOut",
                });
            },
        });

        // Specific animation for switch logo
        gsap.to(switchLogo, {
            rotation: "+=360",
            duration: 0.5,
            ease: "power2.inOut",
        });

        // Animation for description
        gsap.to(aboutDescription, {
            opacity: 0,
            y: -20,
            duration: 0.3,
            onComplete: () => {
                gsap.to(aboutDescription, {
                    opacity: 1,
                    y: 0,
                    duration: 0.3,
                });
            },
        });
    }

    onMount(() => {
        // Scroll-triggered animation for each card
        bentoItems.querySelectorAll(".bento-item").forEach((item) => {
            gsap.fromTo(
                item,
                { y: 50, opacity: 0.7 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.5,
                    scrollTrigger: {
                        trigger: item,
                        start: "top bottom-=100",
                        end: "bottom center",
                        toggleActions: "play reverse play reverse",
                        scrub: 1,
                    },
                },
            );
        });

        // Animation for description
        gsap.fromTo(
            aboutDescription,
            { y: 100, opacity: 0 },
            {
                y: 0,
                opacity: 1,
                duration: 1,
                scrollTrigger: {
                    trigger: aboutDescription,
                    start: "top bottom-=100",
                    end: "bottom center",
                    toggleActions: "play reverse play reverse",
                    scrub: 1,
                },
            },
        );

        // Continuous animation for switch button
        gsap.to(switchButton, {
            scale: 1.1,
            duration: 0.5,
            repeat: -1,
            yoyo: true,
            ease: "power1.inOut",
        });
    });
</script>

<section bind:this={infoSection2} class="h-auto w-full py-20">
    <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-4xl font-bold text-center mb-12">
            Nos Fonctionnalités
        </h2>
        <div
            bind:this={aboutDescription}
            class="about-description justify-center flex flex-col self-center content-center items-center text-black pb-20"
        >
            <p class="text-center w-3/4">{boxDescription}</p>
        </div>
        <div
            bind:this={bentoItems}
            class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4"
        >
            <div
                style="min-height: 250px; background-image: url('{bgImage1}'); background-size: cover; background-position: center;"
                class="bento-item flex flex-col bg-gray-100 justify-between rounded-xl p-4"
            >
                <div class="flex items-center justify-end mb-4">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon1}
                        </div>
                    </div>
                </div>
                <div>
                    <h4 class="text-xl font-bold mb-2">{title1}</h4>
                    <p style="font-size: 12px;">{desc1}</p>
                </div>
            </div>

            <div
                style="min-height: 250px; background-image: url('{bgImage2}'); background-size: cover; background-position: center; position: relative;"
                class="bento-item flex flex-col justify-between rounded-xl p-4 sm:col-span-2 md:col-span-2"
            >
                <div
                    style="position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: linear-gradient(185deg, rgba(0,0,0,0) 0%, rgba(0,0,0, 0.2) 60%, rgba(0,0,0, 0.7) 100%); pointer-events: none;"
                    class="rounded-xl"
                ></div>

                <div class="flex items-center justify-end mb-4 relative z-10">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon2}
                        </div>
                    </div>
                </div>
                <div class="text-white relative z-10">
                    <h4 class="text-xl font-bold mb-2">{title2}</h4>
                    <p style="font-size: 12px;" class="w-4/5">{desc2}</p>
                </div>
            </div>

            <div
                style="min-height: 250px; background-image: url('{bgImage3}'); background-size: cover; background-position: center;"
                class="bento-item flex flex-col justify-between rounded-xl p-4"
            >
                <div class="flex items-center justify-end mb-4">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon3}
                        </div>
                    </div>
                </div>
                <div class="text-white">
                    <h4 class="shadow-text text-xl font-bold mb-2">{title3}</h4>
                    <p style="font-size: 12px;" class="shadow-text">{desc3}</p>
                </div>
            </div>

            <div
                style="min-height: 250px;"
                class="bento-item flex flex-col bg-gray-800 rounded-xl p-4"
            >
                <div class="flex items-center justify-end">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon4}
                        </div>
                    </div>
                </div>
                <div
                    class="text-white flex flex-col gap-4 justify-center content-center self-center items-center text-center"
                >
                    <img
                        bind:this={switchLogo}
                        src={logoIcon}
                        alt="Logo"
                        class="w-10 h-10 mx-auto"
                    />
                    <p style="font-size: 12px;" class="w-2/3">{desc4}</p>
                    <button
                        bind:this={switchButton}
                        on:click={toggleMode}
                        class="gradient-border-button py-2 px-4 rounded-full relative overflow-hidden inline-block mx-auto"
                    >
                        <span class="text-12px relative z-10">{buttonText}</span
                        >
                    </button>
                </div>
            </div>

            <div
                style="min-height: 250px; background-image: url('{bgImage5}'); background-size: cover; background-position: center; position: relative;"
                class="bento-item flex flex-col justify-between rounded-xl p-4 row-span-2"
            >
                <div
                    style="position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: linear-gradient(185deg, rgba(0,0,0,0) 0%, rgba(0,0,0, 0.2) 60%, rgba(0,0,0, 0.7) 100%); pointer-events: none;"
                    class="rounded-xl"
                ></div>

                <div class="flex items-center justify-end mb-4 relative z-10">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon5}
                        </div>
                    </div>
                </div>
                <div class="text-white relative z-10">
                    <h4 class="text-xl font-bold mb-2">{title5}</h4>
                    <p style="font-size: 12px;">{desc5}</p>
                </div>
            </div>
            <div
                style="min-height: 250px;"
                class="bento-item flex flex-col bg-gray-100 justify-between rounded-xl p-4 sm:col-span-2 md:col-span-2"
            >
                <div class="flex items-center justify-end mb-4">
                    <div class="text-12px flex-shrink-0 bg-black">
                        <div class="flex items-center justify-center">
                            {@html icon6}
                        </div>
                    </div>
                </div>
                <div>
                    <h4 class="text-xl font-bold mb-2">{title6}</h4>
                    <p class="w-4/5" style="font-size: 12px;">{desc6}</p>
                </div>
            </div>
        </div>
    </div>
</section>

<style>
    .text-12px {
        font-size: 12px;
        min-height: 30px;
        min-width: 30px;
        line-height: 1;
        align-items: center;
        align-content: center;
        border-radius: 25px;
    }

    .gradient-border-button {
        background-color: #212937;
        transition: all 0.3s ease;
    }

    .gradient-border-button::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        border-radius: 9999px;
        padding: 1px;
        background: linear-gradient(90deg, #69b59e, #7daed6, #aa8ac9);
        -webkit-mask:
            linear-gradient(#fff 0 0) content-box,
            linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
    }

    .gradient-border-button:hover {
        transform: scale(1.05);
    }

    .gradient-border-button:hover::before {
        opacity: 0.9;
    }
    .shadow-text {
        text-shadow: 1px 0 10px rgba(0, 0, 0, 0.6);
    }
</style>
