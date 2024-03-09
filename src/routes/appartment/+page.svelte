<script>
    import { PUBLIC_BASE_URL } from '$env/static/public';
    import axios from "axios";

    let rooms;
    let area;
    let luxurious = 0; // Set default value to false

    let price = '...';

    function handleSubmit() {
        // Update luxurious value based on checkbox state
        luxurious = document.querySelector('input[type=checkbox]').checked ? 1 : 0;

        let url =
            PUBLIC_BASE_URL +
            "/api/predict/?luxurious=" +
            luxurious +
            "&area=" +
            area +
            "&rooms=" +
            rooms;
        console.log(url);
        axios.get(url).then((response) => {
            price = 'CHF ' + response.data;
        });
    }
</script>

<div class="container text-center">
    <h1>Are you paying too much?</h1>
    <p>Our model predicts that you should be paying <b>{price}</b></p>
    <div class="row justify-content-md-center">
        <div class="col col-lg-2">
            <input type="number" class="form-control" placeholder="Area" aria-label="area" bind:value={area}>
        </div>
        <div class="col col-lg-2">
            <input type="number" class="form-control" placeholder="Rooms" aria-label="rooms" bind:value={rooms}>
        </div>
        <div class="col-md-auto">
            <label>
                <input type="checkbox" bind:checked={luxurious}> Luxurious
            </label>
        </div>
        <div class="col-md-auto">
            <button type="button" class="btn btn-primary" on:click={handleSubmit}>Price Estimation</button>
        </div>
    </div>
</div>
