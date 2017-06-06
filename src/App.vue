<template>
<div id="app" class="container">
	<div class="page-header">
		<h1>Vue js 2 and Firebase application</h1>
	</div>
	<div class="panel panel-default">
		<div class="panel-heading">
			<h3>Add Book</h3>
		</div>
		<div class="panel-body">
			<form id="form" class="form-inline" v-on:submit.prevent="addBook">
				<div class="form-group">
					<label for="bookeTitle">Title:</label>
					<input type="text" id="bookTitle" class="form-control" v-model="newBook.title">
				</div>
				<div class="form-group">
					<label for="bookeAuthor">Author:</label>
					<input type="text" id="bookAuthor" class="form-control" v-model="newBook.author">
				</div>
				<div class="form-group">
					<label for="bookeUrl">URL:</label>
					<input type="text" id="bookUrl" class="form-control" v-model="newBook.url">
				</div>
				<input type="submit" class="btn btn-primary" value="Add book">
			</form>
		</div>
	</div>
	<div class="panel panel-default">
		<div class="panel-heading">
			<h3>Books list</h3>
		</div>
		<div class="panel panel-body">
			<table class="table table-striped">
				<thead>
					<tr>
						<th>Title</th>
						<th>Author</th>
						<th>Delete</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="book in books">
						<td>
							<a v-bind:href="book.url">{{ book.title }}</a>
						</td>
						<td>{{ book.author }}</td>
						<td><span class="glyphicon glyphicon-trash" v-on:click="removeBook(book)      "></span></td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</div>
</template>

<script>
import Firebase from 'firebase';
let config = {
	apiKey: "AIzaSyBOQq7zg9mLyiDEEg4qIzljDZGNyJ3tBYs",
	authDomain: "vuejs-firebase-d78d8.firebaseapp.com",
	databaseURL: "https://vuejs-firebase-d78d8.firebaseio.com",
	projectId: "vuejs-firebase-d78d8",
	storageBucket: "vuejs-firebase-d78d8.appspot.com",
	messagingSenderId: "843797352624"
};
let app = Firebase.initializeApp(config);
let db = app.database();

let bookRef = db.ref('books');

export default {
	name: 'app',
	firebase: {
		books: bookRef
	},
	data() {
		return {
			newBook: {
				title: ' ',
				author: ' ',
				url: ' '
			}
		}
	},
	methods: {
		addBook: function() {
			bookRef.push(this.newBook);
			this.newBook.title = ' ';
			this.newBook.author = ' ';
			this.newBook.url = ' ';
		},
		removeBook: function(book) {
			bookRef.child(book['.key']).remove();
            alert('Book removed');
		}
	}
}
</script>

<style>

</style>
