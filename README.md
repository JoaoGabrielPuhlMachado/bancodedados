CREATE DATABASE IF NOT EXISTS `2info3_22_mod1`;
USE `2info3_22_mod1`;

CREATE TABLE tipo_usuario (
cod_tipuser int auto_increment PRIMARY KEY,
desc_tipuser varchar(250) not null
);

insert into tipo_usuario values (1,"usuario"),(2,"admin");

CREATE TABLE midia (
titulo_midia varchar(100) not null,
caminho_midia varchar(250) not null,
cod_midia int auto_increment PRIMARY KEY,
cod_postagem int not null
);

insert into midia(titulo_midia,caminho_midia,cod_postagem) values ("foto de gatinhos","servidor/banco/fotodegatinhos.jpg",1),("foto de alimentos","servidor/banco/fotodealimentos.jpg",2),("foto de cachorro","servidor/banco/fotodecachorro.jpg",3),("foto de hospital","servidor/banco/fotodehospital.jpg",4),("foto de mercado","servidor/banco/fotodemercado.jpg",5),("foto de morador de rua","servidor/banco/fotodemoradorderua.jpg",6),("foto de roupas","servidor/banco/fotoderoupas.jpg",7),("foto de cobertor","servidor/banco/fotodecobertor.jpg",8),("foto de peixes","servidor/banco/fotodepeixes.jpg",9),("foto de cama","servidor/banco/fotodecama.jpg",10);

CREATE TABLE ong (
email_ong varchar(250) not null unique,
telefone_ong varchar(14) null,
nome_ong varchar(100) not null unique ,
cod_ong int auto_increment PRIMARY KEY
);

insert into ong(email_ong,telefone_ong,nome_ong) values ("email1@gmail.com","47123456789","resgate animal"),("email2@gmail.com","47123456780","doacao de alimentos"),("email3@gmail.com","47123456781","castracao gratuita"),("email4@gmail.com","47123456782","vaquinha para cirurgia"),("email5@gmail.com","47123456783","compra de alimentos"),("email6@gmail.com","47123456784","ajuda aos moradores de rua"),("email7@gmail.com","47123456785","doacao de roupas"),("email8@gmail.com","47123456786","doacao de cobertores"),("email9@gmail.com","47123456787","ajuda a vida marinha"),("email10@gmail.com","47123456788","dormitorio gratuito");

CREATE TABLE usuario (
idade int not null,
nome varchar(250) not null,
email varchar(250) not null unique,
telefone varchar(14) null,
cod_usuario int auto_increment PRIMARY KEY,
cod_tipuser int not null,
FOREIGN KEY(cod_tipuser) REFERENCES tipo_usuario (cod_tipuser)
);

insert into usuario(idade,nome,email,telefone,cod_tipuser) values (17,"joÃ£o gabriel","joaogabriel@gmail.com","47112233440",2),(16,"ligia gadotti","ligiagadotti@gmail.com","47112233441",2),(18,"alison","alison@gmail.com","47112233442",1),(21,"heric matheus","quinamaldita@gmail.com","47112233443",1),(30,"davy","rascrow@gmail.com","47112233444",1),(19,"marcus","marcus@gmail.com","47112233445",1),(69,"clodoaldo","clodoaldo@gmail.com","47112233446",1),(43,"joana","joana@gmail.com","47112233447",1),(41,"elder","elder.lopes@ifc.edu.br","47112233448",2),(25,"augusto","augustobalsanelli@proton.me","47112233449",1);

CREATE TABLE postagem (
titulo_postagem varchar(100) not null,
categoria varchar(100) not null,
cod_postagem int not null auto_increment PRIMARY KEY,
texto_postagem varchar(1000) not null,
cod_usuario int not null,
cod_ong int not null,
FOREIGN KEY(cod_usuario) REFERENCES usuario (cod_usuario),
FOREIGN KEY(cod_ong) REFERENCES ong (cod_ong)
);

