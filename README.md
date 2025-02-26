app = Flask(__name__)

#
livros = {
    "1": {
        "título": "O Segredo do Vale",
        "autor_id": "1",
        "ano_publicacao": 2018,
        "gênero": "Ficção",
        "preco": 45.90
    },
    "2": {
        "título": "Viagem ao Espaço",
        "autor_id": "2",
        "ano_publicacao": 2020,
        "gênero": "Ficção Científica",
        "preco": 59.90
    },
    "3": {
        "título": "Histórias Perdidas",
        "autor_id": "3",
        "ano_publicacao": 2015,
        "gênero": "Mistério",
        "preco": 35.50
    }
}


    "1": {
        "nome": "Clara Mendes",
        "nacionalidade": "Brasileira",
        "ano_nascimento": 1980,
        "obras_notáveis": ["O Segredo do Vale", "Noites de Verão"]
    },
    "2": {
        "nome": "Marco Russo",
        "nacionalidade": "Italiano",
        "ano_nascimento": 1975,
        "obras_notáveis": ["Viagem ao Espaço", "O Código das Estrelas"]
    },
    "3": {
        "nome": "Elena Torres",
        "nacionalidade": "Mexicana",
        "ano_nascimento": 1990,
        "obras_notáveis": ["Histórias Perdidas", "O Enigma do Passado"]
    }
}

# Dicionário que representa um banco de dados fictício de clientes
clientes = {
    "1": {
        "nome": "João Silva",
        "email": "joao@email.com",
        "data_cadastro": "2020-05-15",
        "gêneros_favoritos": ["Ficção", "Mistério"],
        "livros_comprados": ["1", "3"]
    },
    "2": {
        "nome": "Ana Souza",
        "email": "ana.s@mail.com",
        "data_cadastro": "2019-08-20",
        "gêneros_favoritos": ["Ficção Científica"],
        "livros_comprados": ["2"]
    },
    "3": {
        "nome": "Carlos Lima",
        "email": "carlos.l@email.com",
        "data_cadastro": "2021-01-10",
        "gêneros_favoritos": ["Aventura", "Mistério"],
        "livros_comprados": ["3"]
    }
}

# Rota para obter a lista de todos os livros
@app.route("/livro", methods=["GET"])  # Define um endpoint acessível via método GET
def livro():
    return jsonify(livros), 200  # Retorna a lista de livros em formato JSON com status HTTP 200 (OK)


@app.route("/cliente", methods=["GET"])  
    return jsonify(clientes), 200  status HTTP 200 (OK)

# Rota para obter a lista de todos os autores
@app.route("/autor", methods=["GET"])  # Define um endpoint acessível via método GET
def autor():
    return jsonify(autores), 200  # Retorna a lista de autores em formato JSON com status HTTP 200 (OK)


@app.route("/delete_livro/<string:id>", methods=["DELETE"])  # Define um endpoint acessível via método DELETE
def delete_livro(id):
    del livros[id]  
    return jsonify(livros), 200  


@app.route("/add_livro", methods=["POST"])  
def add_livro():
    data = request.get_json()  
    livros[f"{len(livros) + 1}"] = data  
    return jsonify(livros), 200  #


@app.route("/up_livro", methods=["PUT"])  # Define um endpoint acessível via método PUT
def up_livro():
    data = request.get_json()  # Obtém os dados do corpo da requisição em formato JSON
    if data["id"] in livros:  # Verifica se o livro existe no dicionário
        for chave, valor in data.items():  # Percorre os campos enviados na requisição
            if chave != "id":  # Garante que o ID não seja alterado
                livros[data["id"]][chave] = valor  # Atualiza os campos do livro
        return jsonify(livros), 200  # Retorna a lista atualizada de livros com status HTTP 200 (OK)
    else:
        return jsonify({"erro": "Livro não encontrado"}), 404  # Retorna um erro caso o livro não seja encontrado

#
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')  # Executa o servidor Flask no modo debug e disponível para toda a rede
