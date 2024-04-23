![image](https://assets-global.website-files.com/61155c49f7b752684a9f0584/61201e989ae795462db99155_logo-arvore.svg)

# Backend challenge 

- [Níveis Estagiário e Júnior](#n%C3%ADveis-estagi%C3%A1rio-e-j%C3%BAnior)
- [Níveis Pleno e Sênior](#n%C3%ADveis-estagi%C3%A1rio-e-j%C3%BAnior)

## Níveis Estagiário e Júnior

### Contexto
Você está começando a desenvolver um sistema para a Árvore, que possui diversos parceiros que desejam replicar e administrar sua estrutura de Escolas e Turmas. O objetivo deste teste é construir uma pequena API que permita essa gestão de forma simples.

### Objetivo
Construir uma API usando a linguagem de sua preferência. O banco de dados pode ser SQLite ou um outro banco de sua preferência. A API deve permitir a um parceiro da Árvore replicar sua estrutura de Escolas e Turmas.

### Modelagem
A modelagem deverá utilizar apenas uma entidade (Entity), que poderá representar uma escola ou uma turma.

### Tipos
- **School:** Representa uma escola.
- **Class:** Representa uma turma e deve obrigatoriamente ser relacionado a uma escola.

### Atributos
- **name:** Nome da entidade.
- **entity_type:** Tipo da entidade.
- **parent_id:** Identificador da escola, caso a entidade seja uma turma. Se for uma escola, terá parent_id nulo.

### Exemplos de Requisições

#### Criação de uma entidade
**Request:**
```
POST /api/v1/entities
Headers:
Content-Type:application/json

Body:
{
  "name": "Escola Exemplo",
  "entity_type": "school",
  "parent_id": null
}
```

**Response:**
```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "data": {
    "id": 1,
    "entity_type": "school",
    "name": "Escola Exemplo",
    "parent_id": null,
    "subtree_ids": []
  }
}
```

#### Exibição de uma entidade
**Request:**
```
GET /api/v1/entities/id-da-entidade
Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 1
```

**Response:**
```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "data": {
    "id": 1,
    "entity_type": "school",
    "name": "Escola Exemplo",
    "parent_id": null,
    "subtree_ids": [2, 3]
  }
}
```

#### Deleção de uma entidade e seus respectivos filhos
**Request:**
```
DELETE /api/v1/entities/id-da-entidade
Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 1
```

**Response:**
```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "message": "Entidade e seus filhos deletados com sucesso."
}
```

### Requisitos mínimos
- Código simples e legível.
- Documentar em um README como seu código está estruturado, como rodá-lo e uma explicação sucinta das principais decisões técnicas que você tomou no seu código.
- Documentação da API.
- Testes.

### Diferenciais
- Uso do GraphQL.
- Uso da linguagem Elixir.

### O que vamos avaliar (Interno)
- Evolução (baseado na jornada, com entrega total ou parcial)
- Funcionalidades x Requisitos
- Git log
- Testes unitários
- Estrutura de consultas (SQL)

---

## Níveis Pleno e Sênior

### Contexto
A Árvore possui diversos parceiros que necessitam replicar e administrar sua estrutura de Redes, Escolas e Turmas. O objetivo deste teste é construir uma API que permita essa gestão de forma eficiente e segura. A modelagem deve ser pensada de forma que reflita a realidade dessas entidades e suas relações, mas sem se prender excessivamente a detalhes.

### Objetivo
Construir uma API usando uma das seguintes linguagens funcionais: Elixir, Clojure, Scala, Node ou Ruby. O banco de dados pode ser qualquer banco relacional de sua escolha. A API deve permitir a um parceiro da Árvore replicar sua estrutura de Redes, Escolas, Turmas e administrá-la conforme necessário. O acesso a esta API deve ser restrito com um mecanismo de autenticação usando uma ou mais chaves de acesso, vinculadas ao parceiro.

### Modelagem
A modelagem deverá utilizar apenas uma entidade (Entity), que poderá representar qualquer nível da estrutura hierárquica.

### Tipos
- **Network:** Representa uma rede de escolas. Não é um nível obrigatório.
- **School:** Representa uma escola, podendo ou não estar relacionada a uma rede.
- **Class:** Representa uma turma e deve obrigatoriamente ser relacionado a uma escola.

### Atributos
- **name:** Nome da entidade.
- **entity_type:** Tipo da entidade.
- **inep (opcional):** Código INEP, usado apenas para entity_type com valor "school".
- **parent_id:** Identificador da entidade antecessora na hierarquia. A entidade mais alta da hierarquia (network ou school) terá parent_id nulo.

### Exemplos de Requisições

#### Criação de uma entidade
**Request:**
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

**Response:**
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

#### Exibição de uma entidade
**Request:**
```
GET /api/v2/partners/entities/id-da-entidade
Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 2
```

**Response:**
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

#### Edição de uma entidade
**Request:**
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

**Response:**
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

#### Deleção de uma entidade e seus respectivos filhos
**Request:**
```
DELETE /api/v2/partners/entities/id-da-entidade
Headers:
Content-Type:application/json

Parameters:
id: integer - ex: 1
```

**Response:**
```
Headers:
Content-Type:application/json; charset=utf-8

Body:
{
  "message": "Entidade e seus filhos deletados com sucesso."
}
```

### Requisitos Mínimos
- Código bem testado.
- Documentar em um README como seu código está estruturado, como rodá-lo e uma explicação sucinta das principais decisões técnicas que você tomou no seu código.
- Documentação da API.

### Diferenciais
- GraphQL: O schema pode refletir a mesma estrutura acima.
- Integração com CI.
- Uso da linguagem Elixir.

### O que vamos avaliar (Interno)
- Evolução (baseado na jornada, com entrega total ou parcial)
- Histórico de commits
- Testes unitários
- Funcionalidades x Requisitos
- Testes implementados e diferentes níveis de cobertura
- Estrutura de consultas (SQL) e performance
- Dimensionamento de banco/storage
