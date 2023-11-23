<script>
    export let list_member
</script>

<div>
    <table border="1">
        <tr>
            <th>Name</th>
            <th>Role</th>
        </tr>
        {#each list_member as {name, role}}
        <tr>
            <td>{name}</td>
            <td>{role}</td>
        </tr>
        {/each}
    </table>
</div>