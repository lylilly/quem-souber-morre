//IMPORTANDO MÓDULO
//import { itens } from "./itens.js"

//ARRAY ITENS DO CARRINHO
//let itens = []

//classe Item
class Item {
    constructor(idItem, nome, descricao, valorUnitario, quantidade, caminho_imagem) {
        this.idItem = idItem
        this.nome = nome
        this.descricao = descricao
        this.valorUnitario = valorUnitario
        this.quantidade = 1
        this.caminho_imagem = caminho_imagem
    }
}

const addItem = (objItem) => {
    const item = new Item(objItem.id, objItem.nome, objItem.descricao, objItem.preco, objItem.quantidade, objItem.caminhoimg)

    //itens.push(item)
    addItemSession(item)
}

const addItemSession = (objItem) => {

    const arrayItem = JSON.parse(sessionStorage.getItem("itensSession")) ?? []

    let pos = -1

    for (let i in arrayItem) {
        if (arrayItem[i].idItem == objItem.idItem) {
            pos = i
            break
        }
    }

    if (pos == -1) {
        arrayItem.push(objItem)
    } else {
        arrayItem[pos].quantidade += 1
    }

    sessionStorage.setItem("itensSession", JSON.stringify(arrayItem))
}

const listarItens = () => {
    return JSON.parse(sessionStorage.getItem("itensSession"))
}

const removeItem = (posicao) => {
    const itens = JSON.parse(sessionStorage.getItem('itensSession'))
    itens.splice(posicao, 1)

    sessionStorage.setItem('itensSession', JSON.stringify(itens))

}

//ALTERANDO A QUANTIDADE DE UM ITEM
const alteraQuantidadeItem = (quant, pos) => {
    const itens = JSON.parse(sessionStorage.getItem('itensSession'))
    itens[pos].quantidade = parseInt(quant) > 0 ? parseInt(quant) : 1

    sessionStorage.setItem('itensSession', JSON.stringify(itens))
}

export { addItem, listarItens, removeItem, alteraQuantidadeItem }

