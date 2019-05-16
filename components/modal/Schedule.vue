<template>
	<div :class="[ openModal ? 'is-active' : '', 'modal' ]">
		<div class="modal-background"></div>
		<div class="modal-card">
			<header class="modal-card-head">
				<p class="modal-card-title">{{ modalTitle }}</p>
				<button class="delete" aria-label="close" @click="closeModal(false)"></button>
			</header>
			<section class="modal-card-body">
		
				<v-flex xs12 sm6 d-flex>
				<v-select :items="items" label="Hora de inicio"></v-select>
				</v-flex>
				<v-flex xs12 sm6 d-flex>
				<v-select :items="items" label="Hora de inicio"></v-select>
				</v-flex>
      			</v-layout> 
			</section>
		</div>
	</div>
</template>

<script>
export default {
	name: 'checkout',
    
	data () {
		return {
			modalTitle: 'Carrito de reservas',
			items:['00:00', '00:30', '01:00', '01:30','02:00','02:30','03:00','03:30','04:00',
			'04:30','05:00','05:30','06:00','06:30','07:00','07:30','08:00','08:30','09:00','09:30',
			'10:00','10:30','11:00', '11:30','12:00','12:30','13:00','13:30','14:00',
			'14:30','15:00','15:30','16:00','16:30','17:00','17:30','18:00','18:30','19:00','19:30',
			'20:00','20:30','21:00','21:30','22:00','22:30','23:00','23:30','24:00']

		}
	},

	computed: {
			openModal () {
				if (this.$store.getters.isReserve) {
					return true;
				} else {
					return false;
				}
			},
		isUserLoggedIn () {
			return this.$store.getters.isUserLoggedIn;
		}
	},

	methods: {
		closeModal (reloadPage) {
			this.$store.commit('showReserve', false);

			if (reloadPage) {
				window.location.reload();
			}
		},
		onNextBtn () {
			if (this.isUserLoggedIn) {
				this.isCheckoutSection = true;
			} else {
				this.$store.commit('showReserve', false);
				this.$store.commit('showLoginModal', true);
			}
		},
		onPrevBtn () {
			this.isCheckoutSection = false;
		}
	}
}
</script>

