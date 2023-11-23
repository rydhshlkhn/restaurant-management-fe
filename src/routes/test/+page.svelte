<script>
    import MemberTbl from "../../components/MemberTbl.svelte"

    let name = 'Riyadh'
    let list_member = [
        {
            name: 'riyad',
            role: 'BE',
        },
        {
            name: 'ikhsan',
            role: 'CTO',
        },
        {
            name: 'linda',
            role: 'FE',
        }
    ]
    let list_member_stg = [
        {
            name: 'stg1',
            role: 'BE',
        },
        {
            name: 'stg2',
            role: 'CTO',
        },
        {
            name: 'stg3',
            role: 'FE',
        }
    ]

    function getName() {
        name = 'Ridyadhi Sholikhin'
    }
</script>
<div>
    <h1>Welcome {name} to Menu</h1>
    <p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
    <button on:click={getName}>Get Name</button>
    <!-- <input type="text" placeholder="Name" on:change={e=>name=e.target.value}}> -->
    <input type="text" placeholder="Name" bind:value={name}>

    <MemberTbl list_member={list_member}></MemberTbl>
    <MemberTbl list_member={list_member_stg}></MemberTbl>
    
</div>
