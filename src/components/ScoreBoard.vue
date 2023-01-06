<template>
    <section class="score">
        Player <span>{{ this.winCount }}</span> x <span>{{ this.loseCount }}</span> CPU
    </section>
</template>

<script>
export default {
    props: [
        'winCount',
        'loseCount'
    ]
}
</script>

<style lang="scss">
section.score {
    padding:  24px;
    border-bottom: 1px solid black;
    font-size: 18px;
    span {
        padding: 8px;
        font-weight: bold;
        border: 1px solid black;
    }
}
</style>