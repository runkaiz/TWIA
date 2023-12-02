<script>
	import Showcase from '$lib/Showcase.svelte';
	import Link from '$lib/Link.svelte';
	import example from '$lib/assets/example.jpeg';

	import { HighlightAuto, LineNumbers } from 'svelte-highlight';
	import 'svelte-highlight/styles/a11y-light.css';

	let langAttribute = `<p lang="en-GB">British English</p>`;
	let unstyledList = `<ul role="list">
	<li>One</li>
	<li>Two</li>
	<li>Three</li>
</ul>`;
	let autofocus = `<!-- Use cautiously! -->
<input name="q" autofocus />`;
	let altText = `<img alt="describe the image"></img>`;
	let button = `<button aria-pressed="true||false">
	Toggle
</button>`;

	let buttonPressed = false;
</script>

<svelte:head>
	<title>This Website Is Accessible</title>
</svelte:head>

<div class="container mx-auto p-6">
	<h1 class="text-4xl font-bold mb-4">This Website is Accessible</h1>
	<p class="mb-6">
		Welcome to my website showcasing several web accessibility features and implementations for web
		developers.
	</p>

	<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
		<Showcase title="High Contrast" reference="https://webaim.org/blog/wcag-2-0-and-link-colors/">
			<p>
				Use WCAG compliant color palettes to improve readability. All code snippets on the website
				uses <Link to="https://github.com/ericwbailey/a11y-syntax-highlighting">a11y-light</Link>.
				You should have a 4.5:1 contrast between the text color and the background. As well as a 3:1
				contrast between the link text color and the surrounding non-link text color.
			</p>
			<ul class="list-disc pl-6">
				<li>4.5:1 contrast between the non-link text color and the background.</li>
				<li>4.5:1 contrast between the link text color and the background.</li>
				<li>3:1 contrast between the link text color and the surrounding non-link text color.</li>
			</ul>
		</Showcase>

		<Showcase
			title="Explicit Language Attribute"
			reference="https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang#accessibility"
		>
			<p>
				Specifying the intended language of the content of your website can help screen readers
				pronunciate more accurately.
			</p>
			<HighlightAuto code={langAttribute} let:highlighted>
				<LineNumbers {highlighted} wrapLines />
			</HighlightAuto>
		</Showcase>

		<Showcase title="Keyboard Navigation">
			<p>
				Although you want your website to respect the accessibility features provided by the
				operating system. Implement custom keyboard navigation to help users who can't use
				pointer-based input if navigating your website is unreliable without one.
			</p>
			<p>
				For example, you should be able to scroll with arrow keys on this page, that is default
				behavior, meaning people will expect this to happen when they press arrow keys. It can be
				confusing if it is rebinded to some other functionality.
			</p>
		</Showcase>

		<Showcase
			title="Autofocus"
			reference="https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/autofocus"
		>
			<p>
				Autofocus is often used in conjunction with forms and is performed the moment the user loads
				into the page. While autofocus spares users from an extra click and directs them to a
				starting location of your choice, visitors with screen readers might find it difficult to
				orient themselves within the layouts of your website as the focus changes without warning.
			</p>
			<HighlightAuto code={autofocus} let:highlighted>
				<LineNumbers {highlighted} wrapLines />
			</HighlightAuto>
		</Showcase>

		<Showcase
			title="Unstyled List Quirks"
			reference="https://gerardkcohen.me/writing/2017/voiceover-list-style-type.html"
		>
			<p>
				Unstyled lists are not announced as lists by VoiceOver, you can fix this by specifying a
				role.
			</p>
			<HighlightAuto code={unstyledList} let:highlighted>
				<LineNumbers {highlighted} wrapLines />
			</HighlightAuto>
			<p>Which would render and appear as:</p>
			<ul role="list">
				<li>One</li>
				<li>Two</li>
				<li>Three</li>
			</ul>
		</Showcase>

		<Showcase
			title="Text Alternatives for Images"
			reference="https://www.w3.org/WAI/tutorials/images/"
		>
			<p>
				Images can be productive representations of information, so it is not recommanded to remove
				images for the sake of accessibility. Instead, provide detailed explanations of the images
				so that it can be read by a screen reader or transcribed into Braille.
			</p>
			<HighlightAuto code={altText} let:highlighted>
				<LineNumbers {highlighted} wrapLines />
			</HighlightAuto>
			<img
				alt="a concrete road in between two long rows of bushes and trees with golden leaves underneath the sun."
				src={example}
			/>
			<p class="aria-hidden">
				Alt Text: a concrete road in between two long rows of bushes and trees with golden leaves
				underneath the sun.
			</p>
		</Showcase>
		<Showcase title="Avoid Visual-Dependent Elements">
			<p>
				Most screen readers do not react when content changes dynamically. Additionally, for toggle
				buttons such as the one below, do not update the text within the buttons at all.
			</p>
			<p>Please never do something like this.</p>
			<div>
				<span>
					<button
						class="	py-2
								px-4
								bg-blue-500
								text-white
								rounded-full
								hover:bg-blue-700
								active:bg-blue-900
								focus:outline-none"
						on:click={() => {
							buttonPressed = !buttonPressed;
						}}
						aria-pressed={buttonPressed}>Toggled {buttonPressed}</button
					>
					{#if buttonPressed}
						✅
					{:else}
						❌
					{/if}
				</span>
			</div>
			<p>At the very least specify an aria attribute to indicate the state.</p>
			<HighlightAuto code={button} let:highlighted>
				<LineNumbers {highlighted} wrapLines />
			</HighlightAuto>
		</Showcase>
		<Showcase title="Text Readability" reference="https://github.com/antijingoist/opendyslexic">
			<p>
				Ensure that visitors to your site can read everything with ease. Choose a font with
				readability in mind, although most default fonts provided by browsers can fulfill that role.
			</p>
			<p>
				Certain fonts may help users with dyslexia, such as OpenDyslexic under the SIL-OFL license.
			</p>
			<p id="opendyslexic">The quick brown fox jumps over the lazy dog</p>
		</Showcase>
	</div>
</div>

<style>
	@font-face {
		font-family: 'OpenDyslexic';
		font-style: normal;
		src: local('OpenDyslexic-Regular'), local('opendyslexic-regular'), local('OpenDyslexic Regular'),
			local('opendyslexic regular'), url('/fonts/OpenDyslexic/OpenDyslexic-Regular.otf');
	}

	#opendyslexic {
		font-family: 'OpenDyslexic';
	}
</style>
