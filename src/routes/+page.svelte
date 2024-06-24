<script lang="ts">
    
    const ARR_LENGTH = 100;

    let curPtr = 1;
    let startSorting = false;
    let data: number[] = Array.from({ length: ARR_LENGTH }, () => Math.round(Math.random() * 100));

    const createArr = () => {
        data = Array.from({ length: ARR_LENGTH }, () => Math.random() * 100 + 1);
    }

    const insertionSort = async (arr: number[]) => {
        const delay = (ms: number) => {
            return new Promise((resolve) => {setTimeout(resolve, ms);});
        }
        // insertion sort is the process of 
        // 'inserting' the current element
        //  into its rightful place.
        startSorting = true;
        for (let i = 1; i < ARR_LENGTH; i++) {
            let j = i;
            while (j > 0 && arr[j - 1] > arr[j]) {
                curPtr = j;
                await delay(10);
                let tmp = arr[j - 1];
                arr[j - 1] = arr[j];
                arr[j] = tmp;
                j--;
            }
            data = arr;
        }
        startSorting = false;
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&family=Playwrite+NG+Modern:wght@100..400&display=swap');
    * {
        font-family: "Playwrite NG Modern";
    }
    .v-container {
        width: 500px;
        height: 500px;
        position: relative;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        flex-direction: column;
        padding: 10px;
        justify-content: center;
        align-items: center;
        gap: 10px;
    }
    .btn-container {
        display: flex;
        width: 100%;
        justify-content: space-around;
        align-items: center;
    }
    button {
        padding: 15px;
        font-size: 1rem;
        font-weight: 500;
        border: none;
        border-radius: 10px;
        background-color: #D7E3FC;
    }

    button:hover {
        cursor: pointer;
        background-color: #CCDBFD;
    }

    .box {
        width: 500px;
        height: 500px;
        display: flex;
        align-items: flex-end;
    }
</style>

<div class="v-container">
    <h2>Insertion Sort</h2>
    <div class="box">
        {#each data as item, i}
            <div style="
                    height: {item}%;
                    width: {1 / data.length * 100}%;
                    background: {startSorting && i == curPtr ? "#abc4ff": "#edf2fb"};
            "/>
        {/each}
    </div>
    <div class="btn-container">
        <button on:click={createArr}>Recreate Array</button>
        <button on:click={() => insertionSort([...data])}>Sort The Array</button>
    </div>
</div>