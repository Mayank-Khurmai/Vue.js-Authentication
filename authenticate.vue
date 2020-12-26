const authenticate = {
	template: `
	<img src="https://swoopnow.com/wp-content/uploads/2017/12/user-authentication.png" class="w-100">
	<h4 class="my-4">{{ response }}</h4>
	<button class="btn btn-primary rounded-0" v-on:click="auth">Try authentication</button>
	`,
	data(){
		return{
			response: "",
			username: this.$route.params.user,
			password: this.$route.params.password,
		}
	},

	methods: {
		auth(){
			this.response = "Authenticating please wait...";
			const formdata = new FormData();
			formdata.append("username",this.username);
			formdata.append("password",this.password);


			const ajax = axios({
				method: "POST",
				url: "data.php",
				data: formdata,
			});

			ajax.then(function(r){
				var message = r.data;
				if(message.trim() == "success")
				{
					this.response = "Hi "+this.username;
				}

				else{
					this.response = "Unauthorized user !";
				}
			}.bind(this));
		}
	}
}

