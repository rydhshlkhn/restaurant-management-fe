<script>
    import axios from 'axios';
    import {onMount} from 'svelte'
    let menus = []

    async function get_menu() {
        var data = JSON.stringify({
        "Name": "MINUNMAN",
        "Category": "Minuman",
        "startDate": "2023-01-01",
        "endDate": "2050-12-31"
        });

        var config = {
        method: 'get',
        url: 'http://localhost:8001/menu',
        headers: { 
            'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2OTA1MzU4NTQsInJvbGUiOiJhZG1pbiIsInVzZXJuYW1lIjoicnlkaCJ9.5wTyDaHO_eTHwmit4-XElq-VD4p0yXwp1f4MUP_oWDI', 
            'Content-Type': 'application/json'
        }
        };

        axios(config)
            .then(function (response) {
                menus = response.data.data
                console.log(response.data.data);
            })
            .catch(function (error) {
                console.log(error);
            });

    }

    onMount(async() => {
        await get_menu()
    })
</script>

<div>
    <button on:click={get_menu}>Get Menu</button>
    <table border="1">
        <tr>
            <th>Name</th>
            <th>Role</th>
        </tr>
        {#each menus as menu}
        <tr>
            <td>{menu.id}</td>
            <td>{menu.name}</td>
        </tr>
        {/each}
    </table>
</div>