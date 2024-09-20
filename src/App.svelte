<script>
    let services = [];
    let name = '';
    let description = '';
    let price = '';
    let editingIndex = -1;

    function addOrUpdateService() {
        if (!name || !description || !price) {
            alert('All fields are required!');
            return;
        }

        const service = { name, description, price: parseFloat(price) };

        if (editingIndex === -1) {
            services.push(service);
        } else {
            services[editingIndex] = service;
            editingIndex = -1;
        }

        resetForm();
    }

    function editService(index) {
        editingIndex = index;
        name = services[index].name;
        description = services[index].description;
        price = services[index].price;
    }

    function deleteService(index) {
        services.splice(index, 1);
    }

    function resetForm() {
        name = '';
        description = '';
        price = '';
    }
</script>

<main>
    <h1>Healthcare Services</h1>
    
    <form on:submit|preventDefault={addOrUpdateService}>
        <input type="text" bind:value={name} placeholder="Service Name" required />
        <input type="text" bind:value={description} placeholder="Description" required />
        <input type="number" bind:value={price} placeholder="Price" required min="0" step="0.01" />
        <button type="submit">{editingIndex === -1 ? 'Add Service' : 'Update Service'}</button>
    </form>
    <ul>
        {#each services as service, index}
            <li>
                <strong>{service.name}</strong> - {service.description} - ${service.price.toFixed(2)}
                <button on:click={() => editService(index)}>Edit</button>
                <button on:click={() => deleteService(index)}>Delete</button>
            </li>
        {/each}
    </ul>
</main>

<style>
    main {
    max-width: 600px;
    margin: auto;
    padding: 2rem;
    background-color: lavender;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

h1 {
    color: #333;
    margin-bottom: 1.5rem;
}

form {
    display: flex;
    flex-direction: column;
    margin-bottom: 2rem;
}

input[type="text"],
input[type="number"] {
    padding: 0.75rem;
    margin: 0.5rem 0;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1rem;
}

button {
    padding: 0.75rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #fff;
    padding: 1rem;
    margin: 0.5rem 0;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

strong {
    color: #333;
}

</style>
