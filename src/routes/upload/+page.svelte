<script>
    import { resolve } from '$app/paths';

    let modalOpen = $state(false);
    let uploadKey = $state('');

    async function uploadFiles(event) {

        event.preventDefault();

        const files = event.target.files;
        let selectedFiles = [...files];

        if (!selectedFiles.length) return;

        const formData = new FormData();
        selectedFiles.forEach(file => formData.append('files', file));

        const res = await fetch('https://storage-worker.ryanh41137.workers.dev/upload', {
            method: 'POST',
            body: formData,
        });

        if (!res.ok) {
            console.error('Upload failed', await res.text());
            uploadKey = 'Upload failed. Please try again.';
            modalOpen = true;
            return;
        }

        const data = await res.json();
        console.log('Upload complete', data);

        const key = data.key;

        uploadKey = key;
        modalOpen = true;
    }

    function closeModal() {
        modalOpen = false;
    }
</script>

<a class="inline-flex items-center gap-2 m-4 px-4 py-2 bg-white text-black font-semibold rounded-sm hover:bg-gray-200" href="{resolve('/')}" role="button">
    <svg xmlns="http://www.w3.org/2000/svg" height="40px" viewBox="0 -960 960 960" width="40px" fill="currentColor"><path d="M226.67-186.67h140v-246.66h226.66v246.66h140v-380L480-756.67l-253.33 190v380ZM160-120v-480l320-240 320 240v480H526.67v-246.67h-93.34V-120H160Zm320-352Z"/></svg>
    <span>Home</span>
</a>

<form class="p-4">
    <div class="flex items-center justify-center w-full">
        <label for="dropzone-file" class="flex flex-col items-center justify-center w-full h-64 bg-neutral-secondary-medium rounded-md border border-dashed border-default-strong rounded-base cursor-pointer hover:bg-neutral-tertiary-medium">
            <div class="flex flex-col items-center justify-center text-body pt-5 pb-6">
                <svg class="w-8 h-8 mb-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h3a3 3 0 0 0 0-6h-.025a5.56 5.56 0 0 0 .025-.5A5.5 5.5 0 0 0 7.207 9.021C7.137 9.017 7.071 9 7 9a4 4 0 1 0 0 8h2.167M12 19v-9m0 0-2 2m2-2 2 2"/></svg>
                <p class="mb-2 text-sm"><span class="font-semibold">Click to upload</span> or drag and drop</p>
                <p class="text-xs">(MAX. 100MB)</p>
            </div>
            <input id="dropzone-file" type="file" class="hidden" multiple onchange={uploadFiles}/>
        </label>
    </div>
</form>

{#if modalOpen}
    <div class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 p-4">
        <div class="w-full max-w-md rounded-lg bg-white p-6 shadow-lg">
            <h3 class="mb-4 text-xl font-semibold">Upload Complete</h3>
            <p class="text-lg mb-4 font-normal text-gray-700">Copy down the following key to access your files:</p>
            <p class="mb-6 text-center text-xl font-semibold text-black bg-gray-200 rounded-md p-2">{`${uploadKey.substring(0, 4)} ${uploadKey.substring(4, 8)}`}</p>
            <button class="inline-flex items-center justify-center rounded bg-gray-200 px-4 py-2 text-sm font-medium text-black hover:bg-gray-300" onclick={closeModal}>Close</button>
        </div>
    </div>
{/if}