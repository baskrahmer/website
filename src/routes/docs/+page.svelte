<script lang="ts">
    import { Carousel, Spline } from '$lib/components';
    import Technologies from '$lib/components/Technologies.svelte';
    import Docs from '$lib/layouts/Docs.svelte';
    import { DEFAULT_DESCRIPTION, DEFAULT_HOST } from '$lib/utils/metadata';
    import { TITLE_SUFFIX } from '$routes/titles';
    import MainFooter from '../../lib/components/MainFooter.svelte';
    import CodeCard, { type CodeCardProps } from './CodeCard.svelte';
    import Sidebar from './Sidebar.svelte';

    const title = 'Docs' + TITLE_SUFFIX;
    const description = DEFAULT_DESCRIPTION;
    const ogImage = DEFAULT_HOST + '/images/open-graph/docs.png';

    const tutorials: CodeCardProps[] = [
        {
            href: '/docs/tutorials/react',
            cover: '/images/tutorials/react.png',
            title: 'React tutorial',
            description: 'Learn Appwrite Auth, Databases, and more with React.'
        },
        {
            href: '/docs/tutorials/sveltekit',
            cover: '/images/tutorials/svelte.png',
            title: 'SvelteKit tutorial',
            description: 'Learn Appwrite Auth, Databases, and more with SvelteKit.'
        },
        {
            href: '/docs/tutorials/vue',
            cover: '/images/tutorials/vue.png',
            title: 'Vue tutorial',
            description: 'Learn Appwrite Auth, Databases, and more with Vue.'
        },
        {
            href: '/docs/tutorials/android',
            cover: '/images/tutorials/android.png',
            title: 'Android tutorial',
            description: 'Learn Appwrite Auth, Databases, and more with Android.'
        },
        {
            href: '/docs/tutorials/flutter',
            cover: '/images/tutorials/flutter.png',
            title: 'Flutter tutorial',
            description: 'Learn Appwrite Auth, Databases, and more with Flutter.'
        }
    ];
</script>

