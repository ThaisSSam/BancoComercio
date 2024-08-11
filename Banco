DROP DATABASE IF EXISTS comercio;

CREATE DATABASE IF NOT EXISTS comercio;

USE comercio;

CREATE TABLE cidade
(
	idcidade 	INT AUTO_INCREMENT PRIMARY KEY,
    nome		VARCHAR(100),
    estado		VARCHAR(002)
);

CREATE TABLE cliente
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

CREATE TABLE fornecedor
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

CREATE TABLE carro
(
	idcarro 	 INT AUTO_INCREMENT PRIMARY KEY,
    marca		 VARCHAR(100),
    modelo		 VARCHAR(100),
    placa		 VARCHAR(010),
    km			 INT
);

CREATE TABLE cargo
(
	idcargo		 INT AUTO_INCREMENT PRIMARY KEY,
    descricao	 VARCHAR(100),
    salario		 DECIMAL(10,2)
);

CREATE TABLE funcionario
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

CREATE TABLE contapagar
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

CREATE TABLE contareceber
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

CREATE TABLE produto
(
	idproduto		INT AUTO_INCREMENT PRIMARY KEY,
    descricao		VARCHAR(100),
    precovenda		decimal(10,2),
    estoque			INT
);

CREATE TABLE venda
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

CREATE TABLE vendaproduto
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


/*
tabelas:
cidade: idcidade, nome, estado
cliente: idcliente, nome, telefone, endereco, numero, bairro, idcidade,
fornecedor: idfornecedor, nome, telefone, endereco, numero, bairro, idcidade,
carro: idcarro, marca, modelo, placa, km
cargo: idcargo, descricao, salario
funcionario: idfuncionario, nome, idcargo, dataadmissao, endereco, numero, bairro, idcidade
contapagar: idpagar, dataemissao, idfornecedor valor, data_pgto, situacao
contareceber: idreceber, dataemissao, idcliente, valor, data_pgto, situacao
produto: idproduto, nome, precovenda, estoque
venda: idvenda, data_venda, idcliente
vendaproduto: idvendaproduto, idvenda, idproduto, quantidade
*/
