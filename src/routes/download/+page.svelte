<script>
    import { resolve } from '$app/paths';
    import download from 'downloadjs';


    const bucketUrl = 'https://pub-740f74e568c24c05b51521b9256abbfb.r2.dev/';


    async function downloadFiles(key) {

        let fileList = await fetch(`https://storage-worker.ryanh41137.workers.dev/files/${key}`);
        fileList = await fileList.json();
        fileList = fileList.files;
        fileList.forEach(file => {
            const fileUrl = bucketUrl + file;
            download(fileUrl);
        });
    }

    function submitKey(event) {
        event.preventDefault();
        if (confirm("These file(s) might be dangerous! Would you like to proceed?")) {
            let key = event.target.elements.key.value.trim();
            // Prevent human error by replacing common mistakes in the key
            key = key.replace(' ', '');
            key = key.replace('I', '1');
            key = key.toUpperCase();
            downloadFiles(key);
        } else {
            alert("Download cancelled.");
        }
    }

</script>

<a class="inline-flex items-center gap-2 m-4 px-4 py-2 bg-white text-black font-semibold rounded-sm hover:bg-gray-200" href="{resolve('/')}" role="button">
    <svg xmlns="http://www.w3.org/2000/svg" height="40px" viewBox="0 -960 960 960" width="40px" fill="currentColor"><path d="M226.67-186.67h140v-246.66h226.66v246.66h140v-380L480-756.67l-253.33 190v380ZM160-120v-480l320-240 320 240v480H526.67v-246.67h-93.34V-120H160Zm320-352Z"/></svg>
    <span>Home</span>
</a>

<div class="flex items-center justify-center p-4 m-4">
    <form class="h-60 w-96 rounded-md border p-4 mb-2" onsubmit={submitKey}>
        <h2 class="text-2xl font-semibold text-heading mb-2">Download Files</h2>
        <p class="text-body mb-2">Enter the key to download your files.</p>
        <div class="relative z-0 w-full mb-6 group">
            <input type="text" name="key" id="key" class="block py-2.5 px-0 w-full text-sm text-heading uppercase font-semibold bg-transparent border-0 border-b-2 border-default-medium appearance-none focus:outline-none focus:ring-0 focus:border-brand peer" placeholder=" " required />
            <label for="key" class="absolute text-sm text-body duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-left peer-focus:start-0 peer-focus:text-fg-brand peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6 rtl:peer-focus:translate-x-1/4 rtl:peer-focus:left-auto">Key</label>
        </div>
        <button type="submit" class="text-body cursor-pointer bg-neutral-secondary-medium box-border border border-default-medium hover:bg-neutral-tertiary-medium hover:text-heading focus:ring-4 focus:ring-neutral-tertiary shadow-xs font-medium leading-5 rounded-full text-sm px-4 py-2.5 focus:outline-none">Download</button>
    </form>
</div>