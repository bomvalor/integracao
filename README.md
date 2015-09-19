# Bomvalor.com

O [Bomvalor.com](http://bomvalor.com) é um site que reúne as melhores ofertas em leilões oficiais na Internet e facilita.

Nós estamos sempre abertos a novas parcerias e a publicação de novos leilões. Por isso criamos este documento para ajudá-lo a preparar os seus leilões para serem publicados no Bomvalor. Se ainda houver alguma dúvida mande para nós no email [contato@bomvalor.com](contato@bomvalor.com).


## Como faço para que meus leilões apareçam no Bomvalor?

A primeira coisa que você precisa fazer é entrar em contato com a gente. Mande um email para [contato@bomvalor.com](contato@bomvalor.com) com o endereço do seu site.

Depois você vai precisar criar duas páginas no seu site com um formato específico ([JSON](https://pt.wikipedia.org/wiki/JSON)). Provavelmente você vai precisar da ajuda de algum programador. Em uma das página estarão as informações sobre os leilões e na outra as informações sobre os lotes. Nas próximas seções você encontrará mais detalhes sobre como essas páginas precisam ser criadas.

Depois de criadas as páginas você precisa enviar para nós o endereço em que elas foram publicadas. À partir dai nós iremos fazer a leitura destes arquivos todos os dias e seus leilões serão mostrados no Bomvalor.

## Leilões

A primeira página que você precisa criar é a que mostrará os dados dos leilões. Esta página deve conter um arquivo JSON com os dados do leilão.

Para facilitar a validação e a identificação precoce de erros nesse arquivo nós criamos um schema JSON para este JSON.
Um schema define o formato do arquivo, como quais os campos, tipos de dados e tamanho máximo permitidos. Você pode verificar o schema de leilões em  **schemas/leilao.json**. Você encontra mais informações sobre JSON Schema no [site do projeto](http://json-schema.org/).


### Arquivo de exemplo:
Abaixo  está um exemplo de como ficará o seu arquivo. Observe que a data e hora precisam estar no formato rfc3339 com o fuso horário especificado. Os acentos e caracteres especiais devem ser codificados.

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
    "endereco": "Local do Leilao"
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

O formato do arquivo é parecido com o arquivo de leilões. Também é um array de objetos e cada objeto deverá respeitar o schema definido no arquivo **schemas/lote.json**.


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
