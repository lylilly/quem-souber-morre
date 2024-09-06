//CRIANDO A CLASSE ITEM
class Item {
    constructor(idItem, nomeItem, descricaoItem, valorUnitario, quantidade, imagemItem) {
        this.idItem = idItem
        this.nomeItem = nomeItem
        this.descricaoItem = descricaoItem
        this.valorUnitario = valorUnitario

        if(quantidade > 1){
            this.quantidade += quantidade
        }else{
            this.quantidade = 1
        }

        this.imagemItem = imagemItem
    }
}

//FUNÇÃO DE ADICIONAR ITEM NO CARRINHO
const addItem = (elemItem) => {
    const objItem = new Item(elemItem.id, elemItem.nome, elemItem.descricao,elemItem.preco, 1, elemItem.caminhoimg)

    addItemSession(objItem)
}

//ADICIONAR O ARRAY DE ITENS NA SESSÃO(SESSION)
const addItemSession = (objItem) => {
    const itens = JSON.parse(sessionStorage.getItem('itensSession')) ?? []
    
    let pos = -1
    
    for(let i in itens){
        if(itens[i].idItem == objItem.idItem){
            pos = i
            break
        }
    }
    
    if(pos == -1){
        itens.push(objItem)
    }else{
        itens[pos].quantidade += 1
    }

    sessionStorage.setItem('itensSession', JSON.stringify(itens))
}

//RETORNAR O ARRAY ITENS DA SESSÃO (SESSION)
const listarItens = () =>{
    return JSON.parse(sessionStorage.getItem('itensSession'))
}

//REMOVENDO ITEM
const removerItem = (posicao) =>{
    const itens = JSON.parse(sessionStorage.getItem('itensSession'))
    itens.splice(posicao,1)

    sessionStorage.setItem('itensSession', JSON.stringify(itens))

    listarItens()
}

//ALTERANDO A QUANTIDADE DE UM ITEM
const alteraQuantidadeItem = (quant, pos) =>{
    const itens = JSON.parse(sessionStorage.getItem('itensSession'))
    itens[pos].quantidade += quant

    sessionStorage.setItem('itensSession', JSON.stringify(itens))
}

export{addItem, listarItens, removerItem, alteraQuantidadeItem}

