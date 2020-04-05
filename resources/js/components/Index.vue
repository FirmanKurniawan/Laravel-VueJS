<template>
<div class="card">
	<div class="card-header">
		<router-link to="/create" class="btn btn-info float-right">Create New Post</router-link>
	</div>
	<div class="card-body">
		<table class="table table-bordered">
			<thead>
				<tr>
					<th scope="col">#</th>
					<th scope="col">Title</th>
					<th scope="col">Description</th>
					<th scope="col" colspan="3">Action</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(post, index) of posts">
					<th scope="row">{{ index+1}}</th>
					<td>{{post.title}}</td>
					<td>{{post.description}}</td>
					<td><router-link :to="{name: 'readPost', params:{id: post.id}}" class="btn btn-info"><i class="fa fa-eye">View</i></router-link></td>
					<td><router-link :to="{name: 'editPost', params:{id: post.id}}" class="btn btn-success"><i class="fa fa-edit">Edit</i></router-link></td>
					<td><button class="btn btn-danger" v-on:click="submitPostDelete(post.id, index)"><i class="fa fa-trash"> Delete</i></button></td>
				</tr>
			</tbody>
		</table>
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
		axios.get('/posts')
		.then(response => {
			this.posts = response.data
		})
		.catch(e => {
			this.errors.push(e)
		})
		},
		methods: {
			submitPostDelete(id, index) {
				if(confirm("Click 'OK' To Delete Post! "))
				axios.delete('/posts/' + id)
				.then(response => {
					console.log(response)
					this.posts.splice(index, 1);
				})
				.catch(e => {
					this.errors.push(e)
				})
			}
		}
}
</script>