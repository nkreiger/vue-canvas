<template>
    <div>
        <!-- button toggles -->
        <div class="row mt-5">
            <div class="col-5" />
            <div class="col-2">
                <button class="btn btn-primary btn-block" @click.prevent="reset">CLEAR</button>
            </div>
            <div class="col-5"/>
        </div>

        <!-- canvas single -->
        <div class="row mt-5">
            <div class="col-2"/>
            <div class="col-8">
                <Canvas :canvas-id="'canvas-one'" ref="childCanvas"/>
            </div>
            <div class="col-2"/>
        </div>
    </div>
</template>

<script>
    import Canvas from "../components/Canvas";
    export default {
        name: "Master",
        data: () => ({
            buttons: ['Simple', 'Separate', 'Replicated'],
            single: true
        }),
        methods: {
            reset() {
                console.log(this.$refs);
                this.$refs.childCanvas.reset();
            }
        },
        components: {
            Canvas
        }
    }
</script>

<style scoped>

</style>
