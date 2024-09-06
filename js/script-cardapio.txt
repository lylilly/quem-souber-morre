//IMPORTANDO MÓDULO
import { addItem } from "./script-carrinho.js"

//PEGANDO ELEMENTOS DO DOM
const divItens = document.querySelector('#itens')

//API
const endPoint = `https://825ab740-8771-4e7c-98a2-f564b1280781-00-23tuuqc3162va.kirk.replit.dev/`

//FUNÇÃO CARREGA API
const apiProdutos = () => {
    fetch(endPoint)
        .then(resp => {
            resp.json()
                .then(dados => {
                    carregaProdutos(dados)
                })
        }).catch(console.log('PRODUTOS LOCALIZADOS'))
}

apiProdutos()

//FUNÇÃO CARREGA CARDS
const carregaProdutos = (dados) => {
    divItens.innerHTML = ''

    dados.map((elem, i) => {
        const divCard = document.createElement('div')
        divCard.setAttribute('class', 'card')

        const divImagem = document.createElement('div')
        divImagem.setAttribute('class', 'imgCard')

        const imagem = document.createElement('img')
        imagem.setAttribute('src', elem.caminhoimg)
        imagem.setAttribute('title', elem.nome)

        divImagem.appendChild(imagem)

        const divDescricao = document.createElement('div')
        divDescricao.setAttribute('class', 'descricao')
        divDescricao.innerHTML = elem.nome

        const divDetalhe = document.createElement('div')
        divDetalhe.setAttribute('class', 'detalhe')
        divDetalhe.innerHTML = elem.descricao

        const divValor = document.createElement('div')
        divValor.setAttribute('class', 'valor')
        divValor.innerHTML = `R$ ${parseFloat(elem.preco).toFixed(2).replace('.', ',')}`

        const divBtnAdd = document.createElement('div')
        divBtnAdd.setAttribute('class', 'btnAdd')

        const buttonAdd = document.createElement('button')
        buttonAdd.setAttribute('class', 'add')
        buttonAdd.innerHTML = `ADICIONAR`
        buttonAdd.addEventListener('click', () => {
            addItem(elem)
            window.location = 'carrinho.html'
        })

        divBtnAdd.appendChild(buttonAdd)

        divCard.appendChild(divImagem)
        divCard.appendChild(divDescricao)
        divCard.appendChild(divDetalhe)
        divCard.appendChild(divValor)
        divCard.appendChild(divBtnAdd)

        divItens.appendChild(divCard)

    })

}
