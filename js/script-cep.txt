//PEGANDO ELEMENTOS DO DOM
const inputCep = document.querySelector('#cepNum')
const divEndereco = document.querySelector('#divEndereco')


//FUNÇÃO NO INPUT
inputCep.addEventListener('blur', (evt) => {
    let numCep = evt.target.value.replace('-', '')
    consultaApi(numCep)
})

//FUNÇÃO CONSULTA VIACEP
const consultaApi = (numCep) => {
    const endPoint = `https://viacep.com.br/ws/${numCep}/json/`

    fetch(endPoint)
        .then(resp => {
            resp.json()
                .then(dados => {
                    carregaDadosForm(dados)
                })

        }).catch(console.log('CEP NÃO LOCALIZADO!!'))
}

//FUNÇÃO CARREGA DADOS NO FORMULÁRIO
const carregaDadosForm = (dados) => {
    divEndereco.classList.remove('ocultar')

    for (let atributo in dados){
        if(document.querySelector(`#${atributo}`)){
            document.querySelector(`#${atributo}`).value = dados[atributo]
            document.querySelector(`#${atributo}`).setAttribute('disabled', 'disabled')
        }
    }

    document.querySelector(`#numero`).focus()
}

