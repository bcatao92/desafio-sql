
# Desafio Python:

## Utilização: 

O programa foi criado utilizando a IDE Vscode, mas deve ser compatível com qualquer ambiente. Ao iniciá-lo, o programa exibe um menu instando o usuário a escolher as funções que deseja executar. São aceitas letras maiúsculas ou minúsculas. O arquivo csv utilizado é o mesmo fornecido.

## Parte 1:

Enunciado: Construa uma tabela auxiliar que sumarize o valor vendido por cada vendedor, ordenando do maior para o menor.

Resposta:
	Observação: para o funcionamento desta função, é necessário importar as bibliotecas csv, pandas e decimal. O csvfile utilizado se encontrava no mesmo diretório que o programa, e se chamava ‘BD_Teste.csv’, e se encontra anexo a este respositório.
	Primeiramente, foi necessário alterar o .csv fornecido, trocando seu delimitador “,” para “;”, pois em seu estado bruto, os valores em reais eram separados dos centavos, o que criaria resultados diferentes dos buscados.
	Com os ajustes feitos, parti para a criação da função vendedoresTotal(csvfile):

![Imagem 1](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem1.jpg)

A função cria um reader para o arquivo csv e um dicionário, pula a linha do cabeçalho e itera pelo arquivo salvando vendedores como chaves e calculando o total de suas vendas. Para somar os valores, foi necessário criar uma função que transformasse os valores de string para decimal, conforme vemos a seguir:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem2.jpg)

Com o dicionário garantindo que os vendedores tinham suas respectivas somas, faltava ordená-los de acordo como os valores, o que não é possível num dicionário. Para isso criei o sort_dicio, uma lista de tuplas ordenada do maior valor para o menor, e uma lista vazia chamada valores, que receberia os valores tratados novamente como string, para que eu pudesse formatar-los novamente como dinheiro:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem3.jpg)

Por fim, para gerar a tabela, foi necessário criar um DataFrame que recebesse os valores e os títulos da tabela, segundo a fórmula a seguir:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem4.jpg)

## Parte 2:
Enunciado: Imprima e identifica qual foi o cliente responsável pela venda com maior valor e com menor valor;

	Resposta:
	
  A função maiorMenor(csvfile) foi utilizada para responder a esta demanda.
  
  ![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem5.jpg)
  
Como as outras, ela cria um leitor de csv e pula a primeira linha do arquivo fornecido. Ela então itera pelo arquivo (deletando a última coluna, criada por um erro de leitura no csv original) e adiciona os clientes e suas respectivas compras numa lista que é organizada do maior para o menor.
	A função então imprime uma mensagem dizendo qual cliente fez a maior compra singular e seu valor, e qual fez a menor compra e seu valor.

## Parte 3:
	Enunciado: Imprima valor médio por Tipo de venda (Serviços, Licenciamento, Produtos)

Resposta:

Para esta demanda, achei importante importar a biblioteca collections.
  
  ![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem6.jpg)

A função mediasTipos(csvfile) cria o dicionário tipos, um collections.Counter chamado contaTipo e uma lista chamada medias. A função então itera pelo arquivo csv contando as ocorrências de cada tipo e armazenando em contaTipo, além de guardar os tipos de serviços e somar suas respectivas arrecadações no dicionário tipos.
	A seguir, contaTipo e tipos são organizados alfabeticamente, de modo que as posições dos tipos sejam correspondentes nas duas listas.
	Por fim, utilizei um for loop para calcular as médias, dividindo os valores totais pelas ocorrências dos tipos e armazenando-as justo aos seus respectivos tipos na lista medias criada anteriormente. Esta lista então é usada para criar o DataFrame que é impresso como resultado da função.

## Parte 4:
Enunciado: Imprima o número de vendas realizada por cliente;
Resposta:
	A biblioteca collections foi usada novamente nesta função.
	Para contar quantas vezes um cliente específico fez compras com a empresa, foi criado um Counter, que foi alimentado na iteração do csv_reader, retornando uma lista com cada cliente e sua frequência. A lista, contaCliente.most_common(), foi utilizada como fonte para o DataFrame, que tinha como colunas “Cliente” e “Vendas”.
![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem7.jpg)


# Desafio SQL

O database manager utilizado foi o PostgreSQL, por questão de familiaridade. Os csv's gerados se encontram no respositório.

## Parte 1: 
Enunciado: Construa o modelo de relacionamento com as categorias utilizadas em todos os campos do arquivo CSV (colocar imagem);

Criando o modelo de relacionamento com o arquivo CSV fornecido. Note que para que a coluna “Valor” não seja separada em duas, foi necessário trocar os delimitadores de “,” para “;” no arquivo original.
A seguir, imagem com a Query utilizada e relação criada:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem8.jpg)

## Parte 2:
Enunciado: Listar todas as vendas (ID) e seus respectivos clientes apenas no ano de 2020


Query:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem9.jpg)

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem10.jpg)

## Parte 3:
Enunciado: Listar a equipe de cada vendedor

Query:
![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem11.jpg)
![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem12.jpg)

## Parte 4:
- Construir uma tabela que avalia trimestralmente o resultado de vendas e plote um gráfico deste histórico.

Tabela:

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem13.jpg)

Para plotar o gráfico, foi necessário converter os valores da receita para Numeric, de outra forma o PostgresSQL não leria a coluna “Receita” como número.

![alt text](https://raw.githubusercontent.com/bcatao92/desafio-sql/main/imagem14.jpg)
