# Movie-Recommendation-System

  A premissa do meu trabalho é coletar os dados de avaliações de filmes de um perfil da plataforma Letterboxd que for colocado no programa, 
  ou então coletar avaliações manualmente, caso você não tenha um perfil, e com base nessas avaliações montar a equação Ax = b, 
  sendo a matriz A com linhas sendo filmes e colunas sendo gêneros, o vetor b sendo a avaliação do usuário para cada filme, 
  e x resultará no quanto o usuário gosta de cada gênero relativo a sua avaliações, pesando também a avaliação geral do mesmo, o que será mostrado na tela. 
  Após isso, essa matriz x será usada para recomendar 4 filmes que o usuário ainda não avaliou, e que tenham seu rating geral maior que 4.0, 
  e que ele possivelmente gostará utilizando o método de mínimos quadrados. Utilizarei um dataset contendo filmes e seus respectivos gêneros para isso, 
  além dos dados de avaliações do usuário coletados do Letterboxd, utilizando a técnica de Web Scraping.

  O programa está dividido em células e foi feito no Google Colab.

# Célula 0
Esta célula instala as bibliotecas necessárias para o projeto: requests, beautifulsoup4, pandas, numpy, matplotlib e scipy. Elas são fundamentais para realizar o scraping dos dados da web, manipulação de tabelas, operações numéricas vetoriais, visualização gráfica e resolução de sistemas de equações com restrições. Pesquisei a função de cada uma dessas bibliotecas para tentar aplicá-las corretamente neste projeto.

# Célula 1
Aqui fiz os imports necessários para rodar o sistema. São trazidas funções para:

acessar páginas da internet (requests);
extrair informações do HTML (BeautifulSoup);
trabalhar com dados tabulares (pandas);
realizar operações matriciais e numéricas (numpy);
interpretar strings como listas (ast);
pausar requisições para não sobrecarregar o servidor (time);
exibir gráficos com os resultados (matplotlib);
resolver sistemas lineares com restrições, usando mínimos quadrados (scipy.optimize.lsq_linear).
Cada biblioteca foi selecionada com base em pesquisas.

# Célula 2
Esta função coleta as avaliações de filmes de um usuário do Letterboxd, página por página. Foi necessário pegar a estrutura do HTML do site e utilizar o BeautifulSoup para acessar os dados corretamente. Ela retorna um DataFrame com os títulos dos filmes e suas respectivas notas (de 0.5 a 5). Esse processo envolve conceitos de web scraping, extração de dados estruturados e automação de coleta de dados. Eu peguei mais funções e coisas prontas para essa parte, já que não está relacionada com a matéria em si.

# Célula 3
Esta função permite que o usuário insira manualmente os títulos dos filmes e suas respectivas notas, caso não deseje usar os dados do Letterboxd, ou não tenha. Essa abordagem é importante para garantir que o sistema funcione mesmo sem conexão à internet ou para testes rápidos. A entrada é validada para garantir que as notas estejam no intervalo permitido (0.5 a 5.0). A manipulação do DataFrame ao final é feita com pandas.

# Célula 4
Esta célula é responsável por carregar o banco de dados local com informações sobre filmes e seus respectivos gêneros. São feitas as seguintes etapas:

Leitura do arquivo CSV contendo os filmes, com pandas.read_csv();
Renomeação das colunas para padronização;
Tratamento de valores ausentes em gêneros (substituindo por listas vazias);
Conversão das strings representando listas de gêneros usando ast.literal_eval.
Esse tipo de pré-processamento foi ideal para garantir que os dados estejam em formato adequado para análises posteriores, como operações matriciais e filtragens.

# Célula 5
Esta célula é o núcleo matemático do projeto, onde aplicamos álgebra linear na forma da equação Ax = b:

A é a matriz de gêneros (cada linha representa um filme e cada coluna, um gênero; valores binários indicam se o filme pertence a cada gênero);
b é o vetor de avaliações atribuídas pelo usuário, ponderadas com a média global do filme, para melhorar a robustez do modelo;
As linhas da matriz A são normalizadas para evitar que filmes com muitos gêneros tenham mais peso na equação.
Este processo se alinha muito a mínimos quadrados. Tive que aplicar também, juntamente com os pesos, uma média ponderada da nota do usuário com o rating global para cada filme, sendo de 70% e 30% respectivamente, assim dando um resultado mais preciso.

