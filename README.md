# Modelagem e-commerce SENAC-20260802_UC5
Modelagem de dados criado no Logic model BRMW
## Modelo Lógico
2
 
3
🔗 ## Modelagem do Banco de Dados

[Abrir modelagem no BRModelo](https://app.brmodeloweb.com/publicview/6a8b2ea357fca559ea8680db)

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

- BRModelo Web (Modelo Lógico Relacional)

## Autor

Luiz Oscar da Costa

Curso Técnico em IA

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
####################################

CREATE DATABASE teste;
USE teste;

-- =========================
-- CATEGORIAS
-- =========================
CREATE TABLE categoria (
    categoria_id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    slug VARCHAR(100) NOT NULL UNIQUE,
    categoria_pai_id INT NULL,
    ativo BOOLEAN DEFAULT TRUE,

    CONSTRAINT fk_categoria_pai
        FOREIGN KEY (categoria_pai_id)
        REFERENCES categoria(categoria_id)
);

-- =========================
-- MARCAS
-- =========================
CREATE TABLE marcas (
    marca_id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    site VARCHAR(255),
    ativo BOOLEAN DEFAULT TRUE
);

-- =========================
-- FORNECEDORES
-- =========================
CREATE TABLE fornecedores (
    fornecedor_id INT AUTO_INCREMENT PRIMARY KEY,
    razao_social VARCHAR(150) NOT NULL,
    nome_fantasia VARCHAR(150),
    cnpj VARCHAR(18) UNIQUE,
    email VARCHAR(150),
    telefone VARCHAR(20),
    prazo_medio_dias INT,
    ativo BOOLEAN DEFAULT TRUE
);

-- =========================
-- CENTROS DE DISTRIBUIÇÃO
-- =========================
CREATE TABLE centro_distribuicao (
    centro_distribuicao_id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cidade VARCHAR(100),
    uf CHAR(2),
    ativo BOOLEAN DEFAULT TRUE
);

-- =========================
-- CLIENTES
-- =========================
CREATE TABLE clientes (
    cliente_id INT AUTO_INCREMENT PRIMARY KEY,
    nome_completo VARCHAR(150) NOT NULL,
    email VARCHAR(150) UNIQUE,
    cpf VARCHAR(14) UNIQUE,
    telefone VARCHAR(20),
    data_nascimento DATE,
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    ativo BOOLEAN DEFAULT TRUE
);

-- =========================
-- CUPONS
-- =========================
CREATE TABLE cupons (
    cupom_id INT AUTO_INCREMENT PRIMARY KEY,
    codigo VARCHAR(50) NOT NULL UNIQUE,
    tipo_desconto VARCHAR(20),
    valor_desconto DECIMAL(10,2),
    valor_minimo DECIMAL(10,2),
    inicio_em DATE,
    fim_em DATE,
    limite_usos INT,
    usos_realizados INT DEFAULT 0,
    ativo BOOLEAN DEFAULT TRUE
);

-- =========================
-- PRODUTOS
-- =========================
CREATE TABLE produtos (
    produto_id INT AUTO_INCREMENT PRIMARY KEY,
    sku VARCHAR(50) UNIQUE,
    nome VARCHAR(150) NOT NULL,
    slug VARCHAR(150) UNIQUE,
    categoria_id INT,
    marca_id INT,
    fornecedor_id INT,
    preco_custo DECIMAL(10,2),
    preco_venda DECIMAL(10,2),
    peso_kg DECIMAL(8,3),
    garantia_meses INT,
    ativo BOOLEAN DEFAULT TRUE,

    CONSTRAINT fk_produto_categoria
        FOREIGN KEY (categoria_id)
        REFERENCES categoria(categoria_id),

    CONSTRAINT fk_produto_marca
        FOREIGN KEY (marca_id)
        REFERENCES marcas(marca_id),

    CONSTRAINT fk_produto_fornecedor
        FOREIGN KEY (fornecedor_id)
        REFERENCES fornecedores(fornecedor_id)
);

-- =========================
-- ENDEREÇOS
-- =========================
CREATE TABLE enderecos (
    endereco_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT NOT NULL,
    tipo VARCHAR(20),
    logradouro VARCHAR(150),
    numero VARCHAR(20),
    complemento VARCHAR(100),
    bairro VARCHAR(100),
    cidade VARCHAR(100),
    uf CHAR(2),
    cep VARCHAR(9),
    principal BOOLEAN DEFAULT FALSE,

    CONSTRAINT fk_endereco_cliente
        FOREIGN KEY (cliente_id)
        REFERENCES clientes(cliente_id)
);

-- =========================
-- ESTOQUE
-- =========================
CREATE TABLE estoques (
    estoque_id INT AUTO_INCREMENT PRIMARY KEY,
    produto_id INT NOT NULL,
    centro_id INT NOT NULL,
    quantidade INT DEFAULT 0,
    reservado INT DEFAULT 0,
    ponto_reposicao INT,
    atualizado_em DATETIME DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_estoque_produto
        FOREIGN KEY (produto_id)
        REFERENCES produtos(produto_id),

    CONSTRAINT fk_estoque_centro
        FOREIGN KEY (centro_id)
        REFERENCES centro_distribuicao(centro_distribuicao_id)
);

-- =========================
-- MOVIMENTAÇÃO DE ESTOQUE
-- =========================
CREATE TABLE movimentacao_estoque (
    movimentacao_estoque_id INT AUTO_INCREMENT PRIMARY KEY,
    produto_id INT NOT NULL,
    centro_id INT NOT NULL,
    tipo VARCHAR(20),
    quantidade INT,
    referencia VARCHAR(100),
    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_mov_produto
        FOREIGN KEY (produto_id)
        REFERENCES produtos(produto_id),

    CONSTRAINT fk_mov_centro
        FOREIGN KEY (centro_id)
        REFERENCES centro_distribuicao(centro_distribuicao_id)
);

-- =========================
-- PEDIDOS
-- =========================
CREATE TABLE pedidos (
    pedido_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT NOT NULL,
    endereco_entrega_id INT NOT NULL,

    status VARCHAR(30),

    subtotal DECIMAL(10,2),
    valor_desconto DECIMAL(10,2),
    valor_frete DECIMAL(10,2),
    valor_total DECIMAL(10,2),

    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
    atualizado_em DATETIME DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_pedido_cliente
        FOREIGN KEY (cliente_id)
        REFERENCES clientes(cliente_id),

    CONSTRAINT fk_pedido_endereco
        FOREIGN KEY (endereco_entrega_id)
        REFERENCES enderecos(endereco_id)
);

-- =========================
-- ITENS DO PEDIDO
-- =========================
CREATE TABLE itens_pedidos (
    item_pedidos_id INT AUTO_INCREMENT PRIMARY KEY,

    pedido_id INT NOT NULL,
    produto_id INT NOT NULL,
    centro_id INT NOT NULL,

    quantidade INT NOT NULL,

    preco_unitario DECIMAL(10,2),
    percentual_desconto DECIMAL(5,2),
    subtotal DECIMAL(10,2),

    CONSTRAINT fk_item_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id),

    CONSTRAINT fk_item_produto
        FOREIGN KEY (produto_id)
        REFERENCES produtos(produto_id),

    CONSTRAINT fk_item_centro
        FOREIGN KEY (centro_id)
        REFERENCES centro_distribuicao(centro_distribuicao_id)
);

