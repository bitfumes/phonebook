<template>
	<div>
		
	<nav class="panel column is-offset-2 is-8" >
	  <p class="panel-heading">
	    Vuejs Phonebook 
	    <button class="button is-primary is-outlined" @click="openAdd">
	      Add New
	    </button>
	    <span class="is-pulled-right" v-if="loading">
	    	<i class="fa fa-refresh fa-spin fa-2x fa-fw"></i>
	    </span>
	  </p>
	  <div class="panel-block">
	    <p class="control has-icons-left">
	      <input class="input is-small" type="text" placeholder="search">
	      <span class="icon is-small is-left">
	        <i class="fa fa-search"></i>
	      </span>
	    </p>
	  </div>
	 
	 
	  <a class="panel-block " v-for="item,key in lists">
	  	<span class="column is-9">
	    	{{ item.name }}
	  	</span>
	    <span class="panel-icon column is-1">
	      <i class="has-text-danger fa fa-trash" aria-hidden="true" @click="del(key,item.id)"></i>
	    </span>
	    <span class="panel-icon column is-1">
	      <i class="has-text-info fa fa-edit" aria-hidden="true" @click="openUpdate(key)"></i>
	    </span><span class="panel-icon column is-1">
	      <i class="has-text-primary fa fa-eye" aria-hidden="true" @click="openShow(key)"></i>
	    </span>
	  </a>
	</nav>

	<Add :openmodal='addActive' @closeRequest='close'></Add>
	<Show :openmodal='showActive' @closeRequest='close'></Show>
	<Update :openmodal='updateActive' @closeRequest='close'></Update>
	</div>
</template>

<script>
let Add = require('./Add.vue');
let Show = require('./Show.vue');
let Update = require('./Update.vue');
	export default{
		components:{Add,Show,Update},
		data(){
			return{
				addActive : '',
				showActive : '',
				updateActive : '',
				lists:{},
				errors:{},
				loading:false
			}
		},
		mounted(){
			axios.post('/getData')
			.then((response)=> this.lists = response.data)
			.catch((error) => this.errors = error.response.data.errors)
		},
		methods:{
			openAdd(){
				this.addActive = 'is-active';
			},
			openShow(key){
				this.$children[1].list = this.lists[key]
				this.showActive = 'is-active';
			},
			openUpdate(key){
				this.$children[2].list = this.lists[key]
				this.updateActive = 'is-active';
			},
			close(){
				this.addActive = this.showActive = this.updateActive = ''
			},
			del(key,id){
				if (confirm("Are you sure ?")) {
					this.loading = !this.loading
					axios.delete(`/phonebook/${id}`)
					.then((response)=> {this.lists.splice(key,1);this.loading = !this.loading})
					.catch((error) => this.errors = error.response.data.errors)	
				}
			}
		}
	}
</script>