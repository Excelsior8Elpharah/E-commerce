# E-commerce
atividade SGBD E-commerce


Cenário: 
Os proprietários de um supermercado precisam 
de um sistema que permita o armazenamento de 
informações sobre produtos, colaboradores e 
clientes. O sistema deve registrar todas as 
vendas realizadas, garantindo uma base de 
dados segura e organizada. Essas informações 
servirão como insumos para campanhas de 
fidelização, permitindo que o supermercado 
conheça as preferências dos clientes e envie 
sugestões personalizadas com base nas compras 
anteriores. 
1. Levantamento de Requisitos 
Abaixo estão 10 perguntas relevantes e suas respostas: 
Perguntas e Respostas 
1. Quais dados sobre os clientes precisam ser armazenados? 
o Nome, CPF, telefone, e-mail, endereço, e data de cadastro. 
2. Quais informações sobre os produtos são importantes? 
o Nome do produto, código de barras, preço de venda, 
quantidade em estoque, e data de validade (se aplicável). 
3. Quais dados dos colaboradores precisam ser guardados? 
o Nome, CPF, cargo, telefone e data de admissão. 
4. Como as vendas serão registradas? 
o Cada venda deve registrar o cliente (se houver), o colaborador 
responsável, os produtos vendidos, quantidade de cada item, 
data e hora da venda e o valor total. 
5. O sistema deve permitir vendas para clientes não cadastrados? 
o Sim, é possível realizar vendas sem cadastro, mas as vendas 
registradas para clientes fidelizados serão priorizadas. 
6. Como o sistema deve tratar o estoque dos produtos? 
o A cada venda, a quantidade vendida de cada produto deve ser 
subtraída do estoque. 
7. Deseja registrar promoções ou descontos aplicados em vendas? 
o Sim, o sistema deve permitir o registro de descontos por 
produto e na venda total. 
8. As vendas podem ser pagas com diferentes formas de 
pagamento? 
o Sim, o sistema deve registrar formas de pagamento, como 
cartão, dinheiro ou Pix. 
9. Será necessário emitir relatórios de vendas e preferências dos 
clientes? 
o Sim, o sistema deve gerar relatórios de vendas diárias e 
relatórios personalizados para clientes cadastrados. 
10. Existem produtos com validade que precisam de controle? 
 Sim, é importante rastrear produtos perecíveis e emitir alertas para itens 
próximos do vencimento. 
2. Modelagem Conceitual, Entidades e Relacionamentos 
Conceituais 
O diagrama conceitual a seguir apresenta as entidades principais e seus 
relacionamentos.
![image](https://github.com/user-attachments/assets/38fa4940-300e-4949-8885-2aba1e1859c2)
 
4. Modelagem Lógica 
Abaixo estão as tabelas normalizadas e seus atributos com os tipos de dados definidos 
para a implementação no banco de dados relacional.
![image](https://github.com/user-attachments/assets/c111908a-463f-49d2-aa02-4f2751fea328)


Tabela: Clientes 
id_cliente (INT) - Chave Primária 
nome (VARCHAR(100)) 
cpf (VARCHAR(11)) - Único 
telefone (VARCHAR(15)) 
email (VARCHAR(100)) 
endereco (VARCHAR(200)) 
data_cadastro (DATE) 

Tabela: Colaboradores 
id_colaborador (INT) - Chave Primária 
nome (VARCHAR(100)) 
cpf (VARCHAR(11)) - Único 
cargo (VARCHAR(50)) 
telefone (VARCHAR(15)) 
data_admissao (DATE) 

Tabela: Produtos 
id_produto (INT) - Chave Primária 
nome_produto (VARCHAR(100)) 
codigo_sku (VARCHAR(13)) - Único 
preco (DECIMAL(10,2)) 
quantidade (INT) 
validade (DATE) 

Tabela: Pedido 
id_pedido (INT) - Chave Primária 
id_cliente (INT) - Chave Estrangeira (Clientes) 
id_colaborador (INT) - Chave Estrangeira (Colaboradores) 
data_hora (DATETIME) 
valor_total (DECIMAL(10,2)) 

Tabela: Itens_Pedido 
id_item (INT) - Chave Primária 
id_pedido (INT) - Chave Estrangeira (Vendas) 
id_produto (INT) - Chave Estrangeira (Produtos) 
quantidade (INT) 
preco_unitario (DECIMAL(10,2)) 

6. Modelo Físico – Código SQL para MySQL 
CREATE DATABASE supermercado;

USE supermercado;

CREATE TABLE clientes ( 
id_cliente INT AUTO_INCREMENT PRIMARY KEY, 
nome VARCHAR(100), 
cpf VARCHAR(11) UNIQUE, 
telefone VARCHAR(15), 
email VARCHAR(100), 
endereco VARCHAR(200), 
data_cadastro DATE 
); 

CREATE TABLE colaboradores ( 
id_colaborador INT AUTO_INCREMENT PRIMARY KEY, 
nome VARCHAR(100), 
cpf VARCHAR(11) UNIQUE, 
cargo VARCHAR(50), 
telefone VARCHAR(15), 
data_admissao DATE 
); 

CREATE TABLE produtos ( 
id_produto INT AUTO_INCREMENT PRIMARY KEY, 
nome_produto VARCHAR(100), 
codigo_sku VARCHAR(13) UNIQUE, 
preco DECIMAL(10,2), 
quantidade INT, 
validade DATE 
); 

CREATE TABLE pedido ( 
id_pedido INT AUTO_INCREMENT PRIMARY KEY, 
id_cliente INT, 
id_colaborador INT, 
data_hora DATETIME, 
valor_total DECIMAL(10,2), 
FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente), 
FOREIGN KEY (id_colaborador) REFERENCES 
colaboradores(id_colaborador) 
);

CREATE TABLE itens_pedido ( 
id_item INT AUTO_INCREMENT PRIMARY KEY, 
id_pedido INT, 
id_produto INT, 
quantidade INT, 
preco_unitario DECIMAL(10,2), 
FOREIGN KEY (id_pedido) REFERENCES vendas(id_pedido), 
FOREIGN KEY (id_produto) REFERENCES produtos(id_produto) 
);
