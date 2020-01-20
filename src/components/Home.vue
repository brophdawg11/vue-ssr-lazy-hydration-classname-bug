<template>
    <div>
        <h1>Vue Lazy Hydration Classname/Attribute Bug</h1>
        <br><br>
        <button @click="hydrated = true">Click to hydrate</button>
        <br><br>
        <LazyHydrate :triggerHydration="hydrated">
            <div id="lazy-id" class="lazy-class">
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

#lazy-id button {
    background-color: red;
}

.lazy-class button {
    color: blue;
}
</style>
