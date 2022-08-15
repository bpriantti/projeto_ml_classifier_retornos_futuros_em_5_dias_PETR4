# Projeto ML classifier retornos futuros em 5 dias - PETR4

__Bussines Problem:__  

> Durante a rotina de investimentos torna-se atrativo para a tomada de decisão o melhor timing para a exposição e alocação de recursos em um determinado ativo, no entanto os métodos convencionais possuem uma certa subjetividade para essa determinada análise, sendo necessário o desenvolvimento de métodos quantitativos validados de forma científica e objetiva ao longo de 20 anos de série histórica.

__Objetivo:__   

> Desenvolver um modelo de  machine learning para a previsão de retornos em 5 dias futuros para o ativo PETR4, listado na bolsa de valores brasileira B3.

__Autor:__  
   - Bruno Priantti.
    
__Contato:__  
  - bpriantti@gmail.com

__Encontre-me:__  
   -  https://www.linkedin.com/in/bpriantti/  
   -  https://github.com/bpriantti
   -  https://www.instagram.com/brunopriantti/
   
__Frameworks Utilizados:__

- Numpy: https://numpy.org/doc/  
- Pandas: https://pandas.pydata.org/
- Matplotlib: https://matplotlib.org/ 
- Seaborn: https://seaborn.pydata.org/  
- Plotly: https://plotly.com/  
- Scikit learn: https://scikit-learn.org/stable/index.html
- Statsmodels: https://www.statsmodels.org/stable/index.html

__Project Steps:__

> Realizou-se o processo de ETL com a API de dados, yfinance e com isso obteve-se a série histórica do ativo petr4 desde de 2000 a 2022:

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i1.png?raw=true)

> Em seguida realizou-se o processo de wralling e calculou-se o retorno para 5 dias da série histórica, a partir deste momento definiu-se o leg de 5 dias para o alvo, e utilizou-se como variavel categorica valores acima de 0.02 como 1 e abaixo como 0.

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i2.png?raw=true)

> A partir desse ponto realizou-se o processo de __feature engineering__ e calculou-se as features demostradas abaixo:

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i3.png?raw=true)

> Observe que todas as features necessárias para um modelo de machine learning devem possuir a característica de serem estacionárias, ou seja possuem a característica de retorno a média, para isso implementou-se um script e foram removidas todas as features que não possuem essa característica, estas listadas abaixo:

> check stationarity:   
Open is not stationary. Dropping it.  
High is not stationary. Dropping it.  
Low is not stationary. Dropping it.  
Close is not stationary. Dropping it.  
sma_20 is not stationary. Dropping it.  
 
> sobraram as features:

> ['pct_change_1', 'pct_change_5', 'pct_change_10', 'rsi_14', 'adx_14','corrSma_20', 'volatility_10', 'volatility_20']

> A partir desse ponto optou-se por analisar a correlação entre as features, tendo como resultado o gráfico de heatmap demostrado abaixo:

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i4.png?raw=true)

> Verificou-se a correlação entre as features e foram removidas features com correlação acima de 0.6, foram removidas:

> ['volatility_20','pct_change_10']

> A partir desse ponto realizou-se o processo de data split em train/test, para seguinte research do modelo de machine learning, utilizou-se a proporção de 50%.

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i5.png?raw=true)

__ML research:__

> optou-se por treinar 4 modelos de machine learning, utilizando o framework scikit-learn, estes foram:
  
  - DecisionTreeClassifier
  - GradientBoostingClassifier
  - KNeighborsClassifier
  - SupportVectorMachine
  
> Ao final do treinamento compilou-se os modelos em um ensemble voting classifier, os resultados de matrix de confusão e classification report obtidos foram os seguintes:

__Resultado:__ DecisionTreeClassifier. (Dados de Desconhecidos - 2011/2021)

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i6.PNG?raw=true)  

__Resultado:__ GradientBoostingClassifier. (Dados de Desconhecidos - 2011/2021)

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i7.PNG?raw=true)  

__Resultado:__ KNeighborsClassifier. (Dados de Desconhecidos - 2011/2021)

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i8.PNG?raw=true)  

__Resultado:__ SupportVectorMachine. (Dados de Desconhecidos - 2011/2021)

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i9.PNG?raw=true)  

> Obs: 

> Como observado para dados desconhecidos obtemos um accuracy médio de 52%, sendo o máximo 56% e o mínimo 43%, no entanto devemos considerar para modelos de quant trading,  o quanto o modelo ganha para cada acerto para isso torna-se necessário o procedimento de backtest, que nada mais é do que testar uma estratégia e verificar o retorno/performance da mesma no passado.

__Enssemble Method:__

> Realizou-se o treinamento o treinamento de um modelo de ensemble voting com os modelos que obtiveram uma melhor performance o resultado obtido foi:

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i10.PNG?raw=true)  

__Backtest Modelos:__

Realizou-se o procedimento de backtest do modelo, como demostrado verificamos que o modelo com a melhor performance foi o modelo enssemble votting com um acumulado de (1750%), verifique a imagem:

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i11.png?raw=true)    

> Vale ressaltar que este modelo foi desenvolvido apenas para a compra ou seja ele possui correlação quando o mercado está tendendo para a alta.

__Modelo Versus Benchmark:__

> Vamos agora realizar uma comparação entre o melhor modelo (esmb) versus o ficar comprado no ativo com a estratégia buy and hold, realizaremos uma análise de equity e drawdown ( que nada mais é que os rebaixamentos da curva de equity).

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i12.png?raw=true)    

> Status:

|item   |Modelo   |Buy and Hold   |
|---|---|---|
|Rentabilidade(%)   |845%   |125%   |
|Max Drawdowns      |-66%   |-82%   |

__Retornos Anuais Modelo:__

![alt text](https://github.com/bpriantti/projetoML_classifier_retornos_futuros_em_5_dias_PETR4/blob/main/images/i13.png?raw=true)   
