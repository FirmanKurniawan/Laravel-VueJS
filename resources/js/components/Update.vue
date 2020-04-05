<template>
<div class="card">
	<div class="card-header">
		Edit Post
	</div>
	<div class="card-body">
		<form v-on:submit="submitPostEdit()">
			<div class="form-group">
				<input type="text" v-model="posts.title" placeholder="Title" class="form-control">
			</div>
			<div class="form-group">
				<textarea rows="5" v-model="posts.description" placeholder="Description" class="form-control"></textarea>
			</div>
			<div class="form-group">
				<router-link to="/" class="btn btn-warning">Cancel</router-link>
				<button class="btn btn-success">Update</button>
			</div>
		</form>
	</div>
</div>
</template>
<script>
	export default {
		data: function() {
			return {
				posts: {
					title: '',
					description: '',
				},
				errors: []
			}
		},
		created() {
			let id = this.$route.params.id;
			axios.get('/posts/' + id + '/edit')
			.then(response => {
				console.log(response)
				this.posts = response.data
			})
			.catch(e => {
				this.errors.push(e)
			})
		},
		methods: {
			submitPostEdit() {
				let id = this.$route.params.id;
				axios.put('/posts/' + id, this.posts)
				.then(response => {
					console.log(response)
					this.$router.push({path: '/'})
					this.posts = response.data
				})
				.catch(e => {
					this.errors.push(e)
				})
			}
		}
	}
</script>