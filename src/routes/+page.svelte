<script>
    import { periodicTable } from "$lib/table.js";

    const categoryColors = {
        metal: '#B8860B',
        nonmetal: '#2E8B57',
        metalloid: '#CD5C5C',
        transitionMetal: '#4682B4',
        lanthanide: '#556B2F',
        actinide: '#8A2BE2',
        nobleGas: '#FF1493'
    };

    let elementMap = {
        "metal": "Metals",
        "nonmetal": "Non Metals",
        "metalloid": "Metalloids",
        "transitionMetal": "Transition Metals",
        "lanthanide": "Lanthanides",
        "actinide": "Actinides",
        "nobleGas": "Noble Gases"
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500&display=swap');

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        background-color: #121212;
        color: #f0f0f0;
    }

    .title {
        font-family: 'Lexend', sans-serif;

        text-align: center;
        font-size: 2rem;
        margin: 20px 0;
    }

    .periodic-table {
        display: grid;
        grid-template-columns: repeat(18, 1fr);
        gap: 15px;
        padding: 20px;
        justify-items: center;
        width: 100%;
        max-width: 100vw;
        overflow-x: auto;
    }

    .element {
        font-family: 'Lexend', sans-serif;
        border-radius: 12px;
        width: calc(100% - 15px);
        aspect-ratio: 1;
        padding: 10px;
        text-align: center;
        background-color: #2c2c3c;
        color: #ffffff;
        font-size: 1rem;
        transition: background-color 0.3s, transform 0.3s;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: relative;
    }

    .element:hover {
        font-family: 'Lexend', sans-serif;
        background-color: #3b3b5b;
        transform: translateY(-5px);
        cursor: pointer;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    }

    .element strong {
        font-family: 'Lexend', sans-serif;
        display: block;
        font-size: 1.2rem;
        margin-bottom: 5px;
        color: rgb(255, 255, 255);
    }

    .element .atomic-number {
        font-family: 'Lexend', sans-serif;
        font-size: 0.8rem;
        color: #ffffff;
        margin-bottom: 5px;
    }

    .element small {
        font-size: 0.8rem;
        color: #ffffff;
    }

    .element[tooltip]:hover::before {
        font-family: 'Lexend', sans-serif;
        content: attr(tooltip);
        position: absolute;
        bottom: 100%;
        left: 50%;
        transform: translateX(-50%);
        padding: 5px 10px;
        background-color: #2a2a40;
        color: #fff;
        font-size: 0.7rem;
        border-radius: 6px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        white-space: nowrap;
    }

    .element[tooltip]:hover::after {
        font-family: 'Lexend', sans-serif;
        content: "";
        position: absolute;
        bottom: 100%;
        left: 50%;
        transform: translateX(-50%);
        width: 0;
        height: 0;
        border-left: 6px solid transparent;
        border-right: 6px solid transparent;
        border-top: 6px solid #2a2a40;
    }

    .key {
        font-family: 'Lexend', sans-serif;
        margin: 20px;
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
        gap: 10vw;
        text-align: center;
    }

    .key-item {
        font-family: 'Lexend', sans-serif;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .key-color {
        width: 15px;
        height: 15px;
        border-radius: 50%;
        margin-right: 2px;
    }
</style>

<svelte:head>
    <title>
        The Periodic Table
    </title>
</svelte:head>

<div class="title">The Periodic Table</div>

<div class="periodic-table">
    {#each periodicTable as element}
        <div
            class="element"
            style="grid-row: {element.row}; grid-column: {element.column}; background-color: {categoryColors[element.category] || "#2c2c3c"};"
            tooltip="{element.name} ({element.massNumber})"
        >
            <div class="atomic-number">{element.atomicNumber}</div>
            <strong>{element.symbol}</strong>
            <small>{element.massNumber}</small>
        </div>
    {/each}
</div>

<div class="key">
    {#each Object.entries(categoryColors) as [category, color]}
        <div class="key-item">
            <div class="key-color" style="background-color: {color};"></div>
            <span>{elementMap[category]}</span>
        </div>
    {/each}
</div>
