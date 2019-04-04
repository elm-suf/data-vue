<template>
    <div class="container">
        <h1 class="title">{{title}}</h1>

        <svg width="600" height="360">
            <path fill="none" stroke="yellow" stroke-width="5" :d="d"/>
            <circle v-for="(item, index) in dataset"
                    :key="index"
                    :cx="item[0]"
                    :cy="item[1]"
                    r="16"
                    @click="itemClicked(item)">
            </circle>
        </svg>
    </div>
</template>

<script>
    import dataset from './dataset'
    import * as d3 from 'd3'
    import {shuffle} from "d3";

    export default {
        name: 'demo-d3',

        data() {
            return {
                title: "D3 demo",
                dataset,
                curve: 'curveStepAfter'
            };
        },
        methods: {
            itemClicked(item) {
                console.log(item);
                this.curve =
                    this.curve === 'curveStepAfter' ? 'curveStepBefore' : 'curveStepAfter'

                this.dataset = shuffle(this.dataset)
            }
        },

        computed: {
            lineGenerator() {
                return d3
                    .line()
                    .curve(d3[this.curve])
                    .x(v => v[0])
                    .y(v => v[1])
            },

            d() {
                return this.lineGenerator(this.dataset)
            }
        }


    };
</script>

<style>
    svg {
        background-color: #2c3e50;
    }

    circle {
        fill: darkgray;
    }

    circle:hover {
        fill: crimson;
    }


    path,
    circle {
        transition: all 500ms ease;
    }
</style>
