# Previsão de Preço de Imóveis
!['capa'](/docs/capa.jpeg)

# 1. Descrição

- Este projeto tem como objetivo principal criar um algorítmo de aprendizado de máquina capaz de prever o valor de um novo imóvel dado as suas características.
- Aqui nosso foco não é ter uma análise exploratória detalhada e vários insights sobre os dados, nosso foco principal é o treinamento e melhoria dos modelos de regressão.

# 2. Tecnologias e ferramentas
- As tecnlogias utilizadas foram Python (Pandas, Numpy, Matplotlib, Seaborn, Scikit-Learn), Visual StudioCode e GitHub (desenvolvimento do projeto e versionamento), algoritmos de aprendizado de máquina, estatística.
  
# 3. Problema de Negócio
**Qual o problema de negócio?**

- Fui contratado por uma imobiliária para gerir, analisar e insights sobre os dados da empresa. Foi-me atribuido a tarefa de entender a correlação do preço do imóvel com cada uma das features que a emprese obtinha no seu site, e em seguida prever o valor de um imóvel. Para esta tarefa irei criar um modelo de **Regressão** para nos dar este valor.


**Qual o contexto?**
- Para a imobiliária é importante ter precisão ao precificar um imóvel, desta forma os lucros seriam maximizados e os prejuísos minimizados.


**Qual o objetivo do projeto?**
- Criar um modelo que preveja o preço do imóvel com uma precisão alta.
- Após a escolha do melhor modelo, utilizar os dados de um novo imóvel solicitado pelo cliente e presumir o seu valor.


**Quais os benefícios do projeto?**
- Saber o preço estimado de um imóvel pode ajudar a fazer um investimento mais conmsciente, a negociar de forma mais justa e evitar surpresas com custo.

# 4. Dentro do projeto
**4.1 EDA**

Nosso primeiro desafio começou com a estrutura dos dados. Como capturamos os dados da API da empresa, os dados vieram formatados como JSON:

!['1'](/docs/1.png)

E precisamos posteriormente o ajustar para o formato de DataFrame, pois é de mais fácil compreensão e é o ideal para projetos de aprendizado de máquina:

!['2'](/docs/2.png)

Em seguida averiguamos os dados faltantes, dados duplicados e outliers, após a identificação dos mesmos os tratamos.

**4.2 Visualizando Correlações**

Depois de tratar os dados e criar novas features, olhamos como estava a correlação entre cada uma das features, isso pode fornecer alguns tipos de informações úteis, e no nosso caso identificamos um grau muito forte de colinearidade entre duas features (suites e banheiros):

!['3'](/docs/3.png)

O que significa essa colinearidade? Significa que essas duas colunas (quarto e banheiro) esão muito correlacionadas entre si, e isso pode causar problemas em modelos de regressão pois torna difícil a distinção individual de cada feature. Após aplicarmos a função logarítmica nos dados, esta correlação irá ser reduzida, e é o que faremos ná próxima etapa.



**4.3 Distribuição dos Dados**

!['4'](/docs/4.png)

Como podemos notar através desse gráfico de histograma, conseguimos notar uma calda longa a direita, os dados não estão distribuídos de forma simétrica (distribuição normal), e isso pode atrapalhar o desempenho do modelo previsor.

E para resolver este problema precisamos realizar uma transofrmação logarítmica das variáveis para que as distribuções se aproximem de uma normal, para que podemos utilizar o modelo de regressão linear.

!['5'](/docs/5.png)

Distribuição dos dados após aplicarmos o o logarítmo nos dados:

!['6'](/docs/6.png)

Percebemos que agora os dados se aproximam de uma normal (forma de sino)



# 5. Modelagem

Os algorítmos de aprendizado de máquina que escolhemos para testar seus desempenhos foram:
- Regressão Logística
- Árvore de Decisão
- Floresta Aleatória

**5.1 Regressão Logística**

O modelo de regressão logística é bastante simples, ele não exige muitos hiperparâmetros, e no nosso caso seus resultados foram:
- R² (Coeficiente de Determinação) = 73%
- MSE (Erro Quadrático Médio ) = 22%

*Quanto mais próximo de 100% for o R², melhor. E quanto mais próximo de 0 for o MSE, melhor*

Logo, este modelo apresenta sim um bom desempenho, as os que testamos a seguir atingem uma performance melhor.

**5.2 Árvore de Decisão**

O primeiro modelo de árvore de decisão que treinamos, não passamos nenhum hiperparâmetro e obtivemos este resultado:

!['7'](/docs/7.png)

*A Linha cinza representa a regressão perfeita, e a preta como nosso modelo se comportou. Quanto mais parecida com a linha cinza, melgor o R² e connsequentemente melhor o desempenho do modelo*

Obtivemos R² = 76% (já melhor que a refressão linear)

Em seguida criamos outro modelo de Árvore, agora com hiperparâmetros testados com Validação Cruzada e Random SearchCV, e os resultados foram:

R² = 80% (ou seja, ganhamos 4% de desempenho com estes ajustes)

**5.3 Floresta Aleatória**

Em seguidas testamos uma algorítmo cru com florestas aleatórias (que é um algorítmo que calcula a média de multiplas árvores de decisão, assim evitando sobreajuste e uma precisão maior nos resultados).

Nossos primeiros resultados foram:

!['8'](/docs/8.png)

R² = 77%

Logo em seguida fizemos o mesmo que na árvore de decisão, e testamos os hiperparâmetros até chegar neste resultado:

R² = 83%

# 6 Conclusão

E assim esolhemos o nosso melhor modelo, sendo ele o de Floresta Aleatória, que apresentou a melhor métrica de validação.

 Após essa escolha, pegamos um dado fictíceo de um cliente que nos informou características do seu imóvel, e nos pediu que calculássemos o valor do mesmo, e estes foram o resultados:

!['9'](/docs/9.png)

O valor do imóvel do cliente foi de : R$ 378.550,60.