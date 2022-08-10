<script lang="ts"> 
    import {LineGraph} from '@src/components/LineGraph';

    let title:string = 'line graph'
    let data:number[] = [10,12,31,8,11,50]
    let maxV:number = Math.max(...data);
    let minV:number = Math.min(...data);
    
</script>

<div class="root">
    <LineGraph data={data} title={title} bind:maxV={maxV} bind:minV={minV}/>
</div>


<style lang="scss">
    .root{
        width:100vw;
        height:100vh;
        
        display: flex;
        flex-flow: column nowrap;
        justify-content: center;
        align-items: center;
    }
</style>