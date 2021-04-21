<script>
	//import Estimates from './Estimates.svelte';
	import {fade, slide, scale} from 'svelte/transition';
	import {flip} from 'svelte/animate';

	var currentView;
	var resincount;
	var resinmins;
	
	var time, hour, min;
	var fulltime;

	$: if (isNaN(resincount) || (resincount >= 0 && resincount <= 160)) {
		resincount = parseInt(resincount);
		resinmins = (160 - resincount) * 8;
		time = new Date();
		hour = time.getHours();
		min = time.getMinutes();
		fulltime = new Date(time.getTime() + resinmins * 60000);
		fulltime = fulltime.toLocaleTimeString();
	} 
	else if (resincount > 160) {
		resincount = Math.floor(resincount / 10); 
	}
	else {
		resincount = 0;
	}

	
</script>

<style>
	:global(body){
		background-color: #333333;
		color: #e6e6e6;
		font-family: 'Ubuntu', Helvetica, sans-serif;
	}
	.main{
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.main-elements{
		height:20%;
		width:25%;
		display: flex;
		flex-direction: column;
		justify-content: space-evenly;
		align-items: center;
		z-index: 50;
	}
	.icon{
		width: 100px;
		height: 100px;
	}
	.bg-effect{
		position:fixed;
		z-index: 20;
		width:100%;
		height:100%;
	}
	.question{
		font-size: 25vh;
		color: rgba(0,0,0,0.1);
	}
	.resinbox{
		border-width: 0px 0px 2px 0px;
		width:100%;
		background-color: rgba(255,255,255,0);
		border-color:#7d7d7d;
		color: #e6e6e6;
		font-size: 30px;
		text-align: center;
	}
	.resinbox:focus{
		outline:none;
	}
	.bigtime{
		font-size: 40px;
		padding:5px;
	}
	.estimates{
		height:150px;
		width:400px;
		top:5px;
		text-align:center;
		display:flex;
		flex-direction: column;
		justify-content: space-evenly;
		align-items: center;
	}

	/* Change Placeholder Style */
	::-webkit-input-placeholder {
		text-align: center;
		font-size:1.5vw;
	}

	:-moz-placeholder { /* Firefox 18- */
		text-align: center; 
		font-size:1.5vw; 
	}

	::-moz-placeholder {  /* Firefox 19+ */
		text-align: center;  
		font-size:1.5vw;
	}

	:-ms-input-placeholder {  
		text-align: center; 
		font-size:1.5vw;
	}

	/* Remove Input Arrows */	
	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button { /* Chrome, Safari, Edge, Opera */
		-webkit-appearance: none;
		margin: 0;
	}

	input[type=number] { /* Firefox */
		-moz-appearance: textfield;
	}


	/* Footer */
	.footer{
		width: 100vw;
		left:0;
		bottom:0;
		height: 5%;
		background-color:#292929;
		overflow:hidden;
		position: fixed;
		z-index: 100;
	}
	.footer-elements{
		width:100%;
		height:100%;
		text-align:center;
		margin: 0 auto;
	}
	.footer-elements > div {
		position:relative;
		display:inline-block;
		top:35%;
		font-size:11px;
		margin-left: 15px;
		width:30%;
	}
	.logo{
		
	}

</style>

<svelte:head>
	<title>Genshin Impact Resin Calculator</title>
</svelte:head>
{#if resincount >= 0 && resincount < 160}
	<div class="bg-effect">
		<marquee scrollamount="50" behavior="alternate">
			<span class="question">How much resin do you have?</span><br>
			<span class="question">How much resin do you have?</span><br>
			<span class="question">How much resin do you have?</span><br>
			<span class="question">How much resin do you have?</span><br>
			<span class="question">How much resin do you have?</span><br>
		</marquee>
	</div>
{/if}
<div class="main">
	<div class="main-elements">
		<img class="icon" src="img/fragileresin" alt="Fragile Resin" />
		<input class="resinbox" type="number" placeholder="How much resin do you have?" bind:value={resincount} autofocus/>

		{#if resincount >= 0 && resincount < 160}
			<div class="estimates" transition:fade>
				<span>Awesome!</span>
				<span>Your resin will be full again at around...</span>
				<span class="bigtime">{fulltime}</span>
			</div>
		{:else if resincount == 160}
			<div transition:fade>
				You have enough resin, my friend!
			</div>
		{/if}
	</div>
</div>
<div class="footer">
	<div class="footer-elements">
		<div class="mew">We are not affiliated with or endorsed by miHoYo.</div>
		<div class="logo">Logo goes here!</div>
		<div class="copyright">Copyright 2021 gntstrsk</div>
	</div>
</div>