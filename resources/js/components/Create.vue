<template>
<div class="card">
	<div class="card-header">
		Create New Post
	</div>
	<div class="card-body">
		<form v-on:submit="submitPost()">
			<div class="form-group">
				<input type="text" v-model="posts.title" placeholder="Title" class="form-control">
			</div>
			<div class="form-group">
				<textarea rows="5" v-model="posts.description" placeholder="Description" class="form-control"></textarea>
			</div>
			<div class="form-group">
				<router-link to="/" class="btn btn-warning">Cancel</router-link>
				<button class="btn btn-success">Create</button>
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
		methods: {
			submitPost() {
				axios.post('/posts', this.posts)
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