class Produto:
def __init__(self, id, nome, categoria_id, quantidade, preco): 
self.id = id
self.nome = nome 
self.categoria_id = categoria_id 
self.quantidade = quantidade
self.preco = preco
class Categoria:
def __init__(self, id, nome): 
self.id = id
self.nome = nome 
class Movimentacao:
def __init__(self, id, produto_id, quantidade, tipo_movimentacao, data): 
self.id = id
self.produto_id = produto_id 
self.quantidade = quantidade 
self.tipo_movimentacao = tipo_movimentacao 
self.data = data 
def cadastrar_produtos(produtos, contador_produtos): 
id = contador_produtos + 1 
nome = input('Nome do produto: ') 
categoria_id = int(input('ID da categoria: ')) 
quantidade = int(input('Insira a quantidade: ')) 
preco = float(input('Insira o preço: ')) 
produtos.append(Produto(id, nome, categoria_id, quantidade, preco))
print("Produto cadastrado com sucesso!")
return contador_produtos + 1 
def consultar_produto_id(produtos, id): 
for produto in produtos: 
if produto.id == id:
print(f'ID: {produto.id}, Nome: {produto.nome}, Categoria: {produto.categoria_id}, Quantidade: {produto.quantidade}, Preço: {produto.preco}')
return 
print("Produto não encontrado.")
def registrar_movimentacao(movimentacoes, contador_movimentos, produtos): 
id = contador_movimentos + 1 
produto_id = int(input("ID do produto: ")) 
quantidade = int(input("Quantidade: ")) 
tipo_movimentacao = input('Tipo de movimentação:\nE - Entrada\nS - Saída: ').strip().upper()
data = input("Data (DD/MM/AAAA): ") 
produto_encontrado = next((p for p in produtos if p.id == produto_id), None) 
if produto_encontrado: 
if tipo_movimentacao == 'E': 
produto_encontrado.quantidade += quantidade 
elif tipo_movimentacao == 'S':
if produto_encontrado.quantidade >= quantidade: 
produto_encontrado.quantidade -= quantidade
else:
print("Quantidade insuficiente no estoque!") 
return contador_movimentos
else:
print("Tipo de movimentação inválido!") 
return contador_movimentos
movimentacoes.append(Movimentacao(id, produto_id, quantidade, tipo_movimentacao, data)) 
print("Movimentação registrada com sucesso!") 
return contador_movimentos + 1
else:
print("Produto não encontrado!") 
return contador_movimentos
def gerar_relatorio_estoque(produtos):
print("Relatório de Estoque:")
for produto in produtos: 
print(f"ID: {produto.id}, Nome: {produto.nome}, Quantidade: {produto.quantidade}, Preço: {produto.preco:.2f}")
def consultar_movimentacoes(movimentacoes, produto_id):
print(f"Movimentações do produto ID {produto_id}:")
for movimentacao in movimentacoes: 
if movimentacao.produto_id == produto_id: 
print(f"ID: {movimentacao.id}, Quantidade: {movimentacao.quantidade}, Tipo: {movimentacao.tipo_movimentacao}, Data: {movimentacao.data}")
def menu():
produtos = [] 
movimentacoes = []
contador_produtos = 0
contador_movimentacoes = 0 
while True: 
escolha = int(input("Escolha uma ação:\n1 - Cadastrar novo produto\n2 - Consultar produto\n3 - Registrar movimentação\n4 - Consultar movimentações\n5 - Gerar relatório\n6 - Sair\nEscolha: "))
if escolha == 1:
contador_produtos = cadastrar_produtos(produtos, contador_produtos)
elif escolha == 2: 
id_produto = int(input("ID do produto para consulta: ")) 
consultar_produto_id(produtos, id_produto)
elif escolha == 3:
contador_movimentacoes = registrar_movimentacao(movimentacoes, contador_movimentacoes, produtos) 
elif escolha == 4:
id_produto = int(input("ID do produto para consultar movimentações: ")) 
consultar_movimentacoes(movimentacoes, id_produto)
elif escolha == 5: 
gerar_relatorio_estoque(produtos) 
elif escolha == 6:
print("Saindo do sistema...")
break
else:
print("Opção inválida!") 
# Executa o menu principal
menu()
