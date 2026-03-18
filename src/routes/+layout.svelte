<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Storage Share</title>
	<meta name="description"
    content="A simple app for uploading and sharing files in the cloud" />
	<meta name="keywords" content="file sharing, cloud storage, upload, download" />
	<meta name="author" content="mrryanperson" />
</svelte:head>
{@render children()}
