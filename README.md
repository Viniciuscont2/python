# python


import pandas as pd
def forca_opcao(msg,conjuto_opcoes,msg_erro = 'Ivalido'):
    opceos = '\n'.join(carros[conjuto_opcoes])
    escolha = input(f"{msg}\n{opceos}\n ->")
    while not escolha in conjuto_opcoes:
        print(msg_erro)
        escolha = input(f"{msg}\n {opceos}\n -> ")
    return escolha


def acha_index(lista,elemento):
    for i in range(len(lista)):
        if lista[i] == elemento:
            return i

def forca_numero(msg, msg_erro = 'Invalido'):
    num = input(msg)
    while not num.isalnumeric():
        print(msg_erro)
        num = input(msg)
    return int(num)
        
carros = {
    'modelo' : ['opala','marea','kombi','celtinha','uno','monza','corcel'],
    'potência (cv)' : [172,130,250,140,100,120,150],
    'consumo (km/l)' : [1,3,8,7,15,2,1.5],
    'cor' : ['laranja','verde','branca','preto','prata','preto','azul'],
    'ano' : ['1972','2004','1985','2014','2001','1980','1975'],
    'estoque' : [5,6,7,8,9,10,11],
    'preço' : [50,10,2.50,1000000,100,200,999999]
}

indices = {}
for i in range(len(carros['modelo'])):
    indices[carros['modelo'][i]] = i



s_ou_n = ['sim','nao']
valor_total = 0

carrinho = {
    'Carros' : {},
    'Valor Total' : 0 ,  
    'Endereço' : {
        'Rua' : '',
        'Cep' : '',
        'Número' : ''
    }
}



print(pd.DataFrame(carros))

while True:
    escolha = forca_opcao('Qual carro voce quer ver:',carros['modelo'])
    index_escolha = indices[escolha]
    for key in carros.keys():
        print(key,carros[key][index_escolha])
    comprar = forca_opcao('voce vai comprar?',s_ou_n)
    if comprar == s_ou_n[0]:
        qtd = forca_numero(f"Quantos {escolha} ?")
        if carros['estoque'][index_escolha] >= qtd:
            carros['estoque'][index_escolha] -= qtd    
            carrinho['Valor Total'] += qtd*carros['preço'][index_escolha]
            if escolha not in carrinho['Carros'].keys():
                carrinho['Carros'][escolha] = qtd
            else:
                carrinho['Carros'][escolha] += qtd
        else:
            print(f"não há {qtd} de {escolha} no estoque. voltaremos ao inicio.")
            continue
            
    encerrar = forca_opcao("Quer encerrar a compra?",s_ou_n)
    if encerrar == s_ou_n[0]:
        for key in carrinho['Endereço'].keys():
            carrinho['Endereço'][key] = input(f"Diga o/a {key}: ")
        print(carrinho)
        break
        
    else:
        ver_mais = forca_opcao("Quer ver outras opções ?", s_ou_n)
        if ver_mais == s_ou_n[1]:
            break
