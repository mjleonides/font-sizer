<template>
	<div class="layout">
		<form>
			<div id="converter">
				<label for="converter-px">
					<input
						id="converter-px"
						type="number"
						v-model="inputPx"
						@input="updater('inputPx')" />
					px
				</label>
				<span class="equal">=</span>
				<label for="converter-rem">
					<input
						id="converter-rem"
						type="number"
						v-model="inputRem"
						@input="updater('inputRem')" />
					rem
				</label>
			</div>
			<label for="root-element-size">
				Root element size
				<input
					id="root-element-size"
					type="number"
					v-model="rootElementSize"
					@input="updater('rootElementSize')" />
				px
			</label>
		</form>
		<table id="common-table"></table>

		<div class="footer">
			<p>
				Crafted by
				<a href="https://leonides.dev" target="_blank">leonides.dev</a>
			</p>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			rootElementSize: 16,
			inputPx: 16,
			inputRem: 1
		};
	},
	mounted() {
		this.renderTable();
	},
	methods: {
		updater(changedVar) {
			if (changedVar === "inputPx") {
				this.inputRem = this.inputPx / this.rootElementSize;
			} else if (changedVar === "inputRem") {
				this.inputPx = this.inputRem * this.rootElementSize;
			} else if (changedVar === "rootElementSize") {
				this.inputRem = this.inputPx / this.rootElementSize;
			}
			this.renderTable();
		},
		renderTable() {
			let table = document.querySelector("#common-table");
			let tablebody = document.createElement("tbody");

			table.innerHTML = "";

			for (let i = 4; i < 33; i = i + 2) {
				let rem = i / this.rootElementSize;
				let row = `<tr>
            <td>${i}px</td><td class="equal">=</td>
            <td>${rem}rem</td>
        </tr>`;
				tablebody.insertAdjacentHTML("beforeend", row);
			}

			table.append(tablebody);
		}
	}
};
</script>

<style lang="scss">
$dark: #1f1f1f;
$light: #f7f9f9;
$faded: #f7f7f73f;

body {
	background-color: $dark;
	color: $light;
	font-size: 1.5rem;
	margin: 0;
	padding: 0;
}

.layout {
	display: flex;
	flex-direction: column;
	height: 100vh;
	justify-content: space-between;
	align-items: center;
}

form {
	margin: 5rem auto 1rem;
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 2rem;
	text-align: center;

	#converter {
		display: flex;
		align-items: center;
		text-align: center;
	}

	input {
		font-size: larger;
		background-color: $dark;
		color: $light;
		text-align: center;
		border: none;
		border-bottom: dotted 1px $faded;
		max-width: 15vmax;
	}
}

table {
	margin: 0 auto;

	tbody {
		display: grid;
		gap: 0.4rem;
	}
}

.equal {
	padding: 0 0.3rem;
	color: $faded;
}

.footer {
	color: grey;
	font-size: 0.75rem;

	a {
		color: white;
	}
}
</style>
