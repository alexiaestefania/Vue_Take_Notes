<template>
    <div class="modal">
        <div class="modal-background"></div>
        <div class="modal-card mt-6">
            <header class="modal-card-head has-background-primary is-outlined ">
                <p class="modal-card-title has-text-white is-family-sans-serif">New note</p>
                <button class="delete" aria-label="close"></button>
            </header>
            <section class="modal-card-body">
                <textarea class="textarea is-primary is-family-sans-serif" name="note" id="note" cols="30" rows="10"
                    placeholder="Write your notes here!"></textarea>
            </section>
            <footer class="modal-card-foot">
                <button class="button is-success"><span class="icon is-small">
                        <i class="bi bi-plus is-size-4"></i>
                    </span>
                    <span class="is-family-sans-serif">Save note</span></button>
            </footer>
        </div>
    </div>
</template>