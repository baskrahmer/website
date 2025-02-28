<script lang="ts" context="module">
    import { writable } from 'svelte/store';

    export type NavLink = {
        label: string;
        href: string;
    };
    export const isHeaderHidden = writable(false);
    export const isMobileNavOpen = writable(false);
</script>

<script lang="ts">
    import { browser } from '$app/environment';
    import { MobileNav } from '$lib/components';
    import { BANNER_KEY } from '$lib/constants';
    import { isVisible } from '$lib/utils/isVisible';
    import { createScrollInfo } from '$lib/utils/scroll';
    import { addEventListener } from '@melt-ui/svelte/internal/helpers';
    import { onMount } from 'svelte';

    let theme: 'light' | 'dark' | null = 'dark';

    function setupThemeObserver() {
        const handleVisibility = () => {
            theme = getVisibleTheme();
        };

        const observer = new MutationObserver(handleVisibility);
        observer.observe(document.body, { childList: true, subtree: true });

        const callbacks = [
            addEventListener(window, 'scroll', handleVisibility),
            addEventListener(window, 'resize', handleVisibility)
        ];

        return () => {
            observer.disconnect();
            callbacks.forEach((callback) => callback());
        };
    }

    function isInViewport(element: Element): boolean {
        return isVisible(element, {
            top: 32,
            bottom: 32,
            left: 0,
            right: window.innerWidth
        });
    }

    function getVisibleTheme() {
        const themes = Array.from(document.querySelectorAll('.theme-dark, .theme-light')).filter(
            (element) => {
                const { classList, dataset } = element as HTMLElement;
                if (
                    classList.contains('aw-mobile-header') ||
                    classList.contains('aw-main-header') ||
                    element === document.body ||
                    typeof dataset['themeIgnore'] === 'string'
                ) {
                    return false;
                }
                return true;
            }
        );

        for (const theme of themes) {
            if (isInViewport(theme)) {
                return theme.classList.contains('theme-light') ? 'light' : 'dark';
            }
        }

        return 'dark';
    }

    onMount(() => {
        return setupThemeObserver();
    });

    let navLinks: NavLink[] = [
        {
            label: 'Docs',
            href: '/docs'
        },
        {
            label: 'Community',
            href: '/community'
        },
        {
            label: 'Blog',
            href: '/blog'
        },
        {
            label: 'Pricing',
            href: '/pricing'
        }
    ];

    $: resolvedTheme = $isMobileNavOpen ? 'dark' : theme;

    const scrollInfo = createScrollInfo();

    $: $isHeaderHidden = (() => {
        if ($scrollInfo.top < 250) {
            return false;
        }
        if ($scrollInfo.direction === 'down') {
            return true;
        }

        return $scrollInfo.deltaDirChange < 200;
    })();

    const hideTopBanner = () => {
        document.body.dataset.bannerHidden = '';
        localStorage.setItem(BANNER_KEY, 'true');
    };
</script>

<div class="u-position-relative">
    <section
        class="aw-mobile-header theme-{resolvedTheme}"
        class:is-transparent={browser && !$isMobileNavOpen}
        class:is-hidden={$isHeaderHidden}
    >
        <div class="aw-mobile-header-start">
            <a href="/">
                <img
                    class="aw-logo aw-u-only-dark"
                    src="/images/logos/appwrite.svg"
                    alt="appwrite"
                    height="24"
                    width="130"
                />
                <img
                    class="aw-logo aw-u-only-light"
                    src="/images/logos/appwrite-light.svg"
                    alt="appwrite"
                    height="24"
                    width="130"
                />
            </a>
        </div>
        <div class="aw-mobile-header-end">
            {#if !$isMobileNavOpen}
                <a href="https://cloud.appwrite.io" class="aw-button">
                    <span class="text">Get started</span>
                </a>
            {/if}
            <button
                class="aw-button is-text"
                aria-label="open navigation"
                on:click={() => ($isMobileNavOpen = !$isMobileNavOpen)}
            >
                {#if $isMobileNavOpen}
                    <span aria-hidden="true" class="aw-icon-close" />
                {:else}
                    <span aria-hidden="true" class="aw-icon-hamburger-menu" />
                {/if}
            </button>
        </div>
    </section>
    <header
        class="aw-main-header is-special-padding theme-{resolvedTheme} is-transparent"
        class:is-hidden={$isHeaderHidden}
    >
        <div class="aw-top-banner">
            <div class="aw-top-banner-content aw-u-color-text-primary">
                <a href="/discord" target="_blank" rel="noopener noreferrer">
                    <span class="aw-caption-500">We are having lots of fun on</span>
                    <span class="aw-icon-discord" aria-hidden="true" />
                    <span class="aw-caption-500">Discord. Come and join us!</span>
                </a>
                {#if browser}
                    <button
                        class="aw-top-banner-button"
                        aria-label="close discord message"
                        on:click={hideTopBanner}
                    >
                        <span class="aw-icon-close" aria-hidden="true" />
                    </button>
                {/if}
            </div>
        </div>

        <div class="aw-main-header-wrapper">
            <div class="aw-main-header-start">
                <a href="/">
                    <img
                        class="aw-logo aw-u-only-dark"
                        src="/images/logos/appwrite.svg"
                        alt="appwrite"
                        height="24"
                        width="130"
                    />
                    <img
                        class="aw-logo aw-u-only-light"
                        src="/images/logos/appwrite-light.svg"
                        alt="appwrite"
                        height="24"
                        width="130"
                    />
                </a>
                <nav class="aw-main-header-nav">
                    <ul class="aw-main-header-nav-list">
                        {#each navLinks as { label, href }}
                            <li class="aw-main-header-nav-item">
                                <a class="aw-link" {href}>{label}</a>
                            </li>
                        {/each}
                    </ul>
                </nav>
            </div>
            <div class="aw-main-header-end">
                <a
                    href="https://github.com/appwrite/appwrite/stargazers"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="aw-button is-text"
                >
                    <span aria-hidden="true" class="aw-icon-star" />
                    <span class="text">Star on GitHub</span>
                    <span class="aw-inline-tag aw-sub-body-400">37.9K</span>
                </a>
<!--                <a href="https://cloud.appwrite.io/register" class="aw-button is-secondary"-->
<!--                    >Sign up</a-->
<!--                >-->
                <a href="https://cloud.appwrite.io" class="aw-button">
                    <span class="text">Get started</span>
                </a>
            </div>
        </div>
    </header>
    <MobileNav bind:open={$isMobileNavOpen} links={navLinks} />

    <main class="aw-main-section" class:aw-u-hide-mobile={$isMobileNavOpen}>
        <slot />
    </main>
</div>
