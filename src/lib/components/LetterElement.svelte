<script lang="ts">
	import { goto } from "$app/navigation";
	import { showModal } from "$lib/store/modalStore";
	import { idModal, nameModal } from "$lib/store/passwordStore";
	import { LetterStatus, LetterType, type LetterItem } from "$lib/types/LetterType";
	import LetterPasswordModal from "./LetterPasswordModal.svelte";

	let { id, letter }: { id: string; letter: LetterItem } = $props();

	let src: string = "/images/letterImg.png";
	let privateIcon: string = "/images/privateIcon.png";

	let idSet = $state("");
	let nameSet = $state("");

	const moveDetail = () => {
		goto(`/fireplace/${id}/letterbox/${letter.uuid}`);
	};

	const openPasswordModal = () => {
		showModal.set(true);
	};

	const openLetter = () => {
		idSet = letter.uuid;
		nameSet = letter.name;
		$idModal = idSet;
		$nameModal = nameSet;
		if (letter.status == LetterStatus.CLOSED) {
			alert("편지가 아직 도착하지 않았어요 :(");
			return;
		}

		if (letter.type == LetterType.PUBLIC) {
			moveDetail();
		} else {
			openPasswordModal();
		}
	};
</script>

<div class="letterInner" onclick={openLetter} onkeydown={() => {}} tabindex="0" role="button">
	<div class="letterImgContainer">
		<img {src} alt="편지" />
		<div class="private">
			{#if letter.type === "PRIVATE"}
				<img src={privateIcon} alt="비공개" />
			{/if}
		</div>
	</div>
	<div class="nameText">{letter.name}</div>
	<div class="dayText">
		{#if letter.diffDate <= -10}
			{`${Math.abs(letter.diffDate)}km`}
		{:else if letter.diffDate < 0}
			{`${Math.abs(letter.diffDate)}00m`}
		{:else}
			📨 도착했어요!
		{/if}
	</div>
</div>

<LetterPasswordModal />

<style>
	.letterInner {
		width: 100%;
		min-height: 50px;
		background-color: #fff;
		border-radius: 10px;
		display: flex;
		align-items: center;
		padding: 0 20px;
	}

	.letterImgContainer {
		width: 40px;
		height: 30px;
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.letterImgContainer > img {
		width: 100%;
		height: 100%;
		position: absolute;
	}

	.private {
		position: relative;
		margin-top: 6px;
		z-index: 2;
	}

	.private > img {
		width: 20px;
	}

	.nameText {
		font-size: 20px;
		margin-left: 20px;
	}

	.dayText {
		font-size: 14px;
		margin-left: auto;
	}
</style>
