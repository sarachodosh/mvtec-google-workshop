<script>
	
	import Menu from './components/common/Menu.svelte'
	// import Test from './test/Test.svelte'
	import Page from './components/views/Page.svelte'
	import Footer from './components/common/Footer.svelte'

</script>

<main>

	<Menu />
	<Page />
	
	<Footer>
		<div slot="about">
			The blues of a pandemic is a project to visualize Google Trends data on the relationship between struggles and solidarity during the COVID-19 pandemic.
		</div>
		<div slot="data">
			Data is based on Google Trends monthly indexes for 60 selected topics between 2016 and 2021. 
		</div>
		<div slot="team">
			Xavier Bolló, Sara Chodosh, Santiago Salcido
		</div>
	</Footer>
</main>

<style>
	main {
		/* padding: 1em; */
		padding-bottom: 0;
		margin: 0 auto;
	}
</style>