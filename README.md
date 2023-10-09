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

## Requisitos Mínimos:

- Código bem testado.
- Documentar em um README como seu código está estruturado, como rodá-lo e uma explicação sucinta das principais decisões técnicas que você tomou no seu código.

## Requisitos Opcionais:

- GraphQL: O schema pode refletir a mesma estrutura acima.

## Prazos:

- Consegue fazer até dia 27/09?
- Caso entregue antes, pontos extras!
- Em caso de dúvidas, basta responder a todos neste e-mail.
