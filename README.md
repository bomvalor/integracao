# Bomvalor.com

O [Bomvalor.com](http://bomvalor.com) é um site que reúne as melhores ofertas em leilões oficiais na Internet.

Nós estamos sempre abertos a novas parcerias e a publicação de novos leilões. Por isso criamos este documento para ajudá-lo a preparar os seus leilões para serem publicados no Bomvalor. Se ainda houver alguma dúvida mande para nós no email [contato@bomvalor.com](contato@bomvalor.com).


## Como faço para que meus leilões apareçam no Bomvalor?

A primeira coisa que você precisa fazer é entrar em contato com a gente. Mande um email para [contato@bomvalor.com](contato@bomvalor.com) com o endereço do seu site.

Depois você vai precisar criar duas páginas no seu site com um formato específico ([JSON](https://pt.wikipedia.org/wiki/JSON)).
Provavelmente você vai precisar da ajuda de algum programador. Em uma das página estarão as informações sobre os leilões e na
outra as informações sobre os lotes. Nas próximas seções você encontrará mais detalhes sobre como essas páginas precisam ser criadas.

Depois de criadas as páginas você precisa enviar para nós o endereço em que elas foram publicadas.
À partir dai nós iremos fazer a leitura destes arquivos todos os dias e seus leilões serão mostrados no Bomvalor.

## Leilões

A primeira página que você precisa criar é a que mostrará os dados dos leilões. Esta página deve conter um arquivo JSON com todas as informações dos leilões.


### Descrição dos campos

- **id_leilao (obrigatório)**: Id do leilão que será usado para relacionar os lotes aos leilões. String com tamanho máximo de 64.

- **url (obrigatório)**: Endereço da página com detalhes do leilão. Precisa ser uma URL válida com tamanho máximo de 200 caracteres.

- **titulo (obrigatório)**: Descriçao curta do Leilão. String com tamanho máximo de 100 caracteres.

- **descricao**: Descrição mais completa do leilão. String com tamanho máximo de 1000 caracteres.

- **leiloeiro**: Nome do leiloeiro responsável pelo leilão. String com tamanho máximo de 70 caracteres.

- **datahora_abertura**: Data e hora de abertura do leilão. String com data e hora no formato rfc3339.

- **datahora_encerramento (obrigatório)**: Data e hora de encerramento do leilão. String com data e hora no formato
rfc3339.

- **cidade**: Nome da cidade onde será realizado o leilão. String com tamanho máximo de 70 caracteres.

- **estado**: UF onde será realizado o leilão. Deve ser informada a sigla do estado com 2 caracteres em maiúsculo.

- **endereco**: Endereço onde será realizado o leilão. Apenas para leilões presenciais.String com tamanho máximo de 150 caracteres.

- **online**: Campo boolean que indica se os compradores poderão enviar lances online. O valor padrão para este campo quando não informado é **true**.

- **presencial**: Campo boolean que indica se o leilão será realizado presencialmente. O valor padrão para este campo quando não informado é **false**.


Para facilitar a validação e a identificação precoce de erros nesse arquivo nós criamos um schema JSON para este JSON.
Um schema define o formato do arquivo, como quais os campos, tipos de dados e tamanho máximo permitidos.
Você pode verificar o schema de leilões em  **schemas/leilao.json**. Você encontra mais informações sobre o que é e como
funciona um "JSON Schema" no [site do projeto](http://json-schema.org/).


### Arquivo de exemplo:
Abaixo  está um exemplo de como ficará o seu arquivo. Observe que os acentos e caracteres especiais devem ser codificados.

```json
[
  {
    "id_leilao": "1",
    "url": "http://www.seusite.com.br/detalhe-do-leilao/?id=1",
    "titulo": "Leil\u00e3o de Imoveis",
    "descricao": "Leilao com diversos imoveis",
    "datahora_abertura": "2015-09-15T00:00:00+03:00",
    "datahora_encerramento": "2015-09-30T14:00:00+03:00",
    "cidade": "Florian\u00f3polis",
    "estado": "SC",
    "endereco": "Local do Leilao",
    "presencial": true,
    "online": true,
    "presencial": true
  },
  {
    "id_leilao": "2",
    "url": "http://www.seusite.com.br/detalhe-do-leilao/?id=2",
    "titulo": "Leil\u00e3o de Carros",
    "descricao": "Leilao com diversos automoveis",
    "datahora_abertura": "2015-09-15T00:00:00+03:00",
    "datahora_encerramento": "2015-09-30T14:00:00+03:00",
    "cidade": "S\\u00e3o Paulo",
    "estado": "SP",
    "endereco": "Local do Leilao"
  }
]
```

## Lotes

O formato do arquivo é parecido com o arquivo de leilões. Também é um array de objetos. Abaixo a descrição dos campos do objeto.


### Descrição dos campos

- **id_lote (obrigatório)**: Id do lote. String com tamanho máximo de 64 caracteres.

- **id_leilao (obrigatório)**: Id do leilão em que este lote será leiloado. String com tamanho máximo de 64.

- **url (obrigatório)**: Endereço da página com detalhes do lote. Precisa ser uma URL válida com tamanho máximo de 200 caracteres.

- **numero_lote (obrigatório)**: Número do lote. String com tamanho máximo de 20 caracteres.

- **titulo (obrigatório)**: Descrição curta do lote. String com tamanho máximo de 100 caracteres.

- **descricao (obrigatório)**: Descrição mais completa do lote. String com tamanho máximo de 1000 caracteres.

- **comitente**: Nome do comitente deste lote. String com tamanho máximo de 70 caracteres.

- **status (obrigatório)** (Obrigatório): Status atual do lote. Este campo precisa ter um dos seguintes valores: *"disponivel"*, *"encerrado"*, *"suspenso"*, *"arrematado"* ou *"propostas"*.

- **visitacao_permitida**: Campo boolean que indica se é permitida a visitação ao lote. O valor padrão para este campo quando não informado é **true**.

- **datahora_abertura**: Data e hora de abertura do lote. Para lotes com 2 praças está será a data de abertura da primeira praça. String com data e hora no formato rfc3339.

- **datahora_encerramento (obrigatório)**: Data e hora de encerramento do lote. Para lotes com 2 praças está será a data de encerramento da primeira praça. String com data e hora no formato rfc3339.

- **valor_lance_inicial (obrigatório)**: Valor do lance inicial do lote. Valor numérico com 2 casas decimais e decimais separados por ponto. Para lances com 2 praças este é o valor inicial da primeira praça.

- **datahora_abertura_2**: Data e hora de abertura da segunda praça do lote. String com data e hora no formato rfc3339.

- **datahora_encerramento_2**: Data e hora de encerramento da segunda praça do lote. String com data e hora no formato rfc3339.

- **valor_lance_inicial_2**: Valor do lance inicial da segunda praça do lote. Valor numérico com 2 casas decimais e decimais separados por ponto.

- **valor_lance_atual (obrigatório)**: Valor atual do lote. Valor numérico com 2 casas decimais e decimais separados por ponto.

- **nome_cidade (obrigatório)**: Nome da cidade onde está localizado o lote. String com tamanho máximo de 70 caracteres.

- **estado (obrigatório)**: UF onde está localizado o lote. Deve ser informada a sigla do estado com 2 caracteres em maiúsculo.

- **qtd_lances (obrigatório)**: Número de lances que o lote já recebeu. Valor numérico inteiro.

- **qtd_visualizacoes**: Número de visitas que o lote recebeu no seu site. Valor númerico inteiro.

- **subcategoria (obrigatório)**: Nome da categoria em que será incluído o lote. String com máximo de 100 caracteres.

- **imagens**: Lista de urls das imagens do lote.


Você encontra o schema do objeto lote em **schemas/lote.json**.

### Arquivo de exemplo:

Abaixo o exemplo de como ficará o seu arquivo.

```json
[
  {
    "id_lote": "123",
    "id_leilao": "1",
    "url": "http://www.seusite.com.br/detalhe-do-lote/?id=123&leilao=1",
    "numero_lote": "1",
    "titulo": "Titulo do lote claro e direto",
    "descricao": "Texto longo com com descri\\u00e7\\u00e3o do lote. Utilizar \\n para pular linhas.",
    "comitente": "Nome do Comitente",
    "visitacao_permitida": true,
    "status":  "disponivel",
    "valor_lance_inicial": 1234000.00,
    "valor_lance_atual": 12345000.00,
    "datahora_abertura": "2015-01-01T00:00:00+03:00",
    "datahora_encerramento": "2016-01-01T15:00:00+03:00",
    "nome_cidade": "S\\u00e3o Paulo",
    "estado": "SP",
    "subcategoria": "Automoveis",
    "imagens": [
      { "url": "http://www.seusite.com.br/imagens/lote123/1.jpg" },
      { "url": "http://www.seusite.com.br/imagens/lote123/2.jpg" },
      { "url": "http://www.seusite.com.br/imagens/lote123/3.jpg" }
    ]
  },
  {
    "id_lote": "124",
    "id_leilao": "1",
    "url": "http://www.seusite.com.br/detalhe-do-lote/?id=124&leilao=1",
    "numero_lote": "2",
    "titulo": "Titulo de outro lote claro e direto",
    "descricao": "Texto longo com com descri\\u00e7\\u00e3o do lote. Utilizar \\n para pular linhas.",
    "comitente": "Nome do Comitente",
    "visitacao_permitida": true,
    "status":  "disponivel",
    "valor_lance_inicial": 12340.00,
    "valor_lance_atual": 12340.00,
    "datahora_abertura": "2015-01-01T00:00:00+03:00",
    "datahora_encerramento": "2016-01-01T15:30:00+03:00",
    "nome_cidade": "Campinas",
    "estado": "SP",
    "subcategoria": "Apartamentos",
    "imagens": [
      { "url": "http://www.seusite.com.br/imagens/lote-124/1.jpg" },
      { "url": "http://www.seusite.com.br/imagens/lote-124/2.jpg" },
      { "url": "http://www.seusite.com.br/imagens/lote-124/3.jpg" },
      { "url": "http://www.seusite.com.br/imagens/lote-124/4.jpg" },
    ]
  }
]
```



## Atenção

- O seu site reutiliza IDs de leilões ou lote? Por exemplo, o site pode ter um novo leilão ou lote daqui a alguns meses com o mesmo número identificador? Nos avise em caso positivo.
