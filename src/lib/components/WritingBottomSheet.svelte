<script lang="ts">
	import { showBottomSheet } from "$lib/store/modalStore";

	let { formData, createLetterProcess, isLoading } = $props();

	const handleCloseBottomSheet = () => {
		showBottomSheet.set(false);
	};
</script>

<div class="bottomSheet">
	<div class="bottomSheetContent">
		<div class="bottomSheetText">벽난로 주인이 언제 편지를 읽었으면 좋겠어요?</div>
		<input
			type="date"
			placeholder="날짜 입력"
			class="dateCustomInput"
			bind:value={formData.openAt}
		/>
		<div class="sheetBtnContainer">
			<button class="sheetCloseBtn" onclick={handleCloseBottomSheet}>닫기</button>
			<button class="sheetSubmitBtn" onclick={createLetterProcess} disabled={isLoading}>확인</button
			>
		</div>
	</div>
</div>

<style>
	.bottomSheet {
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: flex-end;
	}
	.bottomSheetContent {
		width: 100%;
		height: 400px;
		background: white;
		border-radius: 20px 20px 0 0;
		padding: 30px 50px;
		text-align: center;
		display: flex;
		flex-direction: column;
		animation: slideUp 0.3s ease-out;
	}

	.bottomSheetText {
		font-size: 16px;
		margin: 20px 0 50px 0;
	}

	.dateCustomInput {
		appearance: none;
		-webkit-appearance: none;
		width: 100%;
		height: 45px;
		padding: 10px;
		margin: 10px 0;
		font-size: 16px;
		border: none;
		box-shadow: 2px 4px 10px 0 rgba(0, 0, 0, 0.25);
		border-radius: 5px;
		background-color: white;
		color: black;
	}

	.dateCustomInput:focus {
		outline: none;
	}

	.sheetBtnContainer {
		display: flex;
		margin-top: auto;
		gap: 20px;
	}

	.sheetSubmitBtn,
	.sheetCloseBtn {
		flex: 1;
		height: 40px;
		font-size: 16px;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		color: #000;
		background-color: #dcdcdc;
	}

	.sheetSubmitBtn {
		background: #ffe51e;
		border: none;
	}

	.sheetSubmitBtn:disabled {
		background-color: #dcdcdc;
	}

	@keyframes slideUp {
		from {
			transform: translateY(100%);
		}
		to {
			transform: translateY(0);
		}
	}
</style>
