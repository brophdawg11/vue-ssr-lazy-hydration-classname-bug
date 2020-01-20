<template>
    <div>
        <h1>Vue Lazy Hydration Classname/Attribute Bug</h1>
        <p>
            This repo shows a bug in not preserving classes/attributes on the root
            element inside a <code>LazyHydrate</code> element.
            <br><br>
            The second button in this page should have a green background,  but
            you will see it is incorrectly red after mount but before hydration.
            Clicking the first button will hydrate the second button, and cause
            the correct styles to show.
            <br><br>
            This is due to the following progression of classes on the inner:
            <code>div</code>
        </p>
        <ol>
            <li>SSR - <code>div.lazy-class-outer.lazy-class</code></li>
            <li>mounted - <code>div.lazy-class-outer</code></li>
            <li>hydrated - <code>div.lazy-class-outer.lazy-class</code></li>
        </ol>
        <p>
            The library needs to proxy along classes/attributes from the existing
            slot element upon mount when the element is not yet hydrated.
        </p>

        <button @click="hydrated = true">Click to hydrate</button>
        <br><br>
        <LazyHydrate :triggerHydration="hydrated" class="lazy-class-outer">
            <div class="lazy-class">
                <button @click="onClick">
                    Click me
                </button>
            </div>
        </LazyHydrate>
    </div>
</template>

<script>
import LazyHydrate from 'vue-lazy-hydration';

export default {
    name: 'Home',
    components: {
        LazyHydrate,
    },
    data() {
        return {
            hydrated: false
        };
    },
    methods: {
        onClick() {
            window.alert('clicked');
        }
    }
};
</script>

<style>
button {
    width: 300px;
    padding: 10px;
    background-color: black;
    color: white;
    font-size: 1.25rem;
}

code {
    font-family: monospace;
}

.lazy-class-outer button {
    background-color: red;
}

.lazy-class button {
    background-color: green;
}
</style>