<svelte:head>
    <!-- Titles -->
    <title>{title}</title>
    <meta property="og:title" content={title} />
    <meta name="twitter:title" content={title} />
    <!-- Desscription -->
    <meta name="description" content={description} />
    <meta property="og:description" content={description} />
    <meta name="twitter:description" content={description} />
    <!-- Image -->
    <meta property="og:image" content={ogImage} />
    <meta property="og:image:width" content="1200" />
    <meta property="og:image:height" content="630" />
    <meta name="twitter:image" content={ogImage} />
    <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<Docs variant="default">
    <Sidebar />
    <div class="u-position-absolute u-inset-inline-end-0 aw-u-opacity-40-mobile" style="">
        <enhanced:img src="./blur-1.png" alt="" />
    </div>

    <div
        class="u-position-absolute aw-is-not-mobile u-only-light"
        style:inline-size="768px"
        style:block-size="768px"
        style:inset-block-start="26rem"
        style:left="calc(50% - 384px + 600px)"
    >
        <img
            src="/images/animations/tech-light.png"
            width="768"
            height="768"
            alt=""
            style="position: absolute; display: block;"
        />
    </div>

    <main class="aw-main-section u-position-relative">
        <div class="u-position-absolute aw-u-opacity-40-mobile bg-blur">
            <img src="/images/bgs/docs-blur-1.svg" alt="" />
        </div>

        <div
            class="u-position-absolute u-inset-inline-start-0 u-inset-block-start-16 aw-u-opacity-40-mobile"
            style="    margin-inline-start: -30px;"
        >
            <enhanced:img src="./blur-2.png" alt="" />
        </div>

        <section class="aw-hero is-align-start u-position-relative">
            <h1 class="aw-display aw-u-color-text-primary u-max-width-600">
                Learn how to build like a team of hundreds<span class="aw-u-color-text-accent"
                    >_
                </span>
            </h1>
            <p class="aw-description u-max-width-600">
                Appwrite helps you build secure and scalable apps, faster. Leverage Appwrite's
                powerful APIs to stop fighting technologies and start delivering value.
            </p>
        </section>
        <section class="aw-hero is-align-start tech-hero">
            <h2 class="aw-title aw-u-color-text-primary u-max-width-600">
                Get started with your technologies
            </h2>
            <p class="aw-description u-max-width-600">
                Start building with your preferred web, mobile, and native frameworks by following a
                quick start guide.
            </p>
            <Technologies />
            <a href="/docs/sdks" class="aw-button is-secondary" style:align-self="start">
                <span class="aw-sub-body-500">Explore all technologies</span>
            </a>

            <div class="u-position-absolute aw-is-not-mobile u-only-dark spline-wrapper">
                <Spline url="/images/animations/dark-scene.splinecode" width={660} height={660}>
                    <img
                        src="/images/animations/tech-dark.png"
                        width="660"
                        height="660"
                        alt=""
                        style="position: absolute;"
                    />
                </Spline>
            </div>
            <div class="bg-boi" />
        </section>
        <section>
            <h2 class="aw-title aw-u-color-text-primary u-max-width-600">Show me some code</h2>
            <p class="aw-description u-max-width-600 u-margin-block-start-16">
                If you learn best from code examples, follow one of our tutorials.
            </p>
            <Carousel size="medium">
                {#each tutorials as tutorial}
                    <li style:scroll-snap-align="start">
                        <CodeCard {...tutorial} />
                    </li>
                {/each}
            </Carousel>
        </section>
        <section class="aw-hero is-align-start is-no-max-width">
            <h2 class="aw-title aw-u-color-text-primary u-max-width-600">Explore capabilities</h2>
            <p class="aw-description u-max-width-600">
                All the core functionalities you need with a scalable and flexible API. Explore
                Appwrite's product offerings.
            </p>
            <div class="u-margin-block-start-24">
                <ul class="aw-grid-row-4 aw-grid-row-4-m-1">
                    <li>
                        <a href="/docs/products/auth" class="aw-card is-normal">
                            <img
                                src="/images/icons/illustrated/dark/auth.png"
                                alt=""
                                class="u-only-dark"
                                width="48"
                                height="48"
                            />
                            <img
                                src="/images/icons/illustrated/light/auth.png"
                                alt=""
                                class="u-only-light"
                                width="48"
                                height="48"
                            />
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Auth
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Sign in users with multiple OAuth providers.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/products/databases" class="aw-card is-normal">
                            <img
                                src="/images/icons/illustrated/dark/databases.png"
                                alt=""
                                class="u-only-dark"
                                width="48"
                                height="48"
                            />
                            <img
                                src="/images/icons/illustrated/light/databases.png"
                                alt=""
                                class="u-only-light"
                                width="48"
                                height="48"
                            />
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Databases
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Store your application and user data.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/products/functions" class="aw-card is-normal">
                            <img
                                src="/images/icons/illustrated/dark/functions.png"
                                alt=""
                                class="u-only-dark"
                                width="48"
                                height="48"
                            />
                            <img
                                src="/images/icons/illustrated/light/functions.png"
                                alt=""
                                class="u-only-light"
                                width="48"
                                height="48"
                            />
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Functions
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Extend and customize your server's functionality.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/products/storage" class="aw-card is-normal">
                            <img
                                src="/images/icons/illustrated/dark/storage.png"
                                alt=""
                                class="u-only-dark"
                                width="48"
                                height="48"
                            />
                            <img
                                src="/images/icons/illustrated/light/storage.png"
                                alt=""
                                class="u-only-light"
                                width="48"
                                height="48"
                            />
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Storage
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Store images, videos, documents, and files.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/apis/realtime" class="aw-card is-normal">
                            <img
                                src="/images/icons/illustrated/dark/realtime.png"
                                alt=""
                                class="u-only-dark"
                                width="48"
                                height="48"
                            />
                            <img
                                src="/images/icons/illustrated/light/realtime.png"
                                alt=""
                                class="u-only-light"
                                width="48"
                                height="48"
                            />
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Realtime
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Respond to server events in realtime.
                            </p>
                        </a>
                    </li>
                </ul>
            </div>
        </section>
        <section class="aw-hero is-align-start is-no-max-width">
            <h2 class="aw-title aw-u-color-text-primary u-max-width-600">
                Explore ways to integrate
            </h2>
            <p class="aw-description u-max-width-600">
                Choose how you integrate with Appwrite. Explore references for the Appwrite SDK,
                REST API, GraphQL API, or Realtime API.
            </p>
            <div class="u-margin-block-start-24">
                <ul class="aw-grid-row-2">
                    <li>
                        <a href="/docs/sdks" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                SDKs
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Light-weight SDKs for your favorite platforms.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/apis/rest" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                REST API
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Integrate with HTTP requests without the needing an SDK.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/apis/graphql" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                GraphQL
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Leverage GraphQL through our SDKs or integrate directly with REST
                                endpoints.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/apis/realtime" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Realtime
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Respond to auth, databases, storage, and function events in
                                realtime.
                            </p>
                        </a>
                    </li>
                </ul>
            </div>
        </section>
        <section class="aw-hero is-align-start is-no-max-width">
            <h2 class="aw-title aw-u-color-text-primary u-max-width-600">Migrate to Appwrite</h2>
            <p class="aw-description u-max-width-600">
                Own your data with automatic data migrations.
            </p>
            <div class="u-margin-block-start-24">
                <ul class="aw-grid-row-4">
                    <li>
                        <a href="/docs/advanced/migrations/self-hosted" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Self-hosted
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Move data from self-hosted to Appwrite Cloud.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/advanced/migrations/firebase" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Firebase
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Migrate users and data from Firebase to Appwrite.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/advanced/migrations/supabase" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Supabase
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Migrate users and data from Supabase to Appwrite.
                            </p>
                        </a>
                    </li>
                    <li>
                        <a href="/docs/advanced/migrations/nhost" class="aw-card is-normal">
                            <h4
                                class="aw-sub-body-500 aw-u-color-text-primary u-margin-block-start-8"
                            >
                                Nhost
                            </h4>
                            <p class="aw-sub-body-400 u-margin-block-start-4">
                                Migrate users and data from NHost to Appwrite.
                            </p>
                        </a>
                    </li>
                </ul>
            </div>
        </section>

        <MainFooter variant="docs" />
    </main>
</Docs>

<style lang="scss">
    .aw-main-section {
        max-inline-size: unset;
        margin-inline: unset;
        padding-inline-start: 3rem; // 48px
    }

    .bg-blur {
        inset-inline-end: -300px;
        inset-block-start: -100px;
    }

    .tech-hero {
        @include border-block-gradient;

        background: linear-gradient(to right, #19191c80, #19191c00);
        // background-color: #19191c80;
        backdrop-filter: blur(1rem);
        -webkit-backdrop-filter: blur(1rem);

        --m-border-size: 1px;
        --m-border-gradient-before: linear-gradient(
            to right,
            hsl(var(--aw-color-smooth)) 0%,
            hsl(var(--aw-color-smooth)) 90%,
            transparent
        );

        max-inline-size: unset;
        margin-block-start: 2rem;
        margin-inline-start: -3rem;
        padding-block: 5rem;
        padding-inline-start: 3rem;

        position: relative;
        z-index: 10;

        .spline-wrapper {
            --p-size: 700px;
            inline-size: var(--p-size);
            block-size: var(--p-size);
            inset-block-start: -3rem;
            z-index: -1;
            left: calc(50% - 384px + 600px);
        }

        .bg-boi {
            position: absolute;
            background: linear-gradient(to right, #19191c00 0%, #19191c00 10%, #19191c);

            top: 0;
            right: 10rem;
            translate: 100%;
            width: 25rem;
            height: 100%;
            content: '';
            z-index: 9999;
        }
    }
</style>
