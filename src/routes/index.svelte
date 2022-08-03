<script lang="ts"> 
    

    let title:string = 'line graph'
    let data:number[] = [10,12,31,8,11,50]
    let max:number = Math.max(...data);
    let min:number = Math.min(...data);
    
</script>

<div class="root">
    <div class="graph-field">
        <LineGraph {title} {data} bind:{max} bind:{min}/>
    </div>
</div>
