
<script>

	import Header from './Header.svelte';
	import Footer from './Footer.svelte';

	let formPreenchido = false; // Variável para controlar se o formulário está preenchido

    let jsonData; // Variável global para armazenar os dados do formulário

	let temas = "";
	let tags = "";

	let ciencia_pesquisa = "";
	let complexo_industrial = "";
	let comunicacao = "";
	let educacao = "";
	let empreendedorismo = "";
	let financiamento = "";
	let gestao = "";
	let governanca = "";
	let inovacao = "";
	let modelos_assistenciais = "";
	let regulacao = "";
	let socio_ambiental = "";

	let ciencia_pesquisa_percent = "";
	let complexo_industrial_percent = "";
	let comunicacao_percent = "";
	let educacao_percent = "";
	let empreendedorismo_percent = "";
	let financiamento_percent = "";
	let gestao_percent = "";
	let governanca_percent = "";
	let inovacao_percent = "";
	let modelos_assistenciais_percent = "";
	let regulacao_percent = "";
	let socio_ambiental_percent = "";
	
	let alegria = "";
	let raiva = "";
	let nojo = "";
	let medo = "";
	let tristeza = "";
	let surpresa = "";

	let main_state = false;

	function isFormPreenchido() {
        // Verificar se todos os campos do formulário estão preenchidos
        const titulo = document.querySelector('textarea[name="titulo"]');
        const resumo = document.querySelector('textarea[name="resumo"]');
		
        return titulo.value && resumo.value;
    }

	function salvarFormulario() {        
        const titulo = document.querySelector('textarea[name="titulo"]').value;
        const resumo = document.querySelector('textarea[name="resumo"]').value;

        const formulario = {
            titulo,
            resumo
        };

        jsonData = JSON.stringify(formulario, null, 2);
    }
	
	function back_work (){        
        console.log(jsonData)
        fetch('https://zapnews-as-a-service-x4fs6sryfq-rj.a.run.app/upload-info', {
            mode: 'cors',
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: jsonData,})
        .then((response) => response.json())
        .then((data) => {
            console.log('OK!')
            console.log(data)

			temas = data["themes"]
			tags = data["tags"]

			ciencia_pesquisa = data["ciencia_pesquisa"]
			complexo_industrial = data["complexo_industrial"]
			comunicacao = data["comunicacao"]
			educacao = data["educacao"]
			empreendedorismo = data["empreendedorismo"]
			financiamento = data["financiamento"]
			gestao = data["gestao"]
			governanca = data["governanca"]
			inovacao = data["inovacao"]
			modelos_assistenciais = data["modelos_assistenciais"]
			regulacao = data["regulacao"]
			socio_ambiental = data["socio_ambiental"]

			ciencia_pesquisa_percent = data["ciencia_pesquisa_percent"] + '%'
			complexo_industrial_percent = data["complexo_industrial_percent"] + '%'
			comunicacao_percent = data["comunicacao_percent"] + '%'
			educacao_percent = data["educacao_percent"] + '%'
			empreendedorismo_percent = data["empreendedorismo_percent"] + '%'
			financiamento_percent = data["financiamento_percent"] + '%'
			gestao_percent = data["gestao_percent"] + '%'
			governanca_percent = data["governanca_percent"] + '%'
			inovacao_percent = data["inovacao_percent"] + '%'
			modelos_assistenciais_percent = data["modelos_assistenciais_percent"] + '%'
			regulacao_percent = data["regulacao_percent"] + '%'
			socio_ambiental_percent = data["socio_ambiental_percent"] + '%'
			
			alegria = data["alegria"] + '%'
			raiva = data["raiva"] + '%'
			nojo = data["nojo"] + '%'
			medo = data["medo"] + '%'
			tristeza = data["tristeza"] + '%'
			surpresa = data["surpresa"] + '%'

			main_state = true
        })
        .catch((error) => {
            console.log('ERRO!')
            console.log(error)
        });
    }

	function button_action() {		
		main_state = false
		formPreenchido = isFormPreenchido()
		console.log('formPreenchido')
		console.log(formPreenchido)
        salvarFormulario()
        back_work();		
    }

</script>


<Header/>

