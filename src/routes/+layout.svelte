<script>
    export const prerender = true;

    import '../app.css';
    let isDropdownOpen = false; // default state (dropdown close)

    const handleDropdownClick = () => {
        isDropdownOpen = !isDropdownOpen; // togle state on click
    };

    const handleDropdownFocusLoss = ({ relatedTarget, currentTarget }) => {
        // use "focusout" event to ensure that we can close the dropdown when clicking outside or when we leave the dropdown with the "Tab" button
        if (relatedTarget instanceof HTMLElement && currentTarget.contains(relatedTarget)) return; // check if the new focus target doesn't present in the dropdown tree (exclude ul\li padding area because relatedTarget, in this case, will be null)
        isDropdownOpen = false;
    };

    const nav_button = [
        { title: 'Boarding', link: '/Boarding' },
        { title: 'Grooming', link: '/Grooming' },
        { title: 'About', link: '/About' },
        { title: 'Contact', link: '/Contact' }
    ];
</script>

<div class="relative">
    <nav class="bg-teal-500">
        <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
            <div class="flex h-16 justify-between">
                <div class="flex">
                    <div class="-ml-2 mr-2 flex items-center md:hidden">
                        <button
                            type="button"
                            class="inline-flex items-center justify-center rounded-md p-2 text-gray-100 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-teal-600"
                            aria-controls="mobile-menu"
                            aria-expanded="false"
                            on:click={handleDropdownClick}
                            >
                        <span class="sr-only">Open main menu</span>
                            <svg
                                class="block h-6 w-6"
                                xmlns="http://www.w3.org/2000/svg"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke-width="1.5"
                                stroke="currentColor"
                                aria-hidden="true"
                                >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
                                />
                            </svg>
                            <svg
                                class="hidden h-6 w-6"
                                xmlns="http://www.w3.org/2000/svg"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke-width="1.5"
                                stroke="currentColor"
                                aria-hidden="true"
                                >
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                            </svg>
                        </button>
                    </div>
                    <div class="flex flex-shrink-0 items-center">
                        <a href="/">
                            <img
                                class="block h-16 w-auto lg:hidden"
                                src="https://static.wixstatic.com/media/883a38_b765e5d18155474d85fe6c731f7bd26c~mv2_d_9000_10800_s_4_2.jpg/v1/fill/w_260,h_308,al_c,q_80,usm_0.66_1.00_0.01,enc_auto/883a38_b765e5d18155474d85fe6c731f7bd26c~mv2_d_9000_10800_s_4_2.jpg"
                                alt="Your Company"
                            />
                        </a>
                        <a href="/">
                            <img
                                class="hidden h-16 w-auto lg:block"
                                src="https://static.wixstatic.com/media/883a38_b765e5d18155474d85fe6c731f7bd26c~mv2_d_9000_10800_s_4_2.jpg/v1/fill/w_260,h_308,al_c,q_80,usm_0.66_1.00_0.01,enc_auto/883a38_b765e5d18155474d85fe6c731f7bd26c~mv2_d_9000_10800_s_4_2.jpg"
                                alt="Your Company"
                            />
                        </a>
                    </div>
                    <div class="hidden md:ml-6 md:flex md:space-x-8">
                        {#each nav_button as item}
                            <a
                                href={item.link}
                                class="inline-flex items-center border-b-2 border-transparent px-1 pt-1 text-sm font-medium text-gray-100 hover:border-gray-300 hover:text-gray-700"
                            >{item.title}</a
                            >
                        {/each}
                    </div>
                </div>
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <a
                            class="relative inline-flex items-center rounded-md border border-transparent bg-teal-600 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-teal-400 focus:outline-none focus:ring-2 focus:ring-teal-500 focus:ring-offset-2"
                            href="/Gallery"
                            >
                            <span>Gallery</span>
                        </a>
                        <a
                            class="relative inline-flex items-center rounded-md border border-transparent bg-teal-600 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-teal-400 focus:outline-none focus:ring-2 focus:ring-teal-500 focus:ring-offset-2"
                            href="/Forms"
                            >
                            <span>Forms</span>
                        </a>
                    </div>
                    <div class="hidden md:ml-4 md:flex md:flex-shrink-0 md:items-center">
                        <div class="relative ml-3" />
                    </div>
                </div>
            </div>
        </div>
    </nav>
    <div
        class={`md:hidden bg-teal-500 ${isDropdownOpen ? 'visibility: visible' : 'visibility: hidden'}`}
        id="mobile-menu"
        >
        <div class="space-y-1 pt-2 pb-3">
            {#each nav_button as item}
                <a
                    href={item.link}
                    class="block border-l-4 border-transparent py-2 pl-3 pr-4 text-base font-medium text-gray-100 hover:border-gray-300 hover:bg-gray-50 hover:text-gray-700 sm:pl-5 sm:pr-6"
                >{item.title}</a
                >
            {/each}
        </div>
        <div class="border-t border-gray-200 pt-4 pb-3">
            <div class="flex items-center px-4 sm:px-6">
                <div class="flex-shrink-0" />
            </div>
        </div>
    </div>
</div>
<slot />
<footer class="fixed  bottom-0">
    <p class="text-center text-gray-500">
        © 2022 by <a
            href="https://www.linkedin.com/company/imaginehappens-llc/about"
            target="_blank"
            rel="noreferrer">ImagineHappens LLC</a
        >
    </p>
</footer>

