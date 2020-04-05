<template>
	<div class="card">
		<div class="card-header">
			<router-link to="/"><i class="fa fa-arrow-left"></i></router-link>
		</div>
		<div class="card-body">
			<form>
				<div class="form-group">
					<label>Title</label>
					<input v-bind:value="posts.title" type="text" class="form-control">
				</div>
				<div class="form-group">
					<label>Description</label>
					<textarea rows="5" class="form-control">{{posts.description}}</textarea>
				</div>
				<!-- <div class="form-group">
					<button class="btn btn-success">Edit</button>
				</div> -->
			</form>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				posts: [],
				errors: []
			}
		},
		created() {
			let id = this.$route.params.id;
			axios.get('/posts/' + id)
			.then(response => {
				console.log(response)
				this.posts = response.data
			})
			.catch(e => {
				this.errors.push(e)
			})
		}
	}
</script>