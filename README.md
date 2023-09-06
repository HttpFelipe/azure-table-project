# Azure Table Project - API de Contatos

<img src="https://www.viperit.com.br/wp-content/uploads/2021/12/blog-azure-1200x628-min.png">

Este é um projeto que implementa uma API para gerenciar uma tabela de contatos usando o serviço Azure Table Storage. A API permite criar, atualizar, listar, obter por nome e deletar contatos armazenados na tabela.

# Configuração

    SAConnectionString: A string de conexão para o serviço de armazenamento do Azure Table.
    AzureTableName: O nome da tabela onde os contatos serão armazenados.

# Modelo de Contato

A classe Contato implementa a interface ITableEntity. Ela possui as seguintes propriedades:

    Nome: O nome do contato.
    Telefone: O número de telefone do contato.
    Email: O endereço de e-mail do contato.
    PartitionKey: A chave de partição da tabela, neste caso, utilizamos o mesmo valor da RowKey.
    RowKey: A chave da linha, neste caso, é gerada um novo valor único usando Guid.NewGuid().ToString().
    Timestamp: A data e hora da última atualização do contato (gerenciado pelo Azure Table Storage).
    ETag: Uma tag de controle de concorrência (gerenciado pelo Azure Table Storage).

# Endpoints da API

Criar Contato

    Endpoint: POST /Contato
    Descrição: Cria um novo contato na tabela.
    Corpo da Requisição: Um objeto JSON representando os dados do contato (Nome, Telefone e Email).
    Resposta: Retorna o objeto JSON do contato criado com as informações completas, incluindo as propriedades PartitionKey, RowKey, Timestamp e ETag.

Atualizar Contato

    Endpoint: PUT /Contato/{id}
    Descrição: Atualiza um contato existente na tabela.
    Parâmetros: id (string, obrigatório) - A RowKey do contato a ser atualizado.
    Corpo da Requisição: Um objeto JSON representando os dados do contato a serem atualizados (Nome, Telefone e Email).
    Resposta: Retorna um código 200 OK em caso de sucesso.

Listar Todos os Contatos

    Endpoint: GET /Contato/Listar
    Descrição: Lista todos os contatos armazenados na tabela.
    Resposta: Retorna um objeto JSON contendo uma lista com todos os contatos.

Obter Contato por Nome

    Endpoint: GET /Contato/{nome}
    Descrição: Obtém uma lista de contatos que correspondem ao nome fornecido.
    Parâmetros: nome (string, obrigatório) - O nome do contato a ser pesquisado.
    Resposta: Retorna um objeto JSON contendo uma lista com os contatos encontrados.

Deletar Contato

    Endpoint: DELETE /Contato/{id}
    Descrição: Deleta um contato da tabela.
    Parâmetros: id (string, obrigatório) - A RowKey do contato a ser deletado.
    Resposta: Retorna um código 204 No Content em caso de sucesso.
