<template>
    <header>
        <h1>{{ header }}</h1>
        <h2>{{ subheader }}</h2>
    </header>
</template>

<script>
export default {
    props: {
        header: String,
        subheader: String
    }
}
</script>


<style lang="scss" scoped>
header {
    h1 {
        font-size: 12px;
        font-weight: 900;
        text-transform: uppercase;
        color: #000;
        letter-spacing: 1px;
        line-height: 1;
        margin-bottom: 1.25rem;
    }

    h2 {
        font-size: clamp(36px, 4vw, 48px);
        font-weight: 900;
        color: #000;
        letter-spacing: -1px;
        line-height: 1;
    }
}
</style>

