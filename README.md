![image](https://assets-global.website-files.com/61155c49f7b752684a9f0584/61201e989ae795462db99155_logo-arvore.svg)

<div id="user-content-toc">
  <ul>
    <summary><h1 style="display: inline-block;">Challenge Backend</h1></summary>
  </ul>
</div>

## Contexto:

A Árvore possui diversos parceiros que necessitam replicar e administrar sua estrutura de Redes, Escolas e Turmas. O objetivo deste teste é construir uma API que permita essa gestão de forma eficiente e segura. A modelagem deve ser pensada de forma que reflita a realidade dessas entidades e suas relações, mas sem se prender excessivamente a detalhes.

## Objetivo:

Construir uma API usando uma das seguintes linguagens funcionais: Elixir, Clojure, Scala ou Ruby. O banco de dados pode ser qualquer banco relacional de sua escolha. A API deve permitir a um parceiro da Árvore replicar sua estrutura de Redes, Escolas, Turmas e administrá-la conforme necessário. O acesso a esta API deve ser restrito com um mecanismo de autenticação usando uma ou mais chaves de acesso, vinculadas ao parceiro.

## Modelagem:

A modelagem deverá utilizar apenas uma entidade (Entity), que poderá representar qualquer nível da estrutura hierárquica.

### Tipos:

- **Network**: Representa uma rede de escolas. Não é um nível obrigatório.
- **School**: Representa uma escola, podendo ou não estar relacionada a uma rede.
- **Class**: Representa uma turma e deve obrigatoriamente ser relacionado a uma escola.

### Atributos:

- **name**: Nome da entidade.
- **entity_type**: Tipo da entidade.
- **inep** (opcional): Código INEP, usado apenas para `entity_type` com valor "school".
- **parent_id**: Identificador da entidade antecessora na hierarquia. A entidade mais alta da hierarquia (network ou school) terá `parent_id` nulo.

## Exemplos de Requisições:

### Criação de uma entidade:

No exemplo abaixo, uma escola sem um antecessor hierárquico está sendo criada.

**Request**:

```
POST /api/v2/partners/entities

Headers:
Content-Type:application/json

Body:
{
  "name": "Escola Exemplo",
  "entity_type": "school",
  "inep": "123456",
  "parent_id": null
}
```

**Response**:

```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "data": {
    "id": 2,
    "entity_type": "school",
    "inep": "123456",
    "name": "Escola Exemplo",
    "parent_id": null,
    "subtree_ids": []
  }
}
```

*Nota*: A chave `subtree_ids` deverá trazer uma lista com os IDs de todas as entidades relacionadas à entidade retornada.

### Exibição de uma entidade:

**Request**:

```
GET /api/v2/partners/entities/id-da-entidade

Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 2
```

**Response**:

```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "data": {
    "id": 2,
    "entity_type": "school",
    "inep": "123456",
    "name": "Escola Exemplo",
    "parent_id": null,
    "subtree_ids": [3, 4]
  }
}
```

### Edição de uma entidade:

**Request**:

```
PUT /api/v2/partners/entities/id-da-entidade

Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 2

Body:
{
  "name": "Escola Exemplo",
  "entity_type": "school",
  "inep": "789123",
  "parent_id": null
}
```

**Response**:

```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "data": {
    "id": 2,
    "entity_type": "school",
    "inep": "789123",
    "name": "Escola Exemplo",
    "parent_id": null,
    "subtree_ids": [3, 4]
  }
}
```

## Requisitos Mínimos:

- Código bem testado.
- Documentar em um README como seu código está estruturado, como rodá-lo e uma explicação sucinta das principais decisões técnicas que você tomou no seu código.
- Documentação da API.

## Diferenciais:

- GraphQL: O schema pode refletir a mesma estrutura acima.
- Integração com CI.
