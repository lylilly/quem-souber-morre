//IMPORTANDO MÓDULOS 
import { listarItens, removeItem, alteraQuantidadeItem } from './script-carrinho.js'

//PEGANDO ELEMENTOS DO DOM
const divCardsCarrinho = document.querySelector('#cards-carrinho')
const pTotal = document.querySelector("#valorTotal")
const pTotalPagar = document.querySelector("#valorTotalPagar")

divCardsCarrinho.innerHTML = ''

let total = 0.0

listarItens().map((elem, i) => {
    const divCardCarrinho = document.createElement('div')
    divCardCarrinho.setAttribute('class', 'card-carrinho')

    const divImgCard = document.createElement('div')
    divImgCard.setAttribute('class', 'imgCard')

    const imagem = document.createElement('img')
    imagem.setAttribute('src', elem.caminho_imagem)
    imagem.setAttribute('title', elem.nome)

    divImgCard.appendChild(imagem)

    const divDados = document.createElement('div')
    divDados.setAttribute('class', 'dados')

    const divDescricao = document.createElement('div')
    divDescricao.setAttribute('class', 'descricao')
    divDescricao.innerHTML = elem.nome

    const divDetalhe = document.createElement('div')
    divDetalhe.setAttribute('class', 'detalhe')
    divDetalhe.innerHTML = elem.descricao

    const divNumeros = document.createElement('div')
    divNumeros.setAttribute('class', 'numeros')

    const divValor = document.createElement('div')
    divValor.setAttribute('class', 'valor')
    divValor.innerHTML = `R$ ${parseFloat(elem.valorUnitario).toFixed(2).replace('.', ',')}`

    const divInput = document.createElement('div')
    divInput.setAttribute('class', 'div-input')

    const input = document.createElement('input')
    input.setAttribute('type', 'number')
    input.setAttribute('name', 'quantidade')
    input.setAttribute('class', 'quantidade')
    input.setAttribute('min', '1')
    input.setAttribute('value', elem.quantidade)
    input.addEventListener('blur',(evt)=>{
        alteraQuantidadeItem(evt.target.value, i)
        window.location = 'carrinho.html'
    })

    divInput.appendChild(input)

    let valorItem = parseFloat(elem.valorUnitario) * parseFloat(elem.quantidade)

    total += valorItem

    const divValorItem = document.createElement('div')
    divValorItem.setAttribute('class', 'valor')
    divValorItem.innerHTML = `R$ ${parseFloat(valorItem).toFixed(2).replace('.', ',')}`

    divNumeros.appendChild(divValor)
    divNumeros.appendChild(divInput)
    divNumeros.appendChild(divValorItem)

    const divBtnAdd = document.createElement('div')
    divBtnAdd.setAttribute('class', 'btnAdd')

    const imagemBotao = document.createElement('img')
    imagemBotao.setAttribute('src', 'imagens/remover.png')
    imagemBotao.setAttribute('title', `Remover ${elem.nome} do Carrinho?`)
    imagemBotao.addEventListener('click', () => {
        if (confirm(`Deseja remover ${elem.descricao} do carrinho?`)) {
            removeItem(i)
            window.location = 'carrinho.html'
        }
    })

    imagemBotao.innerHTML = 'ADICIONAR'

    divBtnAdd.appendChild(imagemBotao)

    divDados.appendChild(divDescricao)
    divDados.appendChild(divDetalhe)
    divDados.appendChild(divNumeros)

    divCardCarrinho.appendChild(divImgCard)
    divCardCarrinho.appendChild(divDados)
    divCardCarrinho.appendChild(divBtnAdd)

    divCardsCarrinho.appendChild(divCardCarrinho)

})

pTotal.innerHTML = `R$ ${parseFloat(total).toFixed(2).replace('.',',')}`
pTotalPagar.innerHTML = `R$ ${parseFloat(total + 5.0).toFixed(2).replace('.',',')}`