-- =========================
-- PEDIDO x CUPOM
-- =========================
CREATE TABLE pedidos_cupons (
    pedido_cupons_id INT AUTO_INCREMENT PRIMARY KEY,

    pedido_id INT NOT NULL,
    cupom_id INT NOT NULL,

    valor_aplicado DECIMAL(10,2),

    CONSTRAINT fk_pc_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id),

    CONSTRAINT fk_pc_cupom
        FOREIGN KEY (cupom_id)
        REFERENCES cupons(cupom_id)
);

-- =========================
-- PAGAMENTOS
-- =========================
CREATE TABLE pagamentos (
    pagamento_id INT AUTO_INCREMENT PRIMARY KEY,

    pedido_id INT NOT NULL,

    metodo VARCHAR(30),
    parcelas INT,
    valor DECIMAL(10,2),

    status VARCHAR(20),
    codigo_transacao VARCHAR(100),

    processado_em DATETIME,

    CONSTRAINT fk_pagamento_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id)
);

-- =========================
-- ENTREGAS
-- =========================
CREATE TABLE entregas (
    entrega_id INT AUTO_INCREMENT PRIMARY KEY,

    pedido_id INT NOT NULL,

    transportadora VARCHAR(100),
    codigo_rastreio VARCHAR(100),

    status VARCHAR(30),

    previsao_entrega DATETIME,
    enviado_em DATETIME,
    entregue_em DATETIME,

    CONSTRAINT fk_entrega_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id)
);

