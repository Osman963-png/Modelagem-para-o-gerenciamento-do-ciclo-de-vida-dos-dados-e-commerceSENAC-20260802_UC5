# Modelagem e-commerce SENAC-20260802_UC5
Modelagem de dados criado no Logic model BRMW
## Modelo Lógico
2
 
3
🔗 [Abrir modelagem no BRModelo]([https://app.brmodeloweb.com/]([https://app.brmodeloweb.com/logic/6a8af4ae57fca559ea867a4a](https://app.brmodeloweb.com/publicview/6a8b2ea357fca559ea8680db))

# Modelagem de Dados - E-commerce

## Sobre o Projeto

Esta atividade de Modelagem de Dados foi desenvolvida durante o curso Técnico em IA do Senac São Paulo. O objetivo foi aplicar os conceitos de análise de requisitos, modelagem conceitual e modelagem lógica para projetar um banco de dados voltado a um sistema de comércio eletrônico (e-commerce), Lojateck.

A modelagem foi elaborada utilizando a ferramenta BRModelo Web, permitindo a representação estruturada das entidades, atributos e relacionamentos necessários para o funcionamento do sistema.

## Objetivo da Modelagem

O banco de dados foi projetado para atender às principais operações de uma plataforma de vendas online, contemplando o cadastro de clientes, produtos, categorias, pedidos, pagamentos e demais informações relacionadas ao processo de compra.

A estrutura proposta busca garantir a integridade dos dados, reduzir redundâncias e facilitar a manutenção e evolução do sistema.

## Conceitos Aplicados

Durante o desenvolvimento desta atividade foram aplicados os seguintes conceitos:

- Levantamento de requisitos.
- Modelagem de banco de dados relacional.
- Definição de entidades e atributos.
- Chaves primárias e estrangeiras.
- Relacionamentos entre tabelas.
- Normalização de dados.
- Integridade referencial.

## Modelo Lógico

O modelo lógico apresenta a organização das tabelas do banco de dados e os relacionamentos entre elas, servindo como base para a futura implementação em um Sistema Gerenciador de Banco de Dados (SGBD).

A modelagem foi construída considerando as regras de negócio de um ambiente de comércio eletrônico, permitindo o registro e acompanhamento das operações realizadas pelos usuários da plataforma.

## Benefícios da Estrutura Proposta

- Organização eficiente das informações.
- Facilidade para consultas e relatórios.
- Controle dos dados de clientes e produtos.
- Registro do histórico de pedidos.
- Maior consistência e segurança das informações.
- Escalabilidade para futuras funcionalidades.

## Ferramenta Utilizada

- BRModelo Web
- Modelo Lógico Relacional

## Autor

Luiz Oscar da Costa

Curso Técnico em Informática para Internet

Senac São Paulo



# E-commerce Data Modeling

## About the Project

This Data Modeling activity was developed during the Artificial Intelligence Technical Course at Senac São Paulo. The objective was to apply the concepts of requirements analysis, conceptual modeling, and logical modeling to design a database for an e-commerce system called Lojateck.

The model was created using the BRModelo Web tool, allowing a structured representation of the entities, attributes, and relationships required for the system's operation.

## Modeling Objective

The database was designed to support the main operations of an online sales platform, including the management of customers, products, categories, orders, payments, and other information related to the purchasing process.

The proposed structure aims to ensure data integrity, reduce redundancy, and facilitate system maintenance and future evolution.

## Applied Concepts

The following concepts were applied during the development of this project:

- Requirements gathering.
- Relational database modeling.
- Definition of entities and attributes.
- Primary and foreign keys.
- Relationships between tables.
- Data normalization.
- Referential integrity.

## Logical Model

The logical model presents the organization of database tables and the relationships between them, serving as the foundation for future implementation in a Database Management System (DBMS).

The model was developed according to the business rules of an e-commerce environment, enabling the registration and monitoring of operations performed by platform users.

## Benefits of the Proposed Structure

- Efficient information organization.
- Easier data querying and reporting.
- Customer and product data management.
- Order history tracking.
- Improved data consistency and security.
- Scalability for future features and enhancements.

## Tools Used

- BRModelo Web
- Relational Logical Model

## Author

Luiz Oscar da Costa

Artificial Intelligence Technical Course

Senac São Paulo



## Como executar

1. Criar o banco:
```sql
CREATE DATABASE teste;
USE teste;

CREATE DATABASE teste;
USE teste;
CREATE TABLE categoria (
    categoria_id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    slug VARCHAR(100),
    categoria_pai_id INT,
    ativo BOOLEAN
);

CREATE TABLE marcas (
    marca_id INT PRIMARY KEY,
    nome VARCHAR(100),
    site VARCHAR(255),
    ativo BOOLEAN
);


CREATE TABLE fornecedores (
    fornecedor_id INT AUTO_INCREMENT PRIMARY KEY,
    razao_social VARCHAR(150),
    nome_fantasia VARCHAR(150),
    cnpj VARCHAR(18),
    email VARCHAR(150),
    telefone VARCHAR(20),
    prazo_medio_dias INT,
    ativo BOOLEAN
);

USE teste;

CREATE TABLE centro_distribuicao (
    centro_distribuicao_id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) DEFAULT 'nome',
    cidade VARCHAR(100),
    uf CHAR(2),
    ativo BOOLEAN
);

CREATE TABLE clientes (
    cliente_id INT AUTO_INCREMENT PRIMARY KEY,
    nome_completo VARCHAR(150),
    email VARCHAR(150),
    cpf VARCHAR(14),
    telefone VARCHAR(20),
    data_nascimento DATE,
    criado_em DATE,
    ativo BOOLEAN
);

CREATE TABLE cupons (
    cupom_id INT AUTO_INCREMENT PRIMARY KEY,
    codigo VARCHAR(50),
    tipo_desconto VARCHAR(20),
    valor_desconto DECIMAL(10,2),
    valor_minimo DECIMAL(10,2),
    inicio_em DATE,
    fim_em DATE,
    limite_usos INT,
    usos_realizados INT,
    ativo BOOLEAN
);

CREATE TABLE produtos (
    produto_id INT AUTO_INCREMENT PRIMARY KEY,
    sku VARCHAR(50),
    nome VARCHAR(150),
    slug VARCHAR(150),
    categoria_id INT,
    marca_id INT,
    fornecedor_id INT,
    preco_custo DECIMAL(10,2),
    preco_venda DECIMAL(10,2),
    peso_kg DECIMAL(8,3),
    garantia_meses INT,
    ativo BOOLEAN,
    
    FOREIGN KEY (categoria_id) REFERENCES categoria(categoria_id),
    FOREIGN KEY (marca_id) REFERENCES marcas(marca_id),
    FOREIGN KEY (fornecedor_id) REFERENCES fornecedores(fornecedor_id)
);
CREATE TABLE enderecos (
    endereco_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    tipo VARCHAR(20),
    logradouro VARCHAR(150),
    numero VARCHAR(20),
    complemento VARCHAR(100),
    bairro VARCHAR(100),
    cidade VARCHAR(100),
    uf CHAR(2),
    cep VARCHAR(9),
    principal BOOLEAN,

    FOREIGN KEY (cliente_id) REFERENCES clientes(cliente_id)
);

CREATE TABLE estoques (
    estoque_id INT AUTO_INCREMENT PRIMARY KEY,
    produto_id INT,
    centro_id INT,
    quantidade INT,
    reservado INT,
    ponto_reposicao INT,
    atualizado_em DATETIME,

    FOREIGN KEY (produto_id) REFERENCES produtos(produto_id),
    FOREIGN KEY (centro_id) REFERENCES centro_distribuicao(centro_distribuicao_id)
);


CREATE TABLE movimentacao_estoque (
    movimentacao_estoque_id INT AUTO_INCREMENT PRIMARY KEY,
    produto_id INT,
    centro_id INT,
    tipo VARCHAR(20),
    quantidade INT,
    referencia VARCHAR(100),
    criado_em DATETIME,

    FOREIGN KEY (produto_id) REFERENCES produtos(produto_id),
    FOREIGN KEY (centro_id) REFERENCES centro_distribuicao(centro_distribuicao_id)
);

CREATE TABLE pedidos (
    pedido_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    endereco_entrega_id INT,
    status VARCHAR(30),
    subtotal DECIMAL(10,2),
    valor_desconto DECIMAL(10,2),
    valor_frete DECIMAL(10,2),
    valor_total DECIMAL(10,2),
    criado_em DATETIME,
    atualizado_em DATETIME,

    FOREIGN KEY (cliente_id) REFERENCES clientes(cliente_id),
    FOREIGN KEY (endereco_entrega_id) REFERENCES enderecos(endereco_id)
);

CREATE TABLE itens_pedidos (
    item_pedidos_id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    produto_id INT,
    centro_id INT,
    quantidade INT,
    preco_unitario DECIMAL(10,2),
    percentual_desconto DECIMAL(5,2),
    subtotal DECIMAL(10,2),

    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id),
    FOREIGN KEY (produto_id) REFERENCES produtos(produto_id),
    FOREIGN KEY (centro_id) REFERENCES centro_distribuicao(centro_distribuicao_id)
);

CREATE TABLE pedidos_cupons (
    pedido_cupons_id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    cupom_id INT,
    valor_aplicado DECIMAL(10,2),

    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id),
    FOREIGN KEY (cupom_id) REFERENCES cupons(cupom_id)
);

CREATE TABLE pagamentos (
    pagamento_id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    metodo VARCHAR(30),
    parcelas INT,
    valor DECIMAL(10,2),
    status VARCHAR(20),
    codigo_transacao VARCHAR(100),
    processado_em DATETIME,

    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id)
);

CREATE TABLE entregas (
    entrega_id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    transportadora VARCHAR(100),
    codigo_rastreio VARCHAR(100),
    status VARCHAR(30),
    previsao_entrega DATETIME,
    enviado_em DATETIME,
    entregue_em DATETIME,

    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id)
);

CREATE TABLE historico_status_pedido (
    historico_status_pedido_id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    status_anterior VARCHAR(30),
    status_novo VARCHAR(30),
    observacao VARCHAR(255),
    alterado_em DATETIME,

    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id)
);

CREATE TABLE avaliacoes (
    avaliacao_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    produto_id INT,
    pedido_id INT,
    nota INT,
    titulo VARCHAR(100),
    comentario VARCHAR(500),
    criado_em DATETIME,
    aprovado BOOLEAN,

    FOREIGN KEY (cliente_id) REFERENCES clientes(cliente_id),
    FOREIGN KEY (produto_id) REFERENCES produtos(produto_id),
    FOREIGN KEY (pedido_id) REFERENCES pedidos(pedido_id)
);


ALTER TABLE categoria
ADD FOREIGN KEY (categoria_pai_id)
REFERENCES categoria(categoria_id);

ALTER TABLE produtos
ADD FOREIGN KEY (categoria_id)
REFERENCES categoria(categoria_id);

ALTER TABLE produtos
ADD FOREIGN KEY (marca_id)
REFERENCES marcas(marca_id);

ALTER TABLE produtos
ADD FOREIGN KEY (fornecedor_id)
REFERENCES fornecedores(fornecedor_id);

ALTER TABLE enderecos
ADD FOREIGN KEY (cliente_id)
REFERENCES clientes(cliente_id);

ALTER TABLE estoques
ADD FOREIGN KEY (produto_id)
REFERENCES produtos(produto_id);

ALTER TABLE estoques
ADD FOREIGN KEY (centro_id)
REFERENCES centro_distribuicao(centro_distribuicao_id);

ALTER TABLE movimentacao_estoque
ADD FOREIGN KEY (produto_id)
REFERENCES produtos(produto_id);

ALTER TABLE movimentacao_estoque
ADD FOREIGN KEY (centro_id)
REFERENCES centro_distribuicao(centro_distribuicao_id);

ALTER TABLE pedidos
ADD FOREIGN KEY (cliente_id)
REFERENCES clientes(cliente_id);

ALTER TABLE pedidos
ADD FOREIGN KEY (endereco_entrega_id)
REFERENCES enderecos(endereco_id);

ALTER TABLE itens_pedidos
ADD FOREIGN KEY (pedido_id)
REFERENCES pedidos(pedido_id);

ALTER TABLE itens_pedidos
ADD FOREIGN KEY (produto_id)
REFERENCES produtos(produto_id);

ALTER TABLE itens_pedidos
ADD FOREIGN KEY (centro_id)
REFERENCES centro_distribuicao(centro_distribuicao_id);

ALTER TABLE pedidos_cupons
ADD FOREIGN KEY (cupom_id)
REFERENCES cupons(cupom_id);

ALTER TABLE pagamentos
ADD FOREIGN KEY (pedido_id)
REFERENCES pedidos(pedido_id);

ALTER TABLE entregas
ADD FOREIGN KEY (pedido_id)
REFERENCES pedidos(pedido_id);

ALTER TABLE historico_status_pedido
ADD FOREIGN KEY (pedido_id)
REFERENCES pedidos(pedido_id);

ALTER TABLE avaliacoes
ADD FOREIGN KEY (cliente_id)
REFERENCES clientes(cliente_id);

ALTER TABLE avaliacoes
ADD FOREIGN KEY (produto_id)
REFERENCES produtos(produto_id);

ALTER TABLE avaliacoes
ADD FOREIGN KEY (pedido_id)
REFERENCES pedidos(pedido_id);
