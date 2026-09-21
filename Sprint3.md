## Entregavel3 - Do Conceito à Tabela

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
- descricao
- id_veiculo — FK

---

## 2. Normalização

### 1ª Forma Normal (1FN)

Os atributos são atômicos e não existem grupos repetitivos.

### 2ª Forma Normal (2FN)

Não existem dependências parciais dos atributos em relação à chave.

### 3ª Forma Normal (3FN)

Não existem dependências transitivas entre atributos não-chave.

A estrutura foi organizada para evitar redundância e manter cada
informação em sua entidade apropriada.

---

## 3. SQL — CREATE TABLE


CREATE TABLE cliente (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20)
);

CREATE TABLE veiculo (
    id_veiculo INT PRIMARY KEY,
    placa VARCHAR(10) NOT NULL UNIQUE,
    modelo VARCHAR(100) NOT NULL,
    id_cliente INT NOT NULL,

    FOREIGN KEY (id_cliente)
        REFERENCES cliente(id_cliente)
);

CREATE TABLE ordem_servico (
    id_ordem INT PRIMARY KEY,
    data DATE NOT NULL,
    descricao VARCHAR(255),
    id_veiculo INT NOT NULL,

    FOREIGN KEY (id_veiculo)
        REFERENCES veiculo(id_veiculo)
);

INSERT INTO cliente (id_cliente, nome, telefone)
VALUES
(1, 'Ana Silva', '99999-1111'),
(2, 'Bruno Costa', '99999-2222'),
(3, 'Carlos Lima', '99999-3333');

INSERT INTO veiculo (id_veiculo, placa, modelo, id_cliente)
VALUES
(1, 'ABC1D23', 'Honda Civic', 1),
(2, 'DEF4G56', 'Toyota Corolla', 2),
(3, 'GHI7J89', 'Chevrolet Onix', 3);

INSERT INTO ordem_servico
(id_ordem, data, descricao, id_veiculo)
VALUES
(1, '2026-09-01', 'Troca de óleo', 1),
(2, '2026-09-02', 'Revisão dos freios', 2),
(3, '2026-09-03', 'Alinhamento', 3);

SELECT
    cliente.nome,
    veiculo.placa,
    veiculo.modelo
FROM cliente
JOIN veiculo
    ON cliente.id_cliente = veiculo.id_cliente;

SELECT
    cliente.nome,
    veiculo.modelo,
    ordem_servico.data,
    ordem_servico.descricao
FROM cliente
JOIN veiculo
    ON cliente.id_cliente = veiculo.id_cliente
JOIN ordem_servico
    ON veiculo.id_veiculo = ordem_servico.id_veiculo;