-- =========================
-- HISTÓRICO DE STATUS
-- =========================
CREATE TABLE historico_status_pedido (
    historico_status_pedido_id INT AUTO_INCREMENT PRIMARY KEY,

    pedido_id INT NOT NULL,

    status_anterior VARCHAR(30),
    status_novo VARCHAR(30),
    observacao VARCHAR(255),

    alterado_em DATETIME DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_historico_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id)
);

-- =========================
-- AVALIAÇÕES
-- =========================
CREATE TABLE avaliacoes (
    avaliacao_id INT AUTO_INCREMENT PRIMARY KEY,

    cliente_id INT NOT NULL,
    produto_id INT NOT NULL,
    pedido_id INT NOT NULL,

    nota INT CHECK (nota BETWEEN 1 AND 5),

    titulo VARCHAR(100),
    comentario VARCHAR(500),

    criado_em DATETIME DEFAULT CURRENT_TIMESTAMP,

    aprovado BOOLEAN DEFAULT FALSE,

    CONSTRAINT fk_av_cliente
        FOREIGN KEY (cliente_id)
        REFERENCES clientes(cliente_id),

    CONSTRAINT fk_av_produto
        FOREIGN KEY (produto_id)
        REFERENCES produtos(produto_id),

    CONSTRAINT fk_av_pedido
        FOREIGN KEY (pedido_id)
        REFERENCES pedidos(pedido_id),

    CONSTRAINT uk_avaliacao
        UNIQUE(cliente_id, produto_id, pedido_id)
);

-- =========================
-- ÍNDICES PARA JOIN
-- =========================

CREATE INDEX idx_produtos_categoria
ON produtos(categoria_id);

CREATE INDEX idx_produtos_marca
ON produtos(marca_id);

CREATE INDEX idx_produtos_fornecedor
ON produtos(fornecedor_id);

CREATE INDEX idx_enderecos_cliente
ON enderecos(cliente_id);

CREATE INDEX idx_pedidos_cliente
ON pedidos(cliente_id);

CREATE INDEX idx_pedidos_endereco
ON pedidos(endereco_entrega_id);

CREATE INDEX idx_itens_pedido
ON itens_pedidos(pedido_id);

CREATE INDEX idx_itens_produto
ON itens_pedidos(produto_id);

CREATE INDEX idx_itens_centro
ON itens_pedidos(centro_id);

CREATE INDEX idx_estoque_produto
ON estoques(produto_id);

CREATE INDEX idx_estoque_centro
ON estoques(centro_id);

CREATE INDEX idx_pagamentos_pedido
ON pagamentos(pedido_id);

CREATE INDEX idx_entregas_pedido
ON entregas(pedido_id);

CREATE INDEX idx_avaliacoes_produto
ON avaliacoes(produto_id);

CREATE INDEX idx_avaliacoes_cliente
ON avaliacoes(cliente_id);
