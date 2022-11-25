<script>
    import Character from './lib/character.svelte';

    let characters = [],
        page = 1;

    const loadCharacters = async _=>{
        const peticion = `https://rickandmortyapi.com/api/character?page=${page}`,
            response = await fetch(peticion),
            data = await response.json();

        characters = data.results;
    },

    nextPage = _=>{
        page++;
        loadCharacters();
    },

    peviusPage = _=>{
        page--;
        loadCharacters();
    }; 

    loadCharacters();

</script>

<h1 class="title">Rick And Morty Svelte</h1>

<div class="container">
    <div class="btns">
        <button class="btn" on:click={peviusPage} disabled={page===1} > 
                Previus 
        </button>
        <button class="btn">
            {page}
        </button>
        <button class="btn" on:click={nextPage}  disabled={page===42}>
                Next 
        </button>
    </div>


    <div class="grid">
        {#each characters as character }
            <Character character={character}></Character>
        {/each}
    </div>
</div>
