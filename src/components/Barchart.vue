<template>
    <div class="container">
        <svg :width="width" :height="height">
            <rect v-for="(item, index) in nodeList"
                  :key="index"
                  :height="getHeight(item)"
                  :width="barWidth"
                  :x="barWidth * index"
                  :y="height - getHeight(item)">

            </rect>
        </svg>

    </div>
</template>

<script>
    import chartData from './barchartData'
    import * as d3 from 'd3'

    export default {
        // mounted: function () {
        //     d3.select('svg').append('rect').attr('height', 222).attr('width', 222)
        // },
        name: 'bar-chart',

        data() {
            function getNode(e) {
                return {
                    date: new Date(e[0]),
                    gdp: e[1],
                }
            }

            return {
                width: 1080,
                height: 600,
                nodeList: chartData.data.map(e => getNode(e)),
            }
        },
        methods: {
            getHeight(item) {
                const scale = d3.scaleLinear()
                    .domain([0, d3.max(this.nodeList, val => val.gdp)])
                    .range([0, this.height]);
                return scale(item.gdp)
            }
        },
        computed: {

            barWidth() {
                return this.width / this.nodeList.length
            }
        }

    }

</script>

<style>
    svg {
        background-color: #2c3e50;
        margin: 8%;
    }

    rect {
        fill: darkgray;
        stroke: #42b983;
    }

    rect:hover {
        fill: crimson;
    }
</style>
