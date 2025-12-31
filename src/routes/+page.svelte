<!-- +page.svelte -->
<script lang="ts">
	import AvatarComponent from '../lib/components/avataaar/avatarComponent.svelte';
	import { allStyles } from '../lib/components/avataaar/options/options.js';

	// Avatar style
	let avatarStyle = $state('Circle');

	// Get styles for each option
	const getStyles = (optionKey: string): string[] => {
		const option = allStyles.find((s) => s.option === optionKey);
		return option?.styles || [];
	};

	// Initialize state with default values
	let topType = $state('ShortHairSides');
	let accessoriesType = $state('Blank');
	let hairColor = $state('Auburn');
	let facialHairType = $state('Blank');
	let facialHairColor = $state('');
	let clotheType = $state('Hoodie');
	let clotheColor = $state('Red');
	let graphicType = $state('');
	let eyeType = $state('Squint');
	let eyebrowType = $state('UpDown');
	let mouthType = $state('Sad');
	let skinColor = $state('Light');
	let backgroundColor = $state('none'); // Default: transparent (original: '#65C9FF')

	let blobUrl: string = $state('');

	export function getBlob(blob: Blob) {
		console.log('Blob received:', blob, blobUrl);
	}

	$effect(() => {
		if (blobUrl) {
			console.log('Blob URL:', blobUrl);
		}
	});
</script>

<svelte:head>
	<title>Avatar Editor - Test Page</title>
	<style>
		:global(body) {
			margin: 0;
			padding: 0;
			font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
				Cantarell, sans-serif;
			background: #f5f5f5;
		}
		.container {
			max-width: 1400px;
			margin: 0 auto;
			padding: 20px;
		}
		.header {
			text-align: center;
			margin-bottom: 30px;
		}
		.header h1 {
			margin: 0 0 10px 0;
			color: #333;
		}
		.content {
			display: grid;
			grid-template-columns: 300px 1fr;
			gap: 30px;
		}
		.editor-panel {
			background: white;
			border-radius: 8px;
			padding: 20px;
			box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
			height: fit-content;
			position: sticky;
			top: 20px;
		}
		.editor-panel h2 {
			margin: 0 0 20px 0;
			font-size: 18px;
			color: #333;
			border-bottom: 2px solid #eee;
			padding-bottom: 10px;
		}
		.control-group {
			margin-bottom: 20px;
		}
		.control-group label {
			display: block;
			margin-bottom: 8px;
			font-weight: 500;
			font-size: 14px;
			color: #555;
		}
		.control-group select {
			width: 100%;
			padding: 8px 12px;
			border: 1px solid #ddd;
			border-radius: 4px;
			font-size: 14px;
			background: white;
			cursor: pointer;
		}
		.control-group select:hover {
			border-color: #999;
		}
		.control-group select:focus {
			outline: none;
			border-color: #4a90e2;
			box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.1);
		}
		.preview-panel {
			background: white;
			border-radius: 8px;
			padding: 40px;
			box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			min-height: 600px;
		}
		.preview-panel h2 {
			margin: 0 0 30px 0;
			color: #333;
		}
		.avatar-container {
			display: flex;
			justify-content: center;
			align-items: center;
			background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
			border-radius: 12px;
			padding: 40px;
			box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
		}
		.style-toggle {
			display: flex;
			gap: 10px;
			margin-bottom: 20px;
		}
		.style-toggle button {
			flex: 1;
			padding: 10px;
			border: 2px solid #ddd;
			background: white;
			border-radius: 4px;
			cursor: pointer;
			font-size: 14px;
			transition: all 0.2s;
		}
		.style-toggle button:hover {
			border-color: #4a90e2;
		}
		.style-toggle button.active {
			background: #4a90e2;
			color: white;
			border-color: #4a90e2;
		}
	</style>
</svelte:head>

<div class="container">
	<div class="header">
		<h1>🎨 Avatar Editor</h1>
		<p>Customize your avatar with all available options</p>
	</div>

	<div class="content">
		<div class="editor-panel">
			<h2>⚙️ Controls</h2>

			<div class="control-group">
				<label>Avatar Style</label>
				<div class="style-toggle">
					<button
						class={avatarStyle === 'Circle' ? 'active' : ''}
						onclick={() => (avatarStyle = 'Circle')}
					>
						Circle
					</button>
					<button
						class={avatarStyle === 'Transparent' ? 'active' : ''}
						onclick={() => (avatarStyle = 'Transparent')}
					>
						Transparent
					</button>
				</div>
			</div>

			<div class="control-group">
				<label>🎨 Background Color</label>
				<input
					type="text"
					bind:value={backgroundColor}
					placeholder="none or #65C9FF"
					style="width: 100%; padding: 8px 12px; border: 1px solid #ddd; border-radius: 4px; font-size: 14px; box-sizing: border-box;"
				/>
				<small style="display: block; margin-top: 4px; color: #666; font-size: 12px;">
					Enter "none" for transparency (default) or a color (e.g., #65C9FF, #FF0000)
				</small>
			</div>

			<div class="control-group">
				<label>👤 Top Type</label>
				<select bind:value={topType}>
					{#each getStyles('topType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>💈 Hair Color</label>
				<select bind:value={hairColor}>
					<option value="">None</option>
					{#each getStyles('hairColor') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>👓 Accessories</label>
				<select bind:value={accessoriesType}>
					{#each getStyles('accessoriesType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>🧔 Facial Hair Type</label>
				<select bind:value={facialHairType}>
					{#each getStyles('facialHairType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>✂️ Facial Hair Color</label>
				<select bind:value={facialHairColor}>
					<option value="">None</option>
					{#each getStyles('facialHairColor') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>👔 Clothes</label>
				<select bind:value={clotheType}>
					{#each getStyles('clotheType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>🎨 Clothes Color</label>
				<select bind:value={clotheColor}>
					{#each getStyles('clotheColor') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>🎨 Graphic</label>
				<select bind:value={graphicType}>
					<option value="">None</option>
					{#each getStyles('graphicType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>👁 Eyes</label>
				<select bind:value={eyeType}>
					{#each getStyles('eyeType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>✏️ Eyebrow</label>
				<select bind:value={eyebrowType}>
					{#each getStyles('eyebrowType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>👄 Mouth</label>
				<select bind:value={mouthType}>
					{#each getStyles('mouthType') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>

			<div class="control-group">
				<label>🎨 Skin Color</label>
				<select bind:value={skinColor}>
					{#each getStyles('skinColor') as style}
						<option value={style}>{style}</option>
					{/each}
				</select>
			</div>
		</div>

		<div class="preview-panel">
			<h2>Preview</h2>
			<div class="avatar-container">
				<AvatarComponent
					bind:blobUrl
					{getBlob}
					{avatarStyle}
					{topType}
					{accessoriesType}
					{hairColor}
					{facialHairType}
					{facialHairColor}
					{clotheType}
					{clotheColor}
					{graphicType}
					{eyeType}
					{eyebrowType}
					{mouthType}
					{skinColor}
					{backgroundColor}
					style="width: 400px; height: 400px;"
				/>
			</div>
		</div>
	</div>
</div>