<main style="padding-top: 80px;">

	<!--<div class="container">-->

		<div class="scrollable-content">

			<div class="container">
				<div class="scrollable-content">
					<div>
						<label for='titulo'> <p1> Título: </p1> </label>
						<textarea name='titulo' cols="30" rows="4" maxlength="400" style="resize: none;" />	
						<br>
					</div>
					<br>	
					<div>
						<label for='resumo'> <p1> Resumo: </p1> </label>
						<textarea name='resumo' cols="30" rows="7" maxlength="700" style="resize: none;" />	
						<br>
					</div>

					<br>	
					<br>

					<button class='button_style' on:click={button_action}> <img height=60 src="./img/next.png" style="padding-top: 20%"> </button>
					
				</div>
			</div>

			{#if formPreenchido!=""}
			{#if main_state==true}	
			<br>
			<br>	
			
			<div style="border:2px solid grey; border-radius: 15px; padding-right: 10px; padding-left: 10px;">
				<h1><t1>Temas:</t1> {temas}</h1>
				<h1><t1>Tags - FIS:</t1> {tags}</h1>
			</div>

			<br>
			<div style="padding: 1%"></div>	
			<br>

			<div style="border:2px solid grey; border-radius: 15px; padding: 10px">
				<div class="table-container">
					<table style="font-size: 13px;">
						<tr>				
							<th><img height=45 src="img/alegria.svg"></th>
							<th><img height=45 src="img/tristeza.svg"></th>
							<th><img height=45 src="img/medo.svg"></th>
							<th><img height=45 src="img/nojo.svg"></th>
							<th><img height=45 src="img/raiva.svg"></th>
							<th><img height=45 src="img/surpresa.svg"></th>				
						</tr>
						<tr style="height: 40px;">				
							<td>{alegria}</td>
							<td>{tristeza}</td>
							<td>{medo}</td>
							<td>{nojo}</td>
							<td>{raiva}</td>
							<td>{surpresa}</td>
						</tr>
					</table>
				</div>		

				<div class="table-container">
					<table style="font-size: 13px;">
						<tr>
							<!--<th></th>-->
							<th>Ciência/Pesquisa</th>
							<th>Complexo Industrial</th>
							<th>Comunicação</th>
							<th>Educação</th>
							<th>Empreendedorismo</th>
							<th>Financiamento</th>
							<th>Gestão</th>
							<th>Governança</th>
							<th>Inovação</th>
							<th>Modelos Assistenciais</th>
							<th>Regulação</th>
							<th>Socio-Ambiental</th>
						</tr>
						<!--<tr>
							<th>Total:</th>
							<td>{ciencia_pesquisa}</td>
							<td>{complexo_industrial}</td>
							<td>{comunicacao}</td>
							<td>{educacao}</td>
							<td>{empreendedorismo}</td>
							<td>{financiamento}</td>
							<td>{gestao}</td>
							<td>{governanca}</td>
							<td>{inovacao}</td>
							<td>{modelos_assistenciais}</td>
							<td>{regulacao}</td>
							<td>{socio_ambiental}</td>
						</tr>-->
						<tr style="height: 40px;">
							<!--<th>Proporcional:</th>-->
							<td>{ciencia_pesquisa_percent}</td>
							<td>{complexo_industrial_percent}</td>
							<td>{comunicacao_percent}</td>
							<td>{educacao_percent}</td>
							<td>{empreendedorismo_percent}</td>
							<td>{financiamento_percent}</td>
							<td>{gestao_percent}</td>
							<td>{governanca_percent}</td>
							<td>{inovacao_percent}</td>
							<td>{modelos_assistenciais_percent}</td>
							<td>{regulacao_percent}</td>
							<td>{socio_ambiental_percent}</td>
						</tr>
					</table>
				</div>
			</div>
			{/if}	
			{/if}

		</div>

		<div style="padding-bottom: 13%;"></div>
	
	<!--</div>-->

</main>

<Footer/>



<style>
	@import 'src/style.css';

	main {
		text-align: center;
		padding: 0;
		/*max-width: 240px;*/
		/*margin-top: 5%;*/
		/*margin-bottom: 5%;*/
		margin: 0 auto;
	}

	main.container {
        display: grid;
        place-items: center;
        min-height: 100vh;
    }


	h1 {
		font-size: 17px;
		font-weight: 400;
	}

	t1 {		
		color: #082e74;
		font-weight: 600;
	}

	p1 {		
		/*font-size: 2em;*/
		font-size: 15.5px;
		font-weight: 600;
	}

	.button_style {
		padding: 0;
		border: none;
		background: none;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
			padding: 0;
		}
	}

	table {
		max-width: 100%;
		text-align: center;
		margin: 0 auto; /* or margin: 0 auto 0 auto */
	}

	.table-container {
        max-width: 100%;
        overflow-x: auto;
    }

	td, th {
		/*border: 1px solid #dddddd85;*/
		text-align: center;
		padding: 8px;
	}

	.scrollable-content {
        max-width: 100%;
        max-height: 100%;
        overflow: auto;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>