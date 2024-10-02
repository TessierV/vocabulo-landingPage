<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";

    let circles = [
        { id: 1, title: "Circle 1" },
        { id: 2, title: "Circle 2" },
        { id: 3, title: "Circle 3" },
        { id: 4, title: "Circle 4" },
        { id: 5, title: "Circle 5" },
        { id: 1, title: "Circle 1" },
        { id: 2, title: "Circle 2" },
        { id: 3, title: "Circle 3" },
        { id: 4, title: "Circle 4" },
        { id: 5, title: "Circle 5" },
        { id: 1, title: "Circle 1" },
        { id: 2, title: "Circle 2" },
        { id: 3, title: "Circle 3" },
        { id: 4, title: "Circle 4" },
        { id: 5, title: "Circle 5" },
        { id: 1, title: "Circle 1" },
        { id: 2, title: "Circle 2" },
        { id: 3, title: "Circle 3" },
        { id: 4, title: "Circle 4" },
        { id: 5, title: "Circle 5" },
        { id: 6, title: "Circle 6" }
    ];

    // Run this function when the component is mounted
    onMount(() => {
        // Select the container element
        const container = document.querySelector(".scroll-container");

        // Function to handle scroll event
        const handleScroll = () => {
            // Animate the container horizontally based on vertical scroll
            gsap.to(container, {
                x: -window.scrollY * 0.5, // Move left, adjust speed by changing multiplier
                ease: "power2.out", // Easing function for smooth animation
                duration: 0.3 // Duration of the animation in seconds
            });
        };

        // Add scroll event listener
        window.addEventListener("scroll", handleScroll);

        // Cleanup function to remove event listener when component is destroyed
        return () => {
            window.removeEventListener("scroll", handleScroll);
        };
    });
</script>

<!-- Section containing multiple circular elements aligned horizontally -->
<section class="overflow-hidden">
    <div class="scroll-container flex gap-5 pb-40 pt-20">
        <!-- Loop through the circles array and create elements for each -->
        {#each circles as circle}
        <div class="circle-item flex items-center gap-5">
            <!-- SVG circle -->
            <svg class="w-24 h-24" viewBox="0 0 100 100">
                <circle cx="50" cy="50" r="48" stroke="black" stroke-width="2" fill="lightblue" />
            </svg>
            <!-- Circle title -->
            <h2 class="text-2xl font-semibold">{circle.title}</h2>
        </div>
        {/each}
    </div>
</section>

<style>
    /* Styles for SVG circles */
    svg {
        fill: lightblue;
    }

    /* Styles for each circular element */
    .circle-item {
        display: flex; /* Aligns SVG and text horizontally */
        align-items: center; /* Centers SVG and text vertically */
        transition: transform 0.3s ease-in-out;
        white-space: nowrap;
    }

    /* Responsive animation for SVGs */
    @media (min-width: 640px) {
        .circle-item svg {
            width: 50px;
            height: 50px;
        }
    }

    @media (min-width: 1024px) {
        .circle-item svg {
            width: 50px;
            height: 50px;
        }
    }
</style>
