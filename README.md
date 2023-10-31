# Descrição

Hospital do SUS de grande porte solicita análise de 3 meses da base de COVID do IBGE (https://www.ibge.gov.br/estatisticas/investigacoes-experimentais/estatisticas-experimentais/27946-divulgacao-semanal-pnadcovid1?t=o-que-e&utm_source=covid19&utm_medium=hotsite&utm_campaign=covid_19) para definir as principais ações que deve tomar em caso de novo surto de COVID-19. 

Requisitos da análise: 

* Utilização de 20 questões realizadas na pesquisa;
 
* Caracterização dos sintomas clínicos da população;
 
* Características da população;

* Comportamento da população;

* Características econômicas da sociedade;

* Usar banco de dados em nuvem.

# Ferramentas utilizadas

Escolhemos utilizar as seguintes ferramentas/linguagens para a análise:

* **Databricks / Spark**: ferramenta para processamento e manipulação de Big Data. O dataset completo, com os 3 meses escolhidos, tem mais de um milhão de linhas, por isso a escolha do databricks / spark.

* **SQL**: utilizamos SQL para análise e manipulação dos dados, por ser simples, de fácil entendimento e permite bastante maleabilidade, representando uma vantagem pra analisar um conjunto de dados com mais de 130 variáveis.

* **Big Query**: Banco de dados em nuvem mostrado em aula, com interface mais simples para manuseio e com créditos para uso gratuito da GCS por três meses. 

* **Power BI**: Ferramenta de dataviz que permite compartilhamento de dashboards/relatórios de forma gratuita, além de ser uma das mais utilizadas no mercado brasileiro atualmente. 


# Escolha dos dados

Optamos por utilizar dados dos meses de **Julho, Agosto e Setembro de 2020**, pois são os meses com maior número de casos reportados, dentre as opções de dados da pesquisa (Maio a Novembro/2020). 
Fonte: https://g1.globo.com/bemestar/coronavirus/noticia/2021/03/11/1-ano-de-pandemia-graficos-mostram-o-que-funcionou-no-combate-a-covid-e-quais-os-caminhos-para-o-brasil.ghtml


Como poderíamos usar somente 20 questões das 150 disponíveis na pesquisa, seguimos o raciocínio abaixo na escolha das variáveis mais relevantes:

* Inicialmente descartamos variáveis mais granulares e que tinham alto número de nulos, tais como informações específicas dos rendimentos da população (ex: somatório dos valores recebidos em auxílio emergencial, bolsa família, LOAS, retirava o recebimento em dinheiro, em alimentos, valores de recebimento, etc.). 
 
* Também descartamos variáveis mais subjetivas e que não tinham tanta relação com o os pedidos do hospital (gostaria de ter trabalhado na semana passada, qual o motivo de não ter procurado trabalho, gostaria de ter trabalhado mais horas, etc.).

* Selecionamos as variáveis que consideramos mais relevantes para a pesquisa inicialmente. Utilizamos o databricks/spark e SQL para analisar os dados e afunilar a escolha.

* Após a análise, optamos por fazer um ranking de sintomas e comorbidades mais frequentes para diminuir o número de variáveis clínicas e escolhemos as variáveis que acreditamos melhor representar o perfil socioeconômico da população.

# Caminho dos dados

Baixamos as tabelas mensais do site do IBGE e fizemos a leitura com o databricks. Unimos as tabelas dos 3 meses em um único dataset e salvamos com spark no formato parquet. Fizemos a análise descritiva dos dados com SQL. Fizemos a transferência dos dados para o GCS, salvando o arquivo em um bucket. Leitura do dataset em Big Query. No Big Query criamos uma external table e uma view para permitir o acesso aos dados direto com o Power BI. No PBI, importamos os dados para a criação dos gráficos e da apresentação.

# Entregáveis

Nesse repositório encontram-se os seguintes arquivos: 

* Dicionário dos dados fornecido pelo PNAD;

* Planilhas em csv dos três meses utilizados;
 
* Pasta com dataset final (junção dos 3 meses) em parquet;

* Notebook databricks e jupyter com análise descritiva inicial (somente para registro);

* Notebook databricks e jupyter com a transformação dos dados escolhidos (notebook oficial da entrega do tech challenge);

* Dashboard em PBI com análise final dos dados, **respostas aos pedidos do hospital** e conclusões. 
