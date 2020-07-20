<h1>SQL_Anotacoes_Comandos</h1>
<h2>Anotações do Curso de MySQL</h2>

<h3>*CRIANDO O BANCO DE DADOS*</H3>

  - ***CREATE DATABASE*** NAME_EXAMPLE;
  
<h3>*CONECTANDO-SE AO BANCO DE DADOS*</H3>

  - **USE** NAME_EXAMPLE;
  
<h3>*CRIANDO UMA TABELA CLIENTE*</H3>

  - **CREATE TABLE** CLIENTE(
      NOME VARCHAR(30),
      SEXO CHAR(1), (Exemplo de Tunning otimização de perfomance de um DB)
      EMAIL VARCHAR(30),
      CPF INT(11),
      TELEFONE VARCHAR(30),
      ENDERECO VARCHAR(100)
      );
			
<h3>*VERIFICANDO AS TABELAS DE UM BANCO*</H3>

  - **USE** NAME_EXAMPLE;
  - **SHOW** TABLES;
	
<h3>*DESCOBRINDO COMO É A ESTRUTURA (OS CAMPOS) DAS TABELAS*</H3>
	- **DESC* CLIENTE; 
	
<h3>*TUNNING DE TIPO DE DADOS - CHAR VS VARCHAR*</h3>

	- CHAR = UTILIZAR SEMPRE QUE O NÚMERO DE CARACTERES DA COLUNA NUNCA FOR VARIANTE OU SEJA, SEMPRE QUE FOR UMA CONSTANTE
		- EXEMPLO: SEXO / SIGLAS DE ESTADOS
		- É O QUE POSSUI MAIOR PERFOMANCE EM TEMPO DE PROCESSAMENTO
    
	- VARCHAR = É UM TIPO OTIMIZADO QUE SE ADAPTA A QUANTIDADE DE CARACTERES QUE ENTRAR, MESMO QUE SEJA DEFINIDO UM ESPAÇO DE 30
            CARACTERES, ELE UTILIZARÁ APENAS OS ESPAÇAMENTOS QUE FOREM INSERIDOS, OTIMIZANDO A PERFOMANCE DO BD
	
<h3>*TIPOS DE DADOS ENUM VS NUMERICOS*</h3>

	- ENUM = SÓ EXISTE NO MySQL E SERVE PARA EVITAR A INCOMPATIBILIDADE DE INFORMAÇÕES NO BANCO DE DADOS
		- EXEMPLO: NA ENTRADA DE SEXO HÁ OPÇÕES DIVERSAS COMO: "MASCULINO","M","MASC" E ETC PARA EVITAR PODEMOS FAZER UM 				
            TIPO ENUM QUE É UMA ESPÉCIE DE COMBOBOX OU SEJA UM CONJUNTO DELIMITADO DE VALORES
		- EM OUTROS BANCOS SE CHAMA CONSTRAINT DE CHECK
    
	- INT = NÚMEROS INTEIROS SEM VÍRGULA
		- MÁXIMO DE 11 DÍGITOS
    
	- FLOAT = NÚMEROS REAIS COM O USO DA VÍRGULA
		- EXEMPLO: FLOAT(total,virgula) = OU SEJA NÚMERO DE CASAS TOTAIS E DEPOIS QUANTOS NÚMEROS DEPOIS DA VÍRGULA
		- FLOAT(4,2) = 25,00 
		
