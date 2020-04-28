<template>
	<div class="container-fluid">
		<div class="row">
			<main role="main" class="col-md-12 ml-sm-auto col-lg-12 pt-3 px-4">
				<div class="container">
					<div class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pb-2 mt-3 ">
						<h4 class="mb-3">New row</h4>
						<div class="btn-toolbar mb-2 mb-md-0">
							<router-link to="/"  class="btn btn-sm mr-1 btn-outline-secondary">
								Back
							</router-link>
							<a 	href="https://docs.google.com/spreadsheets/d/1oLGI1u68sPh-P1yhWaU7j_WUTHjFMY1aUu6uINfTb0Q/edit?usp=sharing" 
								class="btn btn-sm btn-outline-secondary"
								target="_blank">
							View Google Sheet
							</a>
						</div>
					</div>
					<div v-if="showMsg" class="alert alert-success alert-dismissible fade show" role="alert">
						{{message}}
						<button type="button" class="close" data-dismiss="alert" aria-label="Close">
							<span aria-hidden="true">&times;</span>
						</button>
					</div>
					<div class="col-md-12 order-md-1">
						<form @submit.prevent="addRow">
							<div class="row">
								<div class="col-md-6 mb-3">
									<label for="name">Name</label>
									<input type="text" v-model="name" class="form-control" id="name" placeholder="First &amp; Last Name" required>
								</div>
								<div class="col-md-6 mb-3">
									<label for="phone">Phone</label>
									<input type="text" v-model="phone" class="form-control" id="phone" required>
								</div>
								<div class="col-md-6 mb-3">
									<label for="address">Address</label>
									<input type="text" v-model="address" class="form-control" id="address" placeholder="1234 Main St" required>
								</div>
								<div class="col-md-4 mb-3">
									<label for="city">City</label>
									<input type="text" v-model="city" class="form-control" id="city" placeholder="ex: Algiers" required>
								</div>
								<div class="col-md-2 mb-3">
									<label for="zip">Zip</label>
									<input type="text" v-model="zip" class="form-control" id="city" placeholder="ex: 16000" required>
								</div>
								<div class="col-md-6 mb-3">
									<label for="activity">Activity</label>
									<select v-model="activity" class="custom-select d-block w-100" id="activity" required>
										<option value="">Choose...</option>
										<option value="Painter">Painter</option>
										<option value="Plumber">Plumber</option>
									</select>
								</div>
								<div class="col-md-6">
									<label for="">.</label>
									<button class="btn btn-primary btn-block" type="submit">SUBMIT</button>
								</div>
								
							</div>		
						</form>
					</div>

					
				</div>
				
			</main>
		</div>
	</div>
</template>

<script>
	const { GoogleSpreadsheet } = require('google-spreadsheet');
	const creds = require('@/client_secret.json');
	export default {
		name: "AddRow",
		data() {
			return {
				name: '',
				phone: '',
				address: '',
				city: '',
				zip: '',
				activity: '',
				showMsg : false,
				message: '',
			}
		},
		methods: {
			async addRow() {
				const newRow = {
					name: this.name,
					phone: this.phone,
					address: this.address,
					city: this.city,
					zip: this.zip,
					activity: this.activity,
				}

				const doc = new GoogleSpreadsheet('1oLGI1u68sPh-P1yhWaU7j_WUTHjFMY1aUu6uINfTb0Q');
				await doc.useServiceAccountAuth(creds);
				await doc.loadInfo(); 
				const sheet = doc.sheetsByIndex[0];
				await sheet.addRow(newRow);
				
				this.name = '';
				this.phone = '';
				this.address = '';
				this.city = '';
				this.zip = '';
				this.activity = '';

				this.message = "New row added !";
				this.showMsg = true;

				
			}
		}
	}
</script>

<style scoped>

</style>
