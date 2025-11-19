<script>
    let todoItem = $state('');
    let todoDate = $state();
    let todoList = $state([]);
    let todayDate = Math.floor(new Date().getTime() / 1000);
    $inspect(todayDate);

    // add todoItem to todoList
    function addItem(event) {
        event.preventDefault();
        if (todoItem.trim().length === 0) {
            return;
        }
        let itemDueDate = Math.floor(new Date(todoDate).getTime() / 1000);
        console.log(itemDueDate);
        todoList = [...todoList, {
            text: todoItem,
            dueDate: itemDueDate,
            done: false
        }];
        todoItem = '';
    }

    // remove todoItem from todoList
    function removeItem(index) {
        todoList.splice(index,1);
    }

    function calculateDelta(date1, date2) {
        return Math.round((date2 - date1) / 86400);
    }

</script>

    <form onsubmit={addItem}>
        <input type="text" bind:value={todoItem}>
        <input type="date" bind:value={todoDate}>
        <button type="submit">Add</button>
    </form>

    <div class="todo-list">
        <ul>
            {#each todoList as item, index}
                <li>
                    <input type="checkbox" bind:checked={item.done}>
                    <span class:done={item.done}>{item.text}: due in {calculateDelta(todayDate, item.dueDate)} days</span>
                    <button type="button" onclick={() => removeItem(index)}>&times;</button>
                </li>
            {/each}
        </ul>
    </div>



<style>
    ul {
        list-style: none;
    }
    input[type="checkbox"] {
        height: 20px;
        width: 20px;
        accent-color: green;

    }
    li span.done {
        text-decoration: line-through;
        color: grey;
    }
</style>