<h3>*INSERINDO DADOS NA TABELA*</h3>

	- FORMA 1 = OMITINDO AS COLUNAS
		- INSERT INTO CLIENTE VALUES('JOÃO','M','JOAO@GMAIL.COM',988638273,'22923110','MARIA LACERDA - ESTACIO - RIO DE JANEIRO - RJ');
		- INSERT INTO CLIENTE VALUES('JORGE','M',NULL,885755896,'58748895','OSCAR CURY - BOM RETIRO - PATOS DE MINAS - MG);
    
	- FORMA 2 = COLOCANDO AS COLUNAS ( POSSIBILIDADE DE OMITIR COLUNAS - EXEMPLO EMAIL ABAIXO )
		- INSERT INTO CLIENTE(NOME,SEXO,ENDERECO,TELEFONE,CPF) VALUES ('LILIAN', 'F', 'SENADOR-SOARES - TIJUCA - RIO DE JANEIRO - RJ', '947785696', 887774856);
		
	- FORMA 3 = COMPACTO - EXCLUSIVO DO MySQL
    - INSERT INTO CLIENTE VALUES('ANA','F','ANA@GLOBO.COM',85548962,'548654254','PRES ANTONIO CARLOS - CENTRO - SAO PAULO -SP),
          ('CARLA','F','CARLA@TERATI.COM.BR',7745828,'66587458','SAMUEL SILVA - CENTRO - BELO HORIZONTE - MG');
          
   - SEMPRE SE ATENTAR PARA A DOCUMENTAÇÃO DOS TIPOS DE DADOS (EM TERMOS DE RANGE MAXIMO)
   
   - COMANDO BÁSICO DE UM DB = SELEÇÃO, PROJEÇÃO E JUNÇÃO
   
<h3>*COMANDO SELECT*</h3>
   
   	- COMANDO DE PROJEÇÃO, AO CONTRÁRIO DO QUE DIZ O NOME, ELE NÃO SERVE PARA SELECIONAR E SIM PARA PROJETAR PARA O USUÁRIO O QUE ELE DESEJAR.
	- SINTAXE DO COMANDO: SELECT NOME, SEXO, EMAIL FROM CLIENTE;
	- ALIAS SÃO ESPÉCIES DE APELIDOS QUE PODEMOS DAR PARA CAMPOS NA HORA DA PROJEÇÃO
		- EXEMPLO: SELECT NOME AS CLIENTE, EMAIL, SEXO FROM CLIENTE;
	- COMANDO PARA SELECIONAR TODOS OS DADOS DE UMA TABELA = SELECT * FROM CLIENTE;
		- ESSE COMANDO SÓ SERVE PARA FINS ACADÊMICOS, POIS NUM AMBIENTE DE TRABALHO O USUÁRIO ESCOLHE O QUE QUER PROJETAR, SENDO ASSIM SE É UTILIZADO UM SELECT * , TEMOS UM GRANDE AUMENTO NO TRÁFEGO DA REDE DE COMUNICAÇÃO ENTRE O DB E O SISTEMA E PRINCIPALMENTE NO TEMPO DE PROCESSAMENTO E DE RESPOSTA DO DB, POIS O USUÁRIO QUERIA A EXEMPLO 3 CAMPOS O QUE CUSTARIA 100BYTES DE PROCESSAMENTO E DE TRÁFEGO NA REDE, AO USAR O SELECT * NA TABELA CLIENTE TEREMOS 6 CAMPOS O QUE CUSTARIA 300 BYTES, DEIXANDO O SISTEMA MAIS LENTO E AFETANDO O TRÁFEGO DA NOSSA REDE DE COMUNICAÇÃO COM O DB
		
<h3>*COMANDO WHERE</h3>

	- COMANDO DE SELEÇÃO, SERVE PARA SELECIONARMOS UM OU MAIS REGISTRO PASSANDO UMA DECISÃO LÓGICA COMO ARGUMENTO
	- SINTAXE DO COMANDO: SELECT NOME,SEX FROM CLIENTE WHERE SEXO = 'M';
	- A PROJEÇÃO NÃO TEM NADA HAVER COM A SELEÇÃO
		EXEMPLO: SELECT NOME, ENDERECO FROM CLIENTE WHERER SEXO = 'F';
	- COMANDO LIKE, SERVE PARA FAZER PESQUISAS DENTRO DE UMA LINHA DE DADOS(TUPLA)
	- É NECESSÁRIO A UTILIZAÇÃO DE CARACTER CORINGA REPRESENTADO PELO %
		- EXEMPLO: 
			- 1 = BUSCAR DENTRO DA TUPLA NA COLUNA ENDEREÇO TODOS USUÁRIOS QUE MOREM NO ESTADO DO RJ
			- SELECT NOME, SEXO FROM CLIENTE WHERE ENDERECO LIKE '%RJ'; (PORQUE O ESTADO VEM POR ÚLTIMO NA COLUNA ENDEREÇO)
			
			- 2 = BUSCAR DENTRO DA TUPLA NA COLUNA ENDEREÇO TODOS USUÁRIOS QUE MOREM NA RUA OSCAR CURY
			- SELECT NOME, SEXO FROM CLIENTE WHERE ENDERECO LIKE 'OSCAR CURY%'; (PQ A RUA VEM PRIMEIRO)
			
			- 3 = BUSCAR DENTRO DA TUPLA NA COLUNA ENDEREÇO TODOS USUÁRIOS QUE MOREM NO BAIRRO CENTRO
			- SELECT NOME, SEXO FROM CLIENTE WHERE ENDERECO LIKE '%CENTRO%';
			
<h3>*COMANDO COUNT E GROUP/TUNNING*</h3>

	- FUNÇÃO DE AGREGAÇÃO QUE RETORNARÁ UMA SOMA
	- SINTAXE DO COMANDO: SELECT COUNT(*) AS "Quantidade de Registros" FROM CLIENTE;
	- COMANDO DE AGRUPAR UNIDA AO COUNT
	- SINTAZE DO COMANDO: SELECT SEXO, COUNT(*) FROM CLIENTE GROUP BY SEXO;
	- RETORNARÁ UMA TABELA MOSTRANDO A QUANTIDADE (COUNT) AGRUPADA PELO SEXO OU SEJA QUANTOS REGISTROS TEM EM CADA SEXO
	- EXEMPLO: M = 2 / F = 4
	- Exemplo de Tunning para Aumentar Perfomance do Banco:
		- Temos que primeiro conhecer bem os dados do nosso Banco de Dados
		- É recomendado o uso de um COUNT(*) para conhecermos os dados
		- E FILTRAR MATEMATICAMENTE PARA SABER PORCENTAGENS DOS DADOS
		- EXEMPLO: MEU COUNT DE SEXO E CIDADE RETORNOU DE 100 DADOS AGRUPADOS EM 70 F E 30 RJ
		- PARA TRABALHARMOS COM VALORES LÓGICOS OU CLAÚSULA WHERE TEMOS QUE TER EM MENTE O SEGUINTE
		- NO OR SÓ SERÁ FALSO QUANDO AMBOS FOREM FALSO, OU SEJA INDEPENDENTE DE POSIÇÃO, TODOS QUE TIVEREM PELO MENOS UM VERDADEIRO SERÁ VERDADEIRO
		- NO AND SÓ SERÁ VERDADEIRO QUANDO AMBOS FOREM VERDADEIRO, OU SEJA INDEPENDENTE DE POSIÇÃO, TODOS QUE TIVEREM PELO MENOS UM FASO SERÁ FALSO
		- TENDO EM VISTA ESSAS INFORMAÇÕES NUM WHERE ONDE É USADO UM OR
			- RECOMENDA-SE PARA TUNNING INICIARMOS A CLAÚSULA COM O SEXO POIS TEMOS 70% DE CHANCE DE SAIR VERDADEIRO
				- EXEMPLO: SELECT NOME,SEXO, FROM CLIENTE WHERE SEXO = 'F' OR CIDADE = 'RJ';
		- TENDO EM VISTA ESSAS INFORMAÇÕES NUM WHERE ONDE É USADO UM AND
			- RECOMENDA-SE PARA TUNNING INICIARMOS A CLAÚSULA COM A CIDADE POIS TEMOS 30% DE CHANCE DE SAIR VERDADEIRO E SERÁ OBRIGATÓRIO O BANCO EXAMINAR AMBAS A VARIÁVEIS POIS PRECISAMOS QUE AMBSO SEJAM VERDADEIRO PARA DAR VERDADEIRO, ENTÃO ELE IRÁ FAZER A REQUISIÇÃO 30% DAS VEZES, POIS É A QUE VAI DAR VERDADEIRO
				- EXEMPLO: SELECT NOME,SEXO, FROM CLIENTE WHERE CIDADE = 'RJ' AND SEXO = 'F';
				
	**OBS: SEMPRE EVITAR O RETRABALHO DA CHECAGEM LÓGICA DA SEGUNDA CONDIÇÃO**
	
<h3>FILTRANDO VALORES NULOS</h3>

	- DIFERENTE DOS OUTROS TIPOS DE DADOS, O NULL ELE NÃO ARMAZENA NADA PARA SER COMPARADO COM OUTRO (OU SEJA COM SINAL DE "=")
	- PARA RETORNAR OS CLIENTES QUE POSSUEM O EMAIL NULO FAZEMOS O SEGUINTE:
		- SELECT NOME, SEXO, ENDERECO FROM CLIENTE WHERE EMAIL IS NULL;
	- DA MESMA FORMA PARA RETORNAR OS CLIENTES QUE NÃO POSSUEM O EMAIL NULO FAREMOS O SEGUINTE:
		- SELECT NOME, SEXO, ENDERECO FROM CLIENTE WHERE EMAIL IS NOT NULL;

<h3>ATUALIZANDO REGISTROS</h3>

	- PARA ATUALIZAR REGISTRO É SEMPRE IMPORTANTE LEMBRAR DE UTILIZAR 2 COMANDOS PRINCIPAIS, O SELECT (PARA CONFIRMAR SE REALMENTE É AQUELE ROW QUE VOCÊ QUER ATUALIZAR) E O WHERE (PARA QUE NÃO SETEMOS TODOS OS ROWS DO BANCO)
	- SINTAXE DO COMANDO:
		- SELECT * FROM CLIENTE WHERE NOME = 'LILIAN'; (CONFIRMANDO OS DADOS QUE QUEREMOS SETAR)
		- UPDATE CLIENTE SET EMAIL = 'LILIAN@GMAIL.COM' WHERE NOME = 'LILIAN'; (SEMPRE USAR WHERE PARA N SETAR TODO O BD)
   
  <h3>DELETANDO REGISTROS</h3>
  	
	- PARA DELETAR REGISTRO É SEMPRE IMPORTANTE LEMBRAR DE UTILIZAR 2 COMANDOS PRINCIPAIS, O SELECT (PARA CONFIRMAR SE REALMENTE É AQUELE ROW QUE VOCÊ QUER DELETAR) E O WHERE (PARA QUE NÃO DELETEMOS TODOS OS ROWS DO BANCO)
	- É INTERESSANTE TAMBÉM UTILIZAR O COMANDO COUNT COM O WHERE PARA QUE SAIBAMOS EXATAMENTE QUANTOS REGISTROS VAMOS DELETAR DO NOSSO BANCO.
	- EXEMPLO:
		SELECT COUNT(*) FROM CLIENTE WHERE NOME = 'ANA';
	- COM ESSE EXEMPLO ACIMA SABEREMOS COM EXATIDÃO QUANTOS REGISTROS POSSUEM NO NOSSO BANCO COM O FILTRO PASSADO NA CLÁUSULA WHERE
	- DELETE SINTAXE DO COMANDO:
		- DELETE FROM CLIENTE WHERE NOME = 'ANA';
	- DICA: CASO HAJA MUITOS DADOS RETORNADOS PELO COUNT, E QUEREMOS SABER QUANTOS ROWS SOBRARAM APÓS O DELETE, PODEMOS FAZER CONTAS MATEMÁTICAS DENTRO DO TERMINAL DO MySQL, SEM AFETAR EM NADA O NOSSO BANCO
		- EXEMPLO: SELECT 6 - 1;
   
   <h3>MODELAGEM DE BANCODADOS</h3>

	- PRIMEIRA FORMA NORMAL
		- REGRA 1 = TODO CAMPO VETORIZADO SE TORNARÁ UMA OUTRA TABELA
			- EX: CAMPO TELEFONE ( PODEM TER + DE 1 TELEFONE)
		- REGRA 2 = TODO CAMPO MULTIVALORADO SE TORNARÁ UMA NOVA TABELA OU QUANDO O CAMPO FOR DIVISÍVEL
			- EX: CAMPO ENDEREÇO (POSSUI MULTIVALORES DE TIPO DIFERENTE: RUA CIDADE ESTADO ETC)
		- REGRA 3 = TODA TABELA NECESSITA DE PELO MENOS UM CAMPO QUE IDENTIFIQUE TODO O REGISTRO COMO SENDO ÚNICO (PK)
			- NUNCA SE MODELA BASEADO EM NEGÓCIOS OU SEJA UM CPF NÃO PODE SER PK POIS UM DIA PODE ACONTECER DE MUDAR, É ALGO QUE NÃO TEMOS CONTROLE SOBRE, O CPF É UMA CHAVE NATURAL MAS PRECISAMOS DE UMA CHAVE ARTIFICIAL, QUE TENHAMOS TOTAL CONTROLE
			
	- CARDINALIDADE
		A CARDINALIDADE ESTÁ RELACIONADA A RELAÇÃO ENTRE OBRIGATORIEDADE E CARDINALIDADE_MÁXIMA.
		FUNCIONA DA SEGUINTE MANEIRA, PODEREMOS TER EM UM RELACIONAMENTO A SEGUINTE CARDINALIDADE:
			- (0,n) , (0,1), (1,n), (1,1)
			- A PRIMEIRA COLUNA DO PAR, É DEFINIDA PELA OBRIGATORIEDADE OU SEJA, SE FOR OBRIGADO É 1 (TRUE) SE NÃO É 0 (FALSE), COM ISSO TEMOS MONTADO A NOSSA PRIMEIRA COLUNA DO NOSSO PAR
			- A SEGUNDA COLUNA, É DEFINIDA PELA QUANTIDADE_MÁXIMA, OU SEJA, É PERMITIDO ADICIONAR MAIS DE 1 OU APENAS 1? SE FOR PERMITIDO ADICIONAR APENAS 1, O SEGUNDO PAR É 1, SE NÃO, O SEGUNDO PAR É N .
			EX: 
				ENDEREÇO = OBRIGATÓRIO O CADASTRO DE UM ENDEREÇO (NO MÁXIMO 1)
				TELEFONE = O CLIENTE NÃO É OBRIGADO A INFORMAR TELEFONE, MAS PODE INFORMAR MAIS DE UM CASO QUEIRA
			- PARA UMA TABELA CLIENTE, QUE SE RELACIONA COM AMBAS ENTIDADES, TEREMOS A SEGUINTE CARDINALIDADE:
				ENDERECO -> CLIENTE (1,1) / TELEFONE -> CLIENTE (0,n)
			- JÁ PARA FAZERMOS A CARDINALIDADE INVERSA, QUE É PARA SABER QUANTOS ENDEREÇOS OU TELEFONES O CLIENTE PODE TER
				- É OBRIGATÓRIO UM ENDEREÇO TER UM CLIENTE? SIM ENTÃO 1
				- NO MÁXIMO QUANTOS CLIENTES PODEM TER AQUELE ENDEREÇO? NO MÁXIMO 1
				- É OBRIGATÓRIO UM TELEFONE TER UM CLIENTE? SIM ENTÃO 1
				- NO MÁXIMO QUANTOS CLIENTES PODEM TER AQUELE TELEFONE? NO MÁXIMO 1
				CLIENTE -> ENDEREÇO (1,1) / CLIENTE -> TELEFONE (1,1)
			- COM ISSO PODEREMOS DEFINIR O RELACIONAMENTO FINAL:
				- SEMPRE USAREMOS O SEGUNDO PAR PARA ESTABELECER A CARDINALIDADE FINAL, PARTINDO SEMPRE DA ENTIDADE CENTRAL QUE NESSE CASO É CLIENTE
			- CLIENTE -> ENDERECO (1,1)
			- CLIENTE -> TELEFONE (1,n)
			
<h3>FOREIGN KEY - CHAVE ESTRANGEIRA</h3>

		-  É UMA CHAVE PRIMÁRIA DE UMA TABELA, QUE VAI A OUTRA TABELA FAZER REFERÊNCIA DA OUTRA TABELA.
		- DEPENDERÁ DIRETAMENTE DA CARDINALIDADE FINAL, SEGUINDO AS SEGUINTES REGRAS:
			- EM UM RELACIONAMENTO 1X1 A CHAVE ESTRANGEIRA FICA NA TABELA MAIS FRACA
				- A TABELA MAIS FRACA É DEFINIDA PELA REGRA DE NEGÓCIO ( NO CASO DE UM NEGÓCIO DE UM ESTACIONAMENTO, QUAL TABELA SERIA A MAIS IMPORTANTE, A DE UM CARRO OU A DE UM CLIENTE? A MAIS IMPORTANTE SERIA A DE UM CARRO, TORNANDO-A ASSIM A MAIS FORTE, E A DE CLIENTE A MAIS FRACA
			- EM UM RELACIONAMENTO 1 X N  A CHAVE ESTRANGEIRA FICARÁ SEMPRE NA CARDINALIDADE N
		- SINTAXE DENTRO DO CREATE TABLE
		
			CASO SEJA 1 X N
			FK_CLIENTE INT,
			FOREIGN KEY(FK_CLIENTE)
			REFERENCES CLIENTE(ID_CLIENTE)
			
			EX:
				CREATE TABLE TELEFONE (
				ID_TELEFONE INT PRIMARY KEY AUTO_INCREMENT,
				TIPO ENUM('RES', 'CEL', 'COM') NOT NULL,
				NUMERO VARCHAR(20) NOT NULL,
				FK_CLIENTE INT,

				FOREIGN KEY (FK_CLIENTE)
				REFERENCES CLIENTE (ID_CLIENTE)
				);
			
			CASO SEJA 1X1
			FK_CLIENTE INT UNIQUE,
			FOREIGN KEY(FK_CLIENTE)
			REFERENCES CLIENTE(ID_CLIENTE)
			
			EX:
				CREATE TABLE  ENDERECO(
				ID_ENDERECO INT PRIMARY KEY AUTO_INCREMENT,
				RUA VARCHAR(50) NOT NULL,
				BAIRRO VARCHAR(50) NOT NULL,
				CIDADE VARCHAR (30) NOT NULL,
				ESTADO CHAR(2) NOT NULL,
				FK_CLIENTE INT UNIQUE,
		
				FOREIGN KEY (FK_CLIENTE)
				REFERENCES CLIENTE (ID_CLIENTE)
				);
			
- DESC CLIENTE => DESCOBRINDO OS ATRIBUTOS DE UMA TABELA

<h3>SELEÇÃO, PROJEÇÃO E JUNÇÃO</h3>

	- PROJEÇÃO: É TUDO O QUE VOCÊ QUER VER NA TELA (SELECT)
		- SELECT NOW() AS DATA_ATUAL; (PROJETAR A DATA E HORA ATUAL - EXEMPLO DE FUNÇÃO)
		- SELECT 2 + 2 AS SOMA; (PROJETAR UM ALGORITMO DE PROGRAMAÇÃO EM FORMA DE TABELA)
		- SELECT 2 + 2 AS SOMA, NOME, NOW() FROM CLIENTE; 
		
	- SELEÇÃO: É TUDO QUE VOCÊ PRECISA FILTRAR UM SUBCONJUNTO DENTRO DE UM CONJUNTO(WHERE). SEMPRE PRECEDIDO DE UMA PROJEÇÃO ANTES.
		- SELECT NOME, SEXO, EMAIL FROM CLIENTE WHERE SEXO = 'F';
		- SELECT NUMERO FROM TELEFONE WHERE TIPO = 'CEL';
		
	- JUNÇÃO: É JUNTAR UMA TABELA COM OUTRA PARA OPERAÇÕES SEJA DE PROJEÇÃO OU SELEÇÃO
		- INNER JOIN = É VOCÊ JUNTAR O QUE ESTIVER NO MEIO DAS TABELAS ( NO CASO PK COM FK)
			- EXEMPLO 1 TRAZER NOME, SEXO, BAIRRO, CIDADE:
				SELECT NOME, SEXO, BAIRRO, CIDADE /* PROJEÇÃO */
				FROM CLIENTE /* ORIGEM */
					INNER JOIN ENDERECO /* JUNÇÃO */
					ON ID_CLIENTE = FK_CLIENTE /* CONDIÇÃO */
				WHERE SEXO = 'F'; /* SELEÇÃO */
			- EXEMPLO 2 TRAZER NOME, SEXO, EMAIL, TIPO, NUMERO:
				SELECT NOME,SEXO,EMAIL,TIPO,NUMERO
				FROM CLIENTE 
					INNER JOIN TELEFONE
					ON ID_CLIENTE = FK_CLIENTE;
			- EXEMPLO 3 TRAZER NOME, SEXO, BAIRRO, CIDADE, TIPO, NUMERO
			
				JEITO ERRADO ERRADO ERRADO ERRADO ERRADO ERRADO ERRADO:
				SELECT NOME, SEXO, BAIRRO, CIDADE, TIPO, NUMERO
				FROM CLIENTE
					INNER JOIN ENDERECO
					ON ID_CLIENTE = PK_CLIENTE
					INNER JOIN TELEFONE
					ON ID_CLIENTE = PK_CLIENTE;
					
			- AO SE BUSCAR MAIS DE DUAS TABELA USANDO JOIN, É NECESSÁRIO O USO DE PONTEIRAMENTO PARA APONTARMOS PARA QUAL TABELA ESTAMOS NOS REFERINDO, POIS A CHAVE ESTRANGEIRA PODE TER O MESMO NOME EM MAIS DE UMA TABELA, E O BANCO NÃO SABERIA QUAL CHAVE UTILIZAR, NECESSITANDO ASSIM DE UM PONTEIRAMENTO
				- EXEMPLO REFAZENDO O EXEMPLO 3:
					SELECT CLIENTE.NOME, CLIENTE.SEXO, ENDERECO.BAIRRO, ENDERECO.CIDADE, TELEFONE.TIPO, TELEFONE.NUMERO
				FROM CLIENTE
					INNER JOIN ENDERECO
					ON CLIENTE.ID_CLIENTE = ENDERECO.PK_CLIENTE
					INNER JOIN TELEFONE
					ON CLIENTE.ID_CLIENTE = TELEFONE.PK_CLIENTE;
			- AO SE UTILIZAR PONTEIROS TAMBÉM É COMUM UTILZAR ALIAS PARA AS TABELAS, PARA SIMPLIFICAR A ESCRITA (NAS CHAMADAS DAS TABELAS COLOCAMOS O ALIAS DELAS)
				-  EXEMPLO REFAZENDO O EXEMPLO 3:
				SELECT C.NOME, C.SEXO, E.BAIRRO, E.CIDADE, T.TIPO, T.NUMERO
				FROM CLIENTE C
					INNER JOIN ENDERECO E
					ON C.ID_CLIENTE = E.FK_CLIENTE
					INNER JOIN TELEFONE T
					ON C.ID_CLIENTE = T.FK_CLIENTE;

<h3>CATEGORIA DML - COMANDOS</h3>
		
		- DATA MANIPULATION LANGUAGE => TUDO O QUE SE REFERE A MANIPULAÇÃO DE DADOS 
			- INSERT
				INSERT INTO CLIENTE
				VALUES (NULL, 'PAULA', 'M',NULL,'77452145');
			
			- FILTROS
				SELECT * FROM CLIENTE
				WHERE SEXO = 'M';
				
			- UPDATE (LEMBRAR QUE O QUE TORNA UM REGISTRO(ARROW) ÚNICO É A CHAVE PRIMÁRIA EM QUESTÃO OU A ESTRANGEIRA)
				(SEMPRE UTILIZAR UM SELECT ANTES DE QUALQUER OPERAÇÃO NO BANCO, PARA CONFIRMAR SE REALMENTE É A ARROW DESEJADA)
				
				SELECT * FROM CLIENTE
				WHERE IDCLIENTE = 7;
				
				UPDATE CLIENTE
				SET SEXO = 'F'
				WHERE IDCLIENTE = 7;
				
			- DELETE
				(SEMPRE UTILIZAR UM SELECT ANTES DE QUALQUER OPERAÇÃO NO BANCO, PARA CONFIRMAR SE REALMENTE É A ARROW DESEJADA)
			
				SELECT * FROM CLIENTE
				WHERE IDCLIENTE = 8;
			
				DELETE FROM CLIENTE
				WHERE IDCLIENTE = 8;

<h3>COMANDOS DDL</h3>

	- DATA DEFINITION LANGUAGE => TUDO O QUE FAZEMOS EM RELAÇÃO A UMA TABELA QUE TEM HAVER COM O TIPO.
	- EXEMPLO 1: 
		- CREATE TABLE PRODUTO (
			IDPRODUTO INT PRIMARY KEY AUTO_INCREMENT,
			NOME_PRODUTO VARCHAR(30) NOT NULL,
			PRECO INT,
			FRETE FLOAT(10,2) NOT NULL
		);
		
	- EXEMPLO 2, ALTERANDO O NOME DE UMA COLUNA COM CHANGE:
		- ALTER TABLE PRODUTO
		  CHANGE PRECO VALOR_UNITARIO INT NO NULL;
		 
	- EXEMPLO 3, ALTERANDO O TIPO DE UM DADO PRA ACEITAR VALOR NULO
		- ALTER TABLE PRODUTO
		  CHANGE VALOR_UNITARIO(SEMPRE MOSTRAR ORIGEM) VALOR_UNITARIO INT;
		  
	- EXEMPLO 4, ALTERANDO TIPO DE UM DADO SEM PRECISAR REPETIR O NOME 2 VEZES COMO O CHANGE ACIMA:
		- ALTER TABLE PRODUTO
		  MODIFY VALOR_UNITARIO VARCHAR(50) NOT NULL;
		  
	- EXEMPLO 5, ADICIONANDO COLUNAS
		- ALTER TABLE PRODUTO
		  ADD PESO FLOAT(10,2) NOT NULL;
		  
	- EXEMPLO 6, ADICIONANDO COLUNAS EM UMA ORDEM ESPECÍFICA (APESAR DE NÃO SER MT NECESSÁRIO, POIS ISSO É FACILMENTE MANIPULADO NA PROJEÇÃO)
		- ALTER TABLE PRODUTO
		  ADD PESO FLOAT(10,2) NOT NULL
		  AFTER NOME_PRODUTO;
		  
		  OU ADICIONANDO NA PRIMEIRA POSIÇÃO
		  
		- ALTER TABLE PRODUTO
		  ADD PESO FLOAT(10,2) NOT NULL
		  FIRST;
		  
<h3>ALTERANDO DADOS ERRADOS</h3>

	- SELECT * FROM CLIENTE
	WHERE ID_CLIENTE IN (12,13,18);

	UPDATE CLIENTE SET SEXO = 'F'
	WHERE ID_CLIENTE IN (12,13,18);
	
<h3>FUNÇÃO IFNULL</h3>

	- FUNÇÃO É UM BLOCO DE PROGRAMAÇÃO QUE EXECUTA ALGUMA COISA
	- RECEBE 2 PARÂMETROS, O PRIMEIRO É O FIELD (COLUNA) E O SEGUNDO UMA STRING PRA APRESENTAR NA SAÍDA
	- LEMBRAR DE UTILIZAR UM ALIAS NA COLUNA EM QUESTÃO, PARA NÃO APARECER A FUNÇÃO NA SAÍDA DA TABELA
	-EXEMPLO:
		SELECT  C.NOME, 
			IFNULL(C.EMAIL, '**********') AS 'EMAIL', 
			E.ESTADO, 
			T.NUMERO
		FROM CLIENTE C
		INNER JOIN ESTADO E
		ON C.ID_CLIENTE = E.FK_CLIENTE
		INNER JOIN TELEFONE T
		ON C.ID_CLIENTE = T.FK_CLIENTE;
		
<h3> VIEW </h3>

	- AS VIEWS FUNCIONAM COMO PONTEIROS DE FUNÇÕES, POR TRÁS DE UMA VIEW TERÁ UM COMANDO PRA SER EXECUTADO. POR EXEMPLO UM COMANDO INNER JOIN, ONDE SEMPRE EXECUTAMOS ELE, PODEREMOS CRIAR UMA VIEW E ASSIM EXECUTAR A VIEW E ELA APONTAR DIRETAMENTE PARA O COMANDO EM QUESTÃO.
	- EXEMPLO 1: COMANDO REPETITIVO EXEMPLO
	
		SELECT 	C.NOME, 
			C.SEXO, 
			C.EMAIL, 
			T.TIPO, 
			T.NUMERO,
			E.BAIRRO,
			E.CIDADE, 
			E.ESTADO
		FROM CLIENTE C
		INNER JOIN TELEFONE T 
		ON C.ID_CLIENTE = T.FK_CLIENTE 
		INNER JOIN ENDERECO E
		ON C.ID_CLIENTE = E.FK_CLIENTE;
		
	- CRIANDO A VIEW PRA RESUMIR ESSE COMANDO: (OBS: PADRONIZAR OS NOMES DAS VIEWS, PQ ELAS SE MISTURAM AS TABELAS NO SHOW TABLES)
	
		CREATE VIEW V_RELATORIO AS
		SELECT 	C.NOME, 
			C.SEXO, 
			IFNULL(C.EMAIL,'********') AS 'EMAIL', 
			T.TIPO, 
			T.NUMERO,
			E.BAIRRO,
			E.CIDADE, 
			E.ESTADO
		FROM CLIENTE C
		INNER JOIN TELEFONE T 
		ON C.ID_CLIENTE = T.FK_CLIENTE 
		INNER JOIN ENDERECO E
		ON C.ID_CLIENTE = E.FK_CLIENTE;
		
	- APAGANDO UMA VIEW = DROP VIEW NOME_VIEW;
	
<h3>DML COM VIEWS </h3>

	- EM VIEWS COM JOIN SÓ É PERMITIDO REALIZAR A OPERAÇÃO DE UPDATE, REALIZANDO ASSIM A ALTERAÇÃO NA TABELA E NÃO SÓ NA VIEW.
	- NÃO É PERMITIDO DELETAR OU INSERIR VALORES EM VIEWS COM JOIN 
	- JÁ EM VIEWS SEM JOIN É PERMITIDO TODAS AS OPERAÇÕES DE DML (INSERIR, DELETAR E UPDATE)
		
<h3>ORDENAÇÃO DE DADOS (ORDER BY)</h3>

	- ORDERNANDO POR 1 COLUNA
		- SELECT * FROM CLIENTE
		  ORDER BY NOME;
		  
	- ORDERNANDO POR MAIS DE 1 COLUNA
		- SELECT * FROM CLIENTE
		  ORDER BY NUMERO,NOME;
		  
	- MESCLANDO ORDER BY COM PROJEÇÃO
		- SELECT NOME FROM ALUNOS
		  ORDER BY NUMERO, NOME;
		  
	- ASC X DESC
		- ASC = ASCENDENTE
		- DESC = DESCENDENTE
		
		SELECT * FROM ALUNOS
		ORDER BY NOME DESC;
		
		SELECT NOME FROM ALUNOS
		ORDER BY NUMERO DESC, NOME ASC;
		
	- COM INNER JOIN E VIEWS, SEMPRE COLOCAR NO FINAL DA QUERRY
		- SELECT * FROM V_RELATORIO
		  ORDER BY 1; (NO CASO VAI ORDERNAR PELO NOME)
		  
		- SELECT 	
			C.NOME, 
			C.SEXO, 
			IFNULL(C.EMAIL,'********') AS 'EMAIL', 
			T.TIPO, 
			T.NUMERO,
			E.BAIRRO,
			E.CIDADE, 
			E.ESTADO
		FROM CLIENTE C
		INNER JOIN TELEFONE T 
		ON C.ID_CLIENTE = T.FK_CLIENTE 
		INNER JOIN ENDERECO E
		ON C.ID_CLIENTE = E.FK_CLIENTE
		GROUP BY 1;
		
<h3> Mudando o Delimitador do Banco </h3>

	- Comando: DELIMITER $
	
<h3> STORED PROCEDURES </h3>
	
	SÃO BLOCOS DE PROCEDIMENTOS PROGRAMADOS NO BANCO
	
	- CREATE PROCEDURE <NOME>()
	  BEGIN
	  	<BLOCO DE PROGRAMAÇÃO>;
	  END
	  $ (DELIMITADOR)
	  
	  EX:
	  	CREATE PROCEDURE NOME_EMPRESA()
		BEGIN
			SELECT 'UNIVERSIDADE DOS DADOS' AS EMPRESA;
		END
		$
	
	- CHAMANDO UMA PROCEDURE
		CALL NOME_EMPRESA()$
		
	- APAGANDO PROCEDURE
		DROP PROCEDURE NOME_EMPRESA();
		
	- PASSANDO PARÂMETROS
		DELIMITER $
		
		CREATE PROCEDURE CONTA(NUMERO1 INT, NUMERO2 INT)
		BEGIN
			SELECT NUMERO1 + NUMERO2 AS CONTA;
		END
		$
		
	 
	 
<h3> PADRÃO MVC BEM EXPLICADO </h3>

	- SEÇÃO 13 AULA 63.59 (PROCEDURES NO MUNDO REAL)
	
<h3> PROCEDURES COM QUERRYS </h3>

	- EXEMPLO DE UM BANCO FICTÍCIO COM SUAS PROCEDURES
	
		/* ---------------------------- */

		CREATE DATABASE PROJETO;

		USE PROJETO;

		CREATE TABLE CURSOS(
			ID_CURSOS INT PRIMARY KEY AUTO_INCREMENT,
			NOME VARCHAR(30) NOT NULL,
			HORAS INT(3) NOT NULL,
			VALOR FLOAT (10,2) NOT NULL
		);

		DELIMITER $

		CREATE PROCEDURE CAD_CURSOS(P_NOME VARCHAR(30),
					    P_HORAS INT(3),
					    P_VALOR FLOAT(10,2))
		BEGIN

			INSERT INTO CURSOS VALUES(
			NULL, P_NOME,P_HORAS,P_VALOR);

		END 
		$

		CALL CAD_CURSOS('BI SQL SERVER', 35, 3000.00);
		CALL CAD_CURSOS('POWER BI', 20, 1000.00);
		CALL CAD_CURSOS('TABLEAU', 30, 1200.00);
		CALL CAD_CURSOS('JAVA SEM MISTERIO', 20, 20.00);
		CALL CAD_CURSOS('BOOTCAMP IGTI', 120, 100.00);
		CALL CAD_CURSOS('JDEV JAVA WEB', 1200, 200.00);
	
		/* CRIAR PROCEDURE PARA CONSULTAR DADOS*/

		CREATE PROCEDURE CONS_CURSOS_CAROS()
		BEGIN

			SELECT * FROM CURSOS
			ORDER BY VALOR DESC;
	
		END 
		$

		DELIMITER $

		CREATE PROCEDURE CONS_CURSOS_LONGOS()
		BEGIN
	
			SELECT * FROM CURSOS
			ORDER BY HORAS DESC;

		END
		$

		CREATE PROCEDURE CONS_CURSOS_BARATOS()
		BEGIN

			SELECT * FROM CURSOS
			ORDER BY VALOR;

		END
		$

		CREATE PROCEDURE CONS_CURSOS()
		BEGIN

			SELECT * FROM CURSOS;

		END
		$
		
		
<h3> FUNÇÕES DE AGREGAÇÃO </h3>

	- MAX ( RETORNARÁ O MAIOR VALOR DE UMA COLUNA)
		- SELECT MAX(VALOR) AS CURSO_CARO
		  FROM CURSOS;
		  
	- MIN ( RETORNARÁ O MENOR VALOR DE UMA COLUNA)
		- SELECT MIN(VALOR) AS CURSO_BARATO
		  FROM CURSOS;
		  
	- AVG (RETORNARÁ O VALOR MEDIO DE UMA COLUNA)
		- SELECT AVG(VALOR) AS MEDIA_CURSOS
		  FROM CURSOS;
		  
	- TRUNCATE (FORMATARÁ O DOUBLE COM A QUANTIDADE DE CASAS DECIMAIS PASSADA NO PARÂMETRO/ TRUNCATE(<PARAMETRO1>,<PARAMETRO2>) )
		- SELECT MAX(JANEIRO) AS MAX_JAN,
		  MIN(JANEIRO) AS MIN_JAN,
		  TRUNCATE(AVG(JANEIRO),2) AS MEDIA_JAN
		  FROM VENDEDORES;

	- SUM (RETORNARÁ A SOMA DE TODA A COLUNA)
		- SELECT SUM(JANEIRO) AS TOTAL_JAN,
			 SUM(FEVEREIRO) AS TOTAL_FEV,
			 SUM(MARCO) AS TOTAL_MAR
		 FROM VENDEDORES;
		 
	- SUM COM FILTROS
		- SELECT SEXO, SUM(MARCO) AS TOTAL_MARCO
		  FROM VENDEDORES
		  GROUP BY SEXO;
		 
<h3> SUBQUERRYS </h3>

	- NO CASO DE TENTARMOS RETORNAR O NOME E O MENOR VALOR DO BANCO DE DADOS, TEMOS QUE USAR UM SUBQUERRY, PARA QUE O SQL NOS RETORNE OS VALORES ESPERADOS
	- EXEMPLO:
		SELECT NOME, MARCO FROM VENDEDORES
		WHERE MARCO = (SELECT MIN(MARCO) FROM VENDEDORES);
		
	- PRA SABER QUEM VENDEU ACIMA DA MÉDIA
		SELECT NOME, MARCO FROM VENDEDORES
		WHERE MARCO > (SELECT AVG(MARCO) FROM VENDEDORES);
		
	- PRA SABER QUEM VENDEU ABAIXO DA MÉDIA
		SELECT NOME, MARCO FROM VENDEDORES
		WHERE MARCO < (SELECT AVG(MARCO) FROM VENDEDORES);
		
<h3> OPERAÇÕES COM AS LINHAS DA TABELA </h3>

	- SELECT NOME,
		 JANEIRO
		 FEVEREIRO,
		 MARCO,
		 (JANEIRO + FEVEREIRO + MARCO) AS "TOTAL",
		 TRUNCATE ((JANEIRO + FEVEREIRO + MARCO)/3 , 2) AS "MEDIA"
		 FROM VENDEDORES;
		
	- APLICANDO DESCONTO
		- SELECT NOME,
			 JANEIRO
			 FEVEREIRO,
			 MARCO,
			 (JANEIRO + FEVEREIRO + MARCO) * .25 AS "DESCONTO",
			 TRUNCATE ((JANEIRO + FEVEREIRO + MARCO)/3 , 2) AS "MEDIA"
		 FROM VENDEDORES;
		 
<h3>****** DICIONÁRIO DE DADOS ******</h3>

	- <h4> ADICIONANDO UMA PK</h4>
		ALTER TABLE TABELA
		ADD PRIMARY KEY (COLUNA1)
		
		(NÃO PODE SER AUTO INCREMENTÁVEL)
		
	- <h4> ADICIONANDO COLUNA SEM POSIÇÃO </h4>
		ALTER TABLE TABELA
		ADD COLUNA VARCHAR(30);
		
		(VAI PARA A ULTIMA POSIÇÃO DA TABELA)
		
	- <h4> ADICIONANDO UMA COLUNA COM POSIÇÃO </h4>
		ALTER TABLE TABELA
		ADD COLUMN COLUNA4 VARCHAR(30) NOT NULL UNIQUE
		AFTER COLUNA3;

		(VAI PARA A COLUNA APÓS A COLUNA3, VISTO DE CIMA PARA BAIXO)
		
	- <h4> MODIFICANDO O TIPO DE UM CAMPO</h4>
		ALTER TABLE TABELA MODIFY COLUNA2 DATE NOT NULL;
		
		(A TROCA DE TIPOS TEM QUE SER COMPATÍVEL COM O DADO, POR EXEMPLO NÃO PODEMOS PEGAR UM 'LUIZ' E PASSA-LO PARA INT)
		
	- <h4> RENOMEANDO O NOME DA TABELA </h4>
		ALTER TABLE TABELA
		RENAME PESSOA;
		
<h3> CONSTRAINTS NOMEADAS - BOAS PRÁTICAS </h3>

	- /* retornando aos estudos 20/07 */

		SHOW DATABASES;
		USE COMERCIO

		DROP TABLE ENDERECO;
		DROP TABLE TELEFONE;
		DROP TABLE CLIENTE;

		CREATE TABLE CLIENTE(
			ID_CLIENTE INT,
			NOME VARCHAR(30) NOT NULL
		);

		CREATE TABLE TELEFONE(
			ID_TELEFONE INT,
			TIPO CHAR(3) NOT NULL,
			NUMERO VARCHAR(10) NOT NULL,
			FK_IDCLIENTE INT

		);

		ALTER TABLE CLIENTE ADD CONSTRAINT PK_CLIENTE
		PRIMARY KEY(ID_CLIENTE);

		ALTER TABLE TELEFONE ADD CONSTRAINT FK_CLIENTE_TELEFONE
		FOREIGN KEY(FK_IDCLIENTE) REFERENCES CLIENTE(ID_CLIENTE);
		
		SHOW CREATE TABLE TELEFONE; /* COMANDO PARA VER AS CONSTRAINTS DA TABELA */
		
<h3> DICIONÁRIO DE DADOS </h3>
	
	- COMANDO STATUS = SERVE PARA VERMOS EM QUAL BD ESTAMOS CONECTADOS
	- SHOW DATABASES
		- INFORMATION_SCHEMA
		- MYSQL
		- PERFOMANCE_SCHEMA
	- USE INFORMATION_SCHEMA;
	- SHOW TABLES;

	- DESC TABLE_CONSTRAINTS;

	- SELECT CONSTRAINT_SCHEMA AS "BANCO",
	   	TABLE_NAME AS "TABELA",
	  	CONSTRAINT_NAME AS "NOME TABELA",
	   	CONSTRAINT_TYPE AS "TIPO"
	   	FROM TABLE_CONSTRAINTS
	  	WHERE CONSTRAINT_SCHEMA = "COMERCIO";
		
	/* APAGANDO AS CONSTRAINTS */
	
	- USE COMERCIO;
	
	- ALTER TABLE TELEFONE
	  DROP FOREIGN KEY FK_CLIENTE_TELEFONE;
	
