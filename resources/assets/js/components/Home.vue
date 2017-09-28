<template>
	<div>
		
	<nav class="panel column is-offset-2 is-8" >
	  <p class="panel-heading">
	    Vuejs Phonebook 
	    <button class="button is-primary is-outlined" @click="openAdd">
	      Add New
	    </button>
	  </p>
	  <div class="panel-block">
	    <p class="control has-icons-left">
	      <input class="input is-small" type="text" placeholder="search">
	      <span class="icon is-small is-left">
	        <i class="fa fa-search"></i>
	      </span>
	    </p>
	  </div>
	 
	 
	  <a class="panel-block ">
	  	<span class="column is-9">
	    	marksheet
	  	</span>
	    <span class="panel-icon column is-1">
	      <i class="has-text-danger fa fa-trash" aria-hidden="true"></i>
	    </span>
	    <span class="panel-icon column is-1">
	      <i class="has-text-info fa fa-edit" aria-hidden="true"></i>
	    </span><span class="panel-icon column is-1">
	      <i class="has-text-primary fa fa-eye" aria-hidden="true"></i>
	    </span>
	  </a>
	</nav>

	<Add :openmodal='addActive' @closeRequest='close'></Add>
	</div>
</template>

<script>
let Add = require('./Add.vue');
	export default{
		components:{Add},
		data(){
			return{
				addActive : ''
			}
		},
		methods:{
			openAdd(){
				this.addActive = 'is-active';
			},
			close(){
				this.addActive = ''
			}
		}
	}
</script>