insert into postagem(titulo_postagem,categoria,texto_postagem,cod_usuario,cod_ong) values ("resgate animal","animais","ajude a gente a alimentar animais de rua",2,1),("doaÃ§Ã£o de alimentos","alimentaÃ§Ã£o","ajude-nos financeiramente a conseguir alimentos",1,2),("castraÃ§Ã£o gratuita","animais","castraÃ§Ã£o gratuita em cachorros e gatos",3,3),("vaquinha para cirurgia","pessoas","me ajude a realizar uma cirurgia no apÃªndice",4,4),("compra de alimentos","alimentaÃ§Ã£o","ajude a gente a alimentar necessitados",5,5),("ajuda aos moradores de rua","pessoas","ajude-nos a cuidar dos moradores de rua",6,6),("doaÃ§Ã£o de roupas","roupas","doe suas roupas para pessoas necessitadas",7,7),("doaÃ§Ã£o de cobertores","roupas","pessoas estÃ£o passando frio nas ruas, doe seus cobertores",8,8),("ajuda Ã  vida marinha","animais","ajude os animais marinhos a sobreviver",9,9),("dormitÃ³rios gratuitos","pessoas","compartilhe seu lar para pessoas necessitadas passarem a noite",10,10);

CREATE TABLE comenta (
cod_postagem int not null,
cod_usuario int not null,
dathora_coment timestamp default current_timestamp(),
texto_coment varchar(250) not null,
FOREIGN KEY(cod_postagem) REFERENCES postagem (cod_postagem),
FOREIGN KEY(cod_usuario) REFERENCES usuario (cod_usuario)
);

insert into comenta(cod_postagem,cod_usuario,dathora_coment,texto_coment) values (1,1,'2022-08-24 11:01:21','Adorei a iniciativa'),(2,2,'2022-08-23 21:41:24',"Legal"), (3,3,'2022-08-22 10:00:41',"gostei"),(4,4,'2022-08-21 07:05:31',"nao gostei"),(5,5,'2022-08-20 12:05:00',"desnecessÃ¡rio"),(6,6,'2022-08-19 13:15:17',"ruim"),(7,7,'2022-08-18 08:14:41',"chato"),(8,8,'2022-08-17 05:30:11',"Ã³timo trabalho"),(9,9,'2022-08-16 01:22:29',"projeto legal"),(10,10,'2022-08-15 10:47:57',"gostei, vou doar pra ong");

CREATE TABLE curtir (
cod_postagem int not null,
cod_usuario int not null,
dathora_curtir timestamp default current_timestamp(),
FOREIGN KEY(cod_postagem) REFERENCES postagem (cod_postagem),
FOREIGN KEY(cod_usuario) REFERENCES usuario (cod_usuario)
);

insert into curtir(cod_postagem,cod_usuario,dathora_curtir) values (1,1,'2022-08-24 11:01:21'),(2,2,'2022-04-02 11:01:21'),(3,3,'2022-11-22 22:13:13'),(3,3,'2022-01-04 11:01:21'),(4,4,'2022-07-31 11:01:21'),(5,5,'2022-03-13 11:01:21'),(6,6,'2022-03-20 11:01:21'),(7,7,'2022-11-11 11:01:21'),(8,8,'2022-11-19 11:01:21'),(9,9,'2022-06-15 11:01:21'),(10,10,'2022-12-14 11:01:21');

CREATE TABLE doacao (
cod_ong int not null,
cod_usuario int not null,
dt_doacao date not null,
valor_doacao decimal(10,2) not null,
FOREIGN KEY(cod_ong) REFERENCES ong (cod_ong),
FOREIGN KEY(cod_usuario) REFERENCES usuario (cod_usuario)
);

insert into doacao(cod_ong,cod_usuario,dt_doacao,valor_doacao) values (1,1,'2022-11-11',15.50),(2,2,'2022-12-22',43.75),(3,3,'2022-03-04',135.00),(4,4,'2022-05-31',1547.99),(5,5,'2022-04-15',5.50),(6,6,'2022-09-20',13.13),(7,7,'2022-02-02',22.22),(8,8,'2022-05-11',12.12),(9,9,'2022-01-19',2.35),(10,10,'2022-07-23',5482.35);

CREATE TABLE voluntario (
cod_ong int not null,
cod_usuario int not null,
dt_voluntario date not null,
FOREIGN KEY(cod_ong) REFERENCES ong (cod_ong),
FOREIGN KEY(cod_usuario) REFERENCES usuario (cod_usuario)
);

insert into voluntario(cod_ong,cod_usuario,dt_voluntario) values (1,1,'2022-11-11'),(2,2,'2022-12-22'),(3,3,'2022-03-04'),(4,4,'2022-05-31'),(5,5,'2022-04-15'),(6,6,'2022-09-20'),(7,7,'2022-02-02'),(8,8,'2022-05-11'),(9,9,'2022-01-19'),(10,10,'2022-07-23');

ALTER TABLE midia ADD FOREIGN KEY(cod_postagem) REFERENCES postagem (cod_postagem);
