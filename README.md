# DISCIPLINA DE BANCO DE DADOS 1
# Introdução para mysql
## Comandos
  - mysql -h localhost -u root
  - SHOW SCHEMAS;

## Criar banco de dados
  - CREATE DATABASE comercio;
  - USE comercio;

## Criar tabela
  - CREATE TABLE cidade
    (
    	idcidade 	INT AUTO_INCREMENT PRIMARY KEY,
      nome		VARCHAR(100),
      estado		VARCHAR(002)
    );
    
  - CREATE TABLE cliente
    (
    	idcliente   INT AUTO_INCREMENT PRIMARY KEY,
      nome		VARCHAR(100),
      telefone	VARCHAR(015),
      endereco	VARCHAR(100),
      numero		VARCHAR(020),
      bairro		VARCHAR(050),
      idcidade	int,
      CONSTRAINT FK_cliente_cidade 
      FOREIGN KEY (idcidade) references cidade (idcidade)
    );
    
  - CREATE TABLE fornecedor
    (
    	idfornecedor INT AUTO_INCREMENT PRIMARY KEY,
      nome		 VARCHAR(100),
      telefone	 VARCHAR(015),
      endereco	 VARCHAR(100),
      numero		 VARCHAR(020),
      bairro		 VARCHAR(050),
      idcidade	 int,
      CONSTRAINT FK_fornecedor_cidade 
      FOREIGN KEY (idcidade) references cidade (idcidade)
    );
    
  - CREATE TABLE carro
    (
    	idcarro 	 INT AUTO_INCREMENT PRIMARY KEY,
      marca		 VARCHAR(100),
      modelo		 VARCHAR(100),
      placa		 VARCHAR(010),
      km			 INT
    );
    
  - CREATE TABLE cargo
    (
    	idcargo		 INT AUTO_INCREMENT PRIMARY KEY,
      descricao	 VARCHAR(100),
      salario		 DECIMAL(10,2)
    );
    
  - CREATE TABLE funcionario
    (
    	idfuncionario INT AUTO_INCREMENT PRIMARY KEY,
      nome		  VARCHAR(100),
      telefone	  VARCHAR(015),
      endereco	  VARCHAR(100),
      numero		  VARCHAR(020),
      bairro		  VARCHAR(050),
    	idcidade	 int,
      dataadmissao  DATE,
      datademissao  DATE,
      idcargo		  INT,
      CONSTRAINT FK_funcionario_cidade 
      FOREIGN KEY (idcidade) references cidade (idcidade),
      CONSTRAINT FK_funcionario_cargo
      FOREIGN KEY (idcargo) references cargo (idcargo)
    );
    
  - CREATE TABLE contapagar
    (
    	idcontapagar 	INT AUTO_INCREMENT PRIMARY KEY,
      dataemissao		DATE,
      idfornecedor	INT,
      valor			decimal(10,2),
      datapgto		DATE,
      situacao		VARCHAR(10),
      CONSTRAINT FK_contapagar_fornecedor
      FOREIGN KEY (idfornecedor) references fornecedor (idfornecedor)
    );
    
  - CREATE TABLE contareceber
    (
    	idcontareceber	INT AUTO_INCREMENT PRIMARY KEY,
      dataemissao		DATE,
      idcliente 		INT,
      valor			decimal(10,2),
      datapgto		DATE,
      situacao		VARCHAR(10),
      CONSTRAINT FK_contareceber_cliente
      FOREIGN KEY (idcliente) references cliente (idcliente)
    );
    
  - CREATE TABLE produto
    (
    	idproduto		INT AUTO_INCREMENT PRIMARY KEY,
      descricao		VARCHAR(100),
      precovenda		decimal(10,2),
      estoque			INT
    );
    
  - CREATE TABLE venda
    (
    	idvenda 		INT AUTO_INCREMENT PRIMARY KEY,
      datavenda		DATE,
      idcliente		INT,
      idfuncionario	INT,
    	situacao		VARCHAR(10),
      CONSTRAINT FK_venda_cliente
      FOREIGN KEY (idcliente) references cliente (idcliente),
    	CONSTRAINT FK_venda_funcionario
      FOREIGN KEY (idfuncionario) references funcionario (idfuncionario)
    );
    
  - CREATE TABLE vendaproduto
    (
    	idvendaproduto 	INT AUTO_INCREMENT PRIMARY KEY,
    	idvenda 		INT,
      idproduto		INT,
      quantidade		INT,
      CONSTRAINT FK_vendaproduto_venda
      FOREIGN KEY (idvenda) references venda (idvenda),
    	CONSTRAINT FK_vendaproduto_produto
      FOREIGN KEY (idproduto) references produto (idproduto)    
    );

