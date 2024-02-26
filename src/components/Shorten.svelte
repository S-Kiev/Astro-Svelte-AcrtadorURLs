<script>
    import ClipBoard from "./ClipBoard.svelte";

    let url = "";
    const styleInput = "bg-gray-200 appearance-none border border-gray-200 rounded w-full py-3 py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500";
    const styleButton = "bg-purple-500 hover:bg-purple-400 text-white font-bold py-2 px-10 rounded rounded focus:outline-none focus:shadow-outline";

    let urlResult = "";
    let show = false;

    const copy = () => {
        const app = new ClipBoard({
            target: document.getElementById('clipboard'),
            props: { urlResult }
        });

        app.$destroy();
    }

    const fetchUrl = async () => {
        const options = {
            method: 'POST',
            headers: {
                accept: 'application/json',
                'Content-Type': 'application/json',
                'Authorization': 'sk_b6ECSdoRA4aiIU2Y',
            },
            body: JSON.stringify({ originalURL: url, domain: 'do5r.short.gy' })
        };
        const response = await fetch('https://api.short.io/links', options);
        const data = await response.json();
        console.log(data);
        urlResult = data.shortURL;
        show = true;
    }
    
    //do5r.short.gy
    //sk_b6ECSdoRA4aiIU2Y
</script>


<input type="text" name="" id="" bind:value={url} class={styleInput} placeholder="https://">

<div class="md:flex md:items-center justify-center mt-10">
    <button type="button" class={styleButton} on:click={fetchUrl}>Acortar</button>
</div>


{#if show}
    <div class="md:flex md:items-center mt-10 justify-center">
        <input type="text" bind:value={urlResult} class="text-5xl text-pink-500">
        <button type="button" class={styleButton} on:click={copy}>Copiar</button>
        <div id="clipboard"></div>
    </div>

    <div class="md:flex md:items-center justify-center mt-10">
        <input type="text" name="" id="" bind:value={urlResult} class={styleInput} placeholder="https://">
    </div>
{/if}