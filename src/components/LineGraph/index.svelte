<script lang="ts">
import { onMount } from "svelte";
import { LineGraph } from ".";

	export let data: number[];
	export let title: string;
	export let guideCount: number = 5;
	export let minV: number;
	export let maxV: number;
	
	minV = Math.min(...data);
	maxV = Math.max(...data);
	console.log(`min:${minV},max:${maxV}`);
	const range = maxV - minV;
	const diff = range / guideCount;
	let eleRoot: HTMLDivElement;
	// let eleHeight: number;

	let m_line:string='';
	const makeLine = function(){
		for(let i = 0 ; i < data.length ; i++){
			const d = (eleRoot.clientHeight/maxV);
			m_line += `${i*100},${data[i]*d} `;
		}
		console.log(m_line);
		console.log(data);
	}

	const leftGuides: number[] = [];
	for (let i = 1; i <= guideCount; i++) {
		leftGuides.push(minV + i * diff);
		console.log(`${minV} + ${i} * ${diff} = ${minV + i * diff}`);
	}
	

	onMount(()=>{
		console.log(`eleRoot height: ${eleRoot.clientHeight}`);
		makeLine();
	});
	
</script>

<div class="root">
	<div class="title-field">{title}</div>
	<div class="graph-field">
		<div class="l-guide" bind:this={eleRoot}>
			{#each leftGuides as v}
				<div class="guide-item">{v}</div>
			{/each}
		</div>
		<div class="graphics">
			<svg class="linesvg" viewBox="-50 50 600 513" transform="scale(1,-1)">
				<polyline class="dataLine" points={m_line}  fill="none" stroke="#fff" stroke-width="6" />
            </svg>
		</div>
	</div>
	<div class="under-field">// UNDER</div>
</div>

<style lang="scss">
	.root {
		$title-height: 48px;
		$under-height: 32px;
		height: 80%;
		width: 80%;

		.title-field {
			height: $title-height;
			width: 100%;
			background: blueviolet;
		}
		.graph-field {
			height: calc(100% - $title-height - $under-height);
			width: 100%;
			display: flex;
			position: relative;
			.l-guide {
				height: 100%;
				width: 100%;
				background: #ff0;
				display: flex;
				flex-direction: column-reverse;
				.guide-item {
					flex: 1 0;
					border-bottom: solid 1px #000;
				}
			}
			.graphics {
				right: 0;
				top: 0;
				height: 100%;
				width: calc(100% - 100px);
				position: absolute;
				background: rgba(0, 255, 0, 0.3);
				border-left: solid 2px #000;
				display: flex;
			}
		}
		.under-field {
			height: $under-height;
			width: 100%;
			background:cornflowerblue;
		}
	}
</style>