# Célula 6
Aqui usamos np.linalg.lstsq() para resolver o sistema Ax = b por mínimos quadrados da forma que minimiza o erro quadrático entre as avaliações previstas e as reais. O vetor x resultante representa os pesos do usuário para cada gênero — ou seja, o quanto ele gosta de cada um deles.

# Célula 7
Esta função cria um gráfico de barras que mostra os pesos (preferências) do usuário para cada gênero fornecido. Ela usa matplotlib para plotar os valores, ajustando os rótulos dos gêneros para melhor visualização. O gráfico facilita a visualização das preferências categóricas do usuário.

# Célula 8
Com base no vetor de pesos x, calculamos o quão bem cada filme não assistido combina com os gostos do usuário. O processo envolve:

Filtrar filmes que o usuário ainda não viu e com média global >= 4.0;
Criar uma matriz M semelhante à A, com gêneros dos filmes candidatos;
Normalizar as linhas de M e multiplicar por x para obter uma nota prevista (quanto mais alta, maior a chance do usuário gostar);
Ordenar os resultados e retornar os 4 melhores.
Esse procedimento usa o produto escalar para medir afinidade entre vetores.

# Célula 9
Exibi, em formato de DataFrame, a matriz A com os gêneros de cada filme e a respectiva nota ponderada b. Isso permite:

Verificar quais filmes foram usados para montar a matriz;
Entender como cada filme contribui para a formação do perfil do usuário.

# Célula 10
Este é o ponto de entrada do programa:

Solicita o nome de usuário ou ativa o modo de entrada manual;
Coleta as notas e os filmes assistidos;
Carrega o banco local e monta a matriz A e vetor b;
Resolve o sistema por mínimos quadrados e imprime os pesos dos gêneros;
Exibe os dados usados na criação do perfil e as recomendações finais.
Aqui a integração de todas as partes anteriores ocorre e elas são de fato executadas.

# Considerações finais:
Minha ideia para um sistema de profiling e recomendação de filmes baseado no site Letterboxd foi inspirada no meu projeto da matéria Ágebra Linear Algoritmica, do período 24.2, que era apenas um sistema de recomendações de filmes baseado em avaliações dadas na hora, e apesar de não ter reutilizado nenhum código do mesmo, minha ideia foi inspirada dele.

Ao longo da execução do projeto fui notando que a complexidade do que eu tinha em mente era bem maior do que a esperada, principalmente devido à técnica de Web Scraping e para lidar com os dados na matriz, então tive que improvisar em diversas áreas do código em python, envolveu muita pesquisa, porém no fim consegui fazer com que tudo funcionasse corretamente.

Além disso, também encontrei diversos obstáculos para escolher o dataset, a primor eu havia conseguido uma chave para uma API pública após fazer a solicitação para o site TMDb, porém os gêneros dos filmes desse dataset estavam relativamente errados, ou pelo menos forçados, por exemplo, um dos gêneros de Interestelar era Western, e sci-fi não estava na lista do mesmo, o que acabava gerando resultados muito estranhos nas recomendações, gostar de Interestelar era sinônimo de gostar de Django Livre, que são filmes bem diferentes um do outro.

Depois desse dataset que considerei falho, busquei outro e acabei encontrando um da plataforma Kaggle, e que de fato parecia estar mais correto, apesar de algumas inconsistências, porém tive que mudar completamente o código da célula para utilizar nas matrizes os filmes e gêneros desse novo dataset, o que foi um trabalho bem complexo e inesperado.

# Referências:
Dataset utilizado: https://www.kaggle.com/datasets/ky1338/10000-movies-letterboxd-data

Referência para o Web Scraping: https://github.com/nmcassa/letterboxdpy

Funções desconhecidas por mim foram tiradas somente de pesquisas em diversas outras fontes variadas e vendo suas utilizações práticas, sem muito foco dado a elas.