## Inserir dados na tabela
  - CIDADES
  INSERT INTO cidade (nome, estado) VALUES ('Araçatuba', 'SP');
  INSERT INTO cidade (nome, estado) VALUES ('Birigui', 'SP');
  INSERT INTO cidade (nome, estado) VALUES ('Belo Horizonte', 'MG');
  
  - CLIENTES
  INSERT INTO cliente (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('Eduardo Silva', '(18) 99512-2555', 'Rua Pedro Cavalo','55', 'Centro', 2);
  INSERT INTO cliente (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('Murilo Sauro', '(18) 08100-8588', 'Rua Sem Saída','105', 'Portal', 1);
  INSERT INTO cliente (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('Pedro Bonini', '(18) 08100-8588', 'Rua Valtão','105', 'Portal', 3);
  
  - FORNECEDORES
  INSERT INTO fornecedor (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('Coca Cola do Brasil', '(11) 99852-2555', 'Avenida Paulista','55', 'Centro', 3);
  INSERT INTO fornecedor (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('Heineken Cervejaria', '(21) 08100-8588', 'Rua Sem Saída','4778', 'Moema', 1);
  INSERT INTO fornecedor (nome, telefone, endereco, numero, bairro, idcidade)
  VALUES ('GM do Brasil', '(21) 08100-8588', 'Rua consolação','111', 'Centro', 2);
  
  - CARROS 
  INSERT INTO carro (marca, modelo, placa, km) VALUES ('Fiat', 'Toro', 'ABC1234', 55123);
  INSERT INTO carro (marca, modelo, placa, km) VALUES ('Jeep', 'Renegade', 'CYO8524', 10055);
  INSERT INTO carro (marca, modelo, placa, km) VALUES ('GM', 'Onix', 'ERT8745', 55);
  INSERT INTO carro (marca, modelo, placa, km) VALUES ('FORD', 'Ka', 'TUY8456', 0);
  
  - CARGOS
  INSERT INTO cargo (descricao, salario) VALUES ('Vendedor', 3500);
  INSERT INTO cargo (descricao, salario) VALUES ('Gerente', 15000);
  INSERT INTO cargo (descricao, salario) VALUES ('Mecanico', 4500);
  INSERT INTO cargo (descricao, salario) VALUES ('Serviços Gerais', 1500);
  INSERT INTO cargo (descricao, salario) VALUES ('Contador', 9000);
  
  - FUNCIONARIOS
  INSERT INTO funcionario (nome, telefone, endereco, numero, bairro, idcidade, dataadmissao, datademissao, idcargo)
  VALUES ('Manoel Cardoso', '(11) 98512-2555', 'Avenida Paulista','55', 'Centro', 1, '2024-01-01', null, 3);
  INSERT INTO funcionario (nome, telefone, endereco, numero, bairro, idcidade, dataadmissao, datademissao, idcargo)
  VALUES ('Eduardo Shigueo', '(18) 98512-2555', 'Rua Brasil','1234', 'Centro', 2, '2020-07-10', null, 1);
  INSERT INTO funcionario (nome, telefone, endereco, numero, bairro, idcidade, dataadmissao, datademissao, idcargo)
  VALUES ('Cassio Stersi', '(18) 98512-2555', 'Avenida sumaré','66', 'Centro', 3, '2018-07-10', '2024-07-01', 4);
  INSERT INTO funcionario (nome, telefone, endereco, numero, bairro, idcidade, dataadmissao, datademissao, idcargo)
  VALUES ('Jair Bolsonaro', '(12) 98512-2555', 'Avenida sumaré','66', 'Centro', 3, '2019-01-01', '2023-12-31', 2);
  
  - CONTAS A PAGAR
  INSERT INTO contapagar (dataemissao, idfornecedor, valor, datapgto, situacao)
  VALUES ('2024-01-01', 1, 1500.55, null, 'Aberto');
  INSERT INTO contapagar (dataemissao, idfornecedor, valor, datapgto, situacao)
  VALUES ('2024-01-01', 2, 879.33, '2024-07-13', 'Pago');
  INSERT INTO contapagar (dataemissao, idfornecedor, valor, datapgto, situacao)
  VALUES ('2024-03-12', 3, 965.15, '2024-07-13', 'Pago');
  INSERT INTO contapagar (dataemissao, idfornecedor, valor, datapgto, situacao)
  VALUES ('2024-05-03', 2, 489.55, null, 'Aberto');
  
  - CONTAS A RECEBER
  INSERT INTO contareceber (dataemissao, idcliente, valor, datapgto, situacao)
  VALUES ('2024-01-01', 2, 875.21, null, 'Aberto');
  INSERT INTO contareceber (dataemissao, idcliente, valor, datapgto, situacao)
  VALUES ('2024-01-01', 1, 8578.00, '2024-05-13', 'Pago');
  INSERT INTO contareceber (dataemissao, idcliente, valor, datapgto, situacao)
  VALUES ('2024-03-12', 3, 456.15, '2024-08-18', 'Pago');
  INSERT INTO contareceber (dataemissao, idcliente, valor, datapgto, situacao)
  VALUES ('2024-05-03', 1, 88.89, null, 'Aberto');
  
  - PRODUTOS
  INSERT INTO produto (descricao, precovenda, estoque) VALUES ('Coca cola', 10.55 , 150);
  INSERT INTO produto (descricao, precovenda, estoque) VALUES ('Heineken 600 ml', 18.00 , 450);
  INSERT INTO produto (descricao, precovenda, estoque) VALUES ('Arroz Solito', 10.55 , 780);
  INSERT INTO produto (descricao, precovenda, estoque) VALUES ('Picanha', 55.00 , 8548);
  
  - VENDA 01
  INSERT INTO VENDA (datavenda, idcliente, idfuncionario, situacao) VALUES ('2024-03-21', 1, 1, 'Faturada');
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (1,1,10);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (1,2,5);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (1,2,2);
  
  - VENDA 02
  INSERT INTO VENDA (datavenda, idcliente, idfuncionario, situacao) VALUES ('2024-01-10', 3, 2, 'Faturada');
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (2,3,10);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (2,2,5);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (2,1,55);
  
  - VENDA 03
  INSERT INTO VENDA (datavenda, idcliente, idfuncionario, situacao) VALUES ('2024-07-13', 3, 2, 'Faturada');
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (3,3,10);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (3,2,5);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (3,1,55);
  INSERT INTO vendaproduto (idvenda, idproduto, quantidade) VALUES (3,4,1);

# Beecrowd
## NULL
![Opera Instantâneo_2024-08-17_231243_judge beecrowd com](https://github.com/user-attachments/assets/6962d94a-770d-4421-8131-62d563fff689)
- SELECT customers.id, customers.name
  FROM customers
  LEFT JOIN locations ON customers.id = locations.id_customers
  WHERE locations.id_customers IS NULL;
## Data
![Opera Instantâneo_2024-08-17_232114_resources beecrowd com](https://github.com/user-attachments/assets/613af429-98e1-4c96-a9c5-2bc329a8f218)
- SELECT customers.name, orders.id
  FROM customers
  INNER JOIN orders ON orders.id_customers = customers.id
  WHERE orders.orders_date BETWEEN '2016-01-01' AND '2016-06-30';
## Nome com letra
![Opera Instantâneo_2024-08-17_232354_resources beecrowd com](https://github.com/user-attachments/assets/646f8d5e-7f48-487c-b827-10131e25294b)
- SELECT products.name 
  FROM products
  INNER JOIN providers ON products.id_providers = providers.id
  WHERE products.amount > 10 AND products.amount < 20 
  AND providers.name LIKE 'P%';
## Ordenar e lista de números
![Opera Instantâneo_2024-08-17_232634_resources beecrowd com](https://github.com/user-attachments/assets/625d80df-2d10-4fae-927f-e8103377b975)
- SELECT products.name, categories.name
  FROM products
  INNER JOIN categories ON products.id_categories = categories.id
  WHERE products.amount > 100 AND categories.id IN (1,2,3,6,9) 
  ORDER BY categories.id ASC;
## Mascaca cpf CONCAT
![Opera Instantâneo_2024-08-19_160802_resources beecrowd com](https://github.com/user-attachments/assets/eee132b9-bcd5-46ff-a23c-550dda2f1ec5)
- SELECT CONCAT(
        SUBSTRING(cpf, 1, 3), '.', 
        SUBSTRING(cpf, 4, 3), '.', 
        SUBSTRING(cpf, 7, 3), '-', 
        SUBSTRING(cpf, 10, 2)
    ) AS cpf
  FROM natural_person 
  INNER JOIN customers ON natural_person.id_customers = customers.id;
## Varios WHERE diferentes e apresentar em inteiros
![Opera Instantâneo_2024-08-19_154514_resources beecrowd com](https://github.com/user-attachments/assets/508944af-21fe-4097-9a03-7281b84b288f)
- SELECT 
    name,
    customers_number
  FROM
      (SELECT 
          name, 
          customers_number
       FROM 
          lawyers
       WHERE 
          customers_number = (SELECT MAX(customers_number) FROM lawyers)
       UNION ALL
       SELECT 
          name, 
          customers_number
       FROM 
          lawyers
       WHERE 
          customers_number = (SELECT MIN(customers_number) FROM lawyers)
      ) AS subquery
  UNION ALL
  SELECT 
      'Average' AS name,
      FLOOR(AVG(customers_number)) AS customers_number
  FROM 
      lawyers;
## Média Ponderada 
![Opera Instantâneo_2024-08-19_165902_resources beecrowd com](https://github.com/user-attachments/assets/c6b53764-5e1e-47d1-a070-22cef414d49d)
- SELECT 
    candidate.name, 
    ROUND(
        (
            (score.math * 2) + 
            (score.specific * 3) + 
            (score.project_plan * 5)
        ) / 10, 2
    ) AS avg
    FROM candidate
    INNER JOIN score ON score.candidate_id = candidate.id 
    ORDER BY avg DESC;
## Extrair dia de data 
![Opera Instantâneo_2024-08-19_171006_resources beecrowd com](https://github.com/user-attachments/assets/aa749bcb-2232-45cd-8e0a-7414b5b5ba3d)
- SELECT name, TO_CHAR(payday, 'DD')::integer AS day
  FROM loan;




