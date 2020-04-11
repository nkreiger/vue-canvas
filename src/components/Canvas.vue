<template>
    <div>
        <canvas :id="canvasId" class="canvas-style" v-on:mousedown="mouseDown"
        />
    </div>
</template>

<script>
    // TODO: move all of this logic to master
    // packages
    const paper = require('paper');

    export default {
        name: "Canvas",
        props: ['canvasId'],
        data: () => ({
            path: null,
            scope: null
        }),
        methods: {
            reset() {
                this.scope.project.activeLayer.removeChildren();
            },
            pathCreate(scope) {
                scope.activate();
                return new paper.Path({
                    strokeColor: "#000000",
                    strokeJoin: 'round',
                    strokeWidth: 1.5
                })
            },
            createTool(scope) {
                scope.activate();
                return new paper.Tool();
            },
            mouseDown() {
                // in order to access functions in nested tool
                let self = this;

                // create drawing tool
                this.tool = this.createTool(this.scope);

                this.tool.onMouseDown = (event) => {
                    // init path
                    self.path = self.pathCreate(self.scope);
                    // add point to path
                    self.path.add(event.point);
                };

                this.tool.onMouseDrag = (event) => {
                    self.path.add(event);
                };

                this.tool.onMouseUp = (event) => {
                    // line completed
                    self.path.add(event.point);
                }
            }
        },
        mounted() {
            this.scope = new paper.PaperScope();

            this.scope.setup(this.canvasId);
        }
    }
</script>

<style scoped>
    .canvas-style {
        cursor: crosshair;
        width: 100% !important;
        height: 500px !important;
        border: 5px solid black;
        border-radius: 10px;
        display: block;
        margin: auto;
        box-shadow: 0 10px 8px -8px black;
    }
</style>
