<script lang="ts">
	import { showBottomSheet } from "$lib/store/modalStore";
	let url: string = window.location.href;

	const handleCloseBottomSheet = () => {
		showBottomSheet.set(false);
	};

	const copyLink = async () => {
		try {
			await window.navigator.clipboard.writeText(window.location.href);
			alert("링크가 복사되었습니다 :)");
		} catch (err) {
			alert("복사에 실패했습니다 :(");
			console.error(err);
		} finally {
			handleCloseBottomSheet();
		}
	};
</script>

<div class="bottomSheet">
	<div class="bottomSheetContent">
		<div class="bottomSheetText">나의 벽난로 링크</div>
		<div class="linkBox" onclick={copyLink} onkeydown={() => {}} tabindex="0" role="button">
			{url}
		</div>
		<div class="desc">공유 시 『인스타 (스토리) 친한친구』 로만 부탁드립니다.</div>
		<div class="sheetBtnContainer">
			<button class="sheetCloseBtn" onclick={handleCloseBottomSheet}>닫기</button>
			<button class="sheetSubmitBtn" onclick={copyLink}>링크 복사</button>
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
		z-index: 2;
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

	.linkBox {
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
		align-content: center;
		overflow: scroll;
		white-space: nowrap;
	}

	.desc {
		margin-top: 16px;
		color: rgb(216, 83, 83);
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

	@keyframes slideUp {
		from {
			transform: translateY(100%);
		}
		to {
			transform: translateY(0);
		}
	}
</style>
