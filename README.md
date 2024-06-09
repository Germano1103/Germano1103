CREATE DATABASE PADARIA_EMILLY;

USE PADARIA_EMILLY;

CREATE table USUARIO (
ID bigint primary KEY auto_increment,
NOME varchar(75) NOT NULL,
USUARIO varchar(50) NOT NULL unique,
SENHA varchar(100) NOT NULL,
PERFIL varchar(10) NOT NULL default 'PADRAO',	
ESTADO BOOLEAN NOT NULL DEFAULT TRUE,  
DATA_HORA_CRIACAO datetime DEFAULT current_timestamp,
ULTIMO_LOGIN DATETIME DEFAULT '0001-01-01 00:00:00'
);

CREATE table CATEGORIA(
ID int primary KEY auto_increment,
NOME varchar(50) NOT NULL unique,
DESCRICAO varchar(200)
);

CREATE table PRODUTO(
ID bigint primary KEY auto_increment, 	
NOME varchar(50) NOT NULL unique,
DESCRICAO varchar(200),
PRECO decimal(10,2) NOT NULL,
QUANTIDADE INT NULL,
CATEGORIA_ID INT NOT NULL,
USUARIO_ID bigint NOT NULL,
DATA_HORA_DESCRICAO datetime default current_timestamp,
constraint FK_PRODUTO_CATEGORIA foreign key(CATEGORIA_ID) references CATEGORIA(ID),
constraint FK_PRODUTO_USUARIO foreign key(USUARIO_ID) references USUARIO(ID)
)







create table cliente(
ID INT PRIMARY KEY AUTO_INCREMENT, 
nome VARCHAR(50),
TELEFONE VARCHAR(15),
MORADA VARCHAR(100)
);

create table vendas(
id int primary key auto_increment,
total_venda decimal(10,2) not null, 
valor_pago decimal(10, 2) not null, 
troco decimal(10, 2) not null,
desconto decimal(10, 2) not null, 
cliente_id int, 
USUARIO_ID bigint not null,
data_hora_criacao datetime default current_timestamp,
ultima_atualizacao datetime default current_timestamp,
constraint fk_venda_clientes foreign key (cliente_id) references clientes(id),
constraint fk_venda_usuarios foreign key (usuario_id) references USUARIOS(ID)
);	

create table vendas_item(
venda_id int not null,
produto_id bigint not null,
quantidade int not null,
total decimal(10, 2) not null,
desconto decimal(10, 2) not null, 
constraint fk_venda_item_venda foreign key (venda_id) references vendas(id),
constraint fk_venda_item_produto foreign key (produto_id) references produtos(id)
);
