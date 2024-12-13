<script>
    import checkmark from '../../public/checkmark.svg';
</script>

<div class="submit-container">
    <button type = "submit" class="submission-button">
        <img src={checkmark} alt="Checkmark Icon" class="icon" />
    </button>
</div>

<style>
    .submission-button {
        background-color: #06f77e;
        border: 2px solid #000000;
        border-radius: 50%;
        padding: 6px;
        margin: 5px;
    }

    .submit-container {
        flex-direction: row;
    }
</style>