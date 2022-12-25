<script>
    import PersonInfo from "./lib/PersonInfo.svelte";

    let todo;
    export let todos = [
        {
            id: "3d12e585-3a5d-4c37-bacc-484e9fdb557f",
            content: "Make a Svelte Project",
            isComplete: false,
        },
    ];

    const handleEnter = (key) => {
        if (key.keyCode !== 13) return;
        todos = [
            ...todos,
            {
                id: crypto.randomUUID(),
                content: todo,
                isComplete: false,
            },
        ];
        todo = "";
    };

    let me = {
        name: "Gökhan Tanrıverdi",
        nickname: "GhostKozak",
        website: "https://www.kozak.work",
        discord: "GhostKozak#0722",
        github: "https://github.com/GhostKozak",
    };
</script>

<main class="flex justify-center items-center h-full">
    <div class="max-w-xl w-full">
        <div class="flex flex-col mb-10">
            <label for="todoInput" class="mb-4 text-2xl">Add Todo:</label>
            <input
                type="text"
                id="todoInput"
                class="w-full rounded mt-1 p-3 outline-none bg-gray-700 focus:bg-gray-800 transition-all text-white placeholder:text-white placeholder:opacity-60"
                on:keydown={handleEnter}
                bind:value={todo}
                placeholder="🛒 Buy a 💻 from 🏪"
            />
        </div>
        <div class="max-h-96 h-full">
            <h2 class="text-2xl mb-4">Todos:</h2>
            {#each todos as todo (todo.id)}
                <div
                    data-index={todo.id}
                    class={`border relative border-gray-400/80 rounded p-2 mb-1 flex ${
                        todo.isComplete ? "bg-green-200 text-black" : ""
                    } `}
                >
                    {#if todo.isComplete}
                        <s>{todo.content}</s>
                    {:else}
                        {todo.content}
                    {/if}
                    <label
                        for="todoCheck{todo.id}"
                        class="absolute w-full h-full left-0 top-0 z-10 cursor-pointer"
                    />
                    <input
                        class="form-check-input appearance-none h-4 w-4 border border-gray-300 rounded-sm bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 my-1 align-top bg-no-repeat bg-center bg-contain float-left cursor-pointer ml-auto mr-2 hidden"
                        type="checkbox"
                        value=""
                        id="todoCheck{todo.id}"
                        bind:checked={todo.isComplete}
                    />
                </div>
            {/each}
            <div class="mt-10">
                <PersonInfo {...me} />
            </div>
        </div>
    </div>
</main>

<style>
    :global(html),
    :global(body),
    :global(#app) {
        @apply bg-slate-900 h-full text-white;
    }
</style>
