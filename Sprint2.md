# Entregável.02 — Mapa do Domínio

## Entidades

### CLIENTE
- id_cliente — PK
- nome
- telefone

### VEÍCULO
- id_veiculo — PK
- placa
- modelo
- id_cliente — FK

### ORDEM DE SERVIÇO
- id_ordem — PK
- data
- descrição
- id_veiculo — FK

## Relacionamentos

- Cliente possui Veículo — 1:N
- Veículo possui Ordem de Serviço — 1:N

## Diagrama ER

```mermaid

erDiagram
    CLIENTE ||--o{ VEICULO : possui
    VEICULO ||--o{ ORDEM_SERVICO : possui

    CLIENTE {
        int id_cliente PK
        string nome
        string telefone
    }

    VEICULO {
        int id_veiculo PK
        string placa
        string modelo
        int id_cliente FK
    }

    ORDEM_SERVICO {
        int id_ordem PK
        date data
        string descricao
        int id_veiculo FK
    }

CREATE TABLE cliente (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100),
    telefone VARCHAR(20)
);

CREATE TABLE veiculo (
    id_veiculo INT PRIMARY KEY,
    placa VARCHAR(10),
    modelo VARCHAR(100),
    id_cliente INT,
    FOREIGN KEY (id_cliente)
        REFERENCES cliente(id_cliente)
);

CREATE TABLE ordem_servico (
    id_ordem INT PRIMARY KEY,
    data DATE,
    descricao VARCHAR(255),
    id_veiculo INT,
    FOREIGN KEY (id_veiculo)
        REFERENCES veiculo(id_veiculo)
);
