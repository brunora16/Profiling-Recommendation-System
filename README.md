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
