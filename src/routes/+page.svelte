<script>
    import cards from '$lib/cards.js';

    let results = [];

    for(let card of cards) {
        card.search = `${card.title} ${card.desc} ${card.keys}`.toLowerCase();
    }

    const search = event => {
        let terms = event.target.value.toLowerCase().split(' ');

        results = [];
        let count = 0;
        for(let card of cards) {
            count++;
            if(count>1000) return;
            let valid = false;
            for(let term of terms)
                if(card.search.includes(term))
                    valid = true;
            
            if(valid)
                results.splice(results.length, 0, card);
        }
    }

    search({
        target: {
            value: ""
        }
    });
</script>

<span class="wrapper">
    <input placeholder="Search" class="search" on:input={search}>
    <p class="spacer"></p>
    {#each results as card}
        <div class="card">
            <img 
                alt="{card.name}" 
                aria-label="Card art for { card.title }" 
                src="cards/{ card.image }" />
        </div>
    {/each}
</span>

<style>
    .search {
        width: 100%;
        padding: 0;
        margin: 0;
        height: 4vh;
        font-size: 3vh;
    }

    .card {
        width: 250px;
        height: 350px;
        float: left;
        border-radius: 12px;
        margin-top: 12px;
        margin-right: 4px;
        background-image: url("back.png");
        background-size: 250px 350px;
        overflow: hidden;
    }

    .card > img {
        width: 100%;
        height: 100%;
        padding: 0px;
        margin: 0px;
    }
</style>