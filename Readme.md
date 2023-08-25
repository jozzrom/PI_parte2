<p align=center><img src=https://d31uz8lwfmyn8g.cloudfront.net/Assets/logo-henry-white-lg.png><p>

# <h1 align=center> **PROYECTO INDIVIDUAL Nº2** </h1>

# <h1 align=center>**`Cryptocurrency Market Data Analytics`**</h1>


En este repositorio encontrarás el segundo proyecto individual Henry que consiste de 2 partes principales:

1.- La realización de ETL utilizando la API CoinGecko

2.- EDA + KPI

<hr>  

# <h1 align=center> **PLANTEAMIENTO DE PROBLEMA**

## 1.1.- ETL

Realizar extracción de datos desde la API CoinGecko, opcionalmente se puede complementar con la extracción desde otras API siempre y cuando complemente o mejoren el análisis.


## 1.2.- Análisis exploratorio de los datos + KPI: (Exploratory Data Analysis-EDA)

Realizar una análisis exploratorio de los datos una vez limpios, es decir, investigar las relaciones que hay entre las variables de los datasets, ver si hay outliers o anomalías, analizar la existencia de algún patrón interesante que valga la pena explorar en un análisis posterior. 

Se deben sugerir 3 KPIs. Deben estar adecuadamente representados de forma visual. Se debe de tomar en cuenta que tiene que tener una relación con la historia que se está contando. Asimismo, se espera que en la presentación se explique el análisis y la funcionalidad de los KPIs sugeridos.


# <h1 align=center> **DESARROLLO**

# **`1.1.- ETL`**

Se seleccionan 10 de las criptomonedas más reconocidas por su innovación tecnológica. Dicha elección se basó en el raking con mayor market_cap según la página web CoinGecko el día 16-Agosto-2023. Entre los casos de uso de los tokens seleccionados se encuentran: renderización distribuida, computación en la nube, IA, blockchain y crowdsourcing de modelos de predicción de mercado. A continuación una lista de las monedas seleccionadas:


+ 1.	Render (RNDR)
+ 2.	Akash Network USD
+ 3.	SingularityNET (AGIX)
+ 4.	Fetch.ai (FET)
+ 5.	Ocean Protocol (OCEAN)
+ 6.	iExec RLC (RLC)
+ 7.	OriginTrail (TRAC)
+ 8.	inSure DeFi (SURE)
+ 9.	IQ (IQ)
+ 10.	Numeraire (NMR)

En el pdf anexo al github encontrarás más información sobre los casos de uso relacionados con estas criptomonedas. 

# **` 1.1.1.- Extracción de datos Históricos con API CoinGecko `**

Se inicia con la extracción de los datos Históricos con API CoinGecko, el procedimiento se encuentra ubicado en el archivo  *`"1_extraccion_de_datos.ipynb"`* del repositorio. 

Se utiliza la función *`"get_coin_market_chart_range_by_id()"`* para obtener datos históricos de las criptomonedas (precio, volumen, market_cap), esto con la finalidad de entender la evolución de cada moneda en el tiempo. Para la extracción de la data histórica se realizan los siguientes pasos:
+	Se especifica la fecha inicial (01-01-2018) y la fecha final (16-08-2023) de la data que se quiere descargar. 
+	Se especifica el precio en USD
+	Se especifica el id de la moneda. 
+	Una vez utilizada la función, nos devuelve un dataset con datos cuyas columnas venían en forma de lista de la siguiente manera: [fechaunix,dato] por lo que se desanidan dichos datos.

Se obtienen un csv para cada token. Cada csv obtenido lleva el nombre de la moneda y contiene la siguiente información:

+	Fecha: Es la fecha y hora en la que se observó el precio y los otros valores correspondientes a la moneda en el mercado.
+	Price: Este valor representa el precio de la moneda en el momento específico registrado por la marca de tiempo correspondiente en USD.
+	Market caps: Este valor representa la capitalización de mercado de cada moneda en el momento registrado por la marca de tiempo. La capitalización de mercado es el producto del precio actual de la criptomoneda y su suministro circulante. Indica el valor total de todas las unidades de la criptomoneda en circulación.
+	Total_volumes: Este valor representa el volumen total de operaciones de cada moneda en el período especificado por la marca de tiempo. El volumen total se refiere a la cantidad total que se ha comprado o vendido en ese intervalo de tiempo.

A pesar de que se especificó la misma fecha para todas las monedas (01-01-2018- 16-08-2023) , la fecha inicial de las monedas es:
+	Akash: 2020-10-16
+	Singularitynet: 2018-01-22
+	render_token: 2020-06-15
+	origintrail_df: 2018-02-02	
+	ocean_df: 2019-05-04
+	numeraire_df: 2018-01-02
+	insure_df: 2020-01-09
+	iexec_rlc_df: 2018-01-02
+	fetch_ai_df: 2019-03-01
+	everipedia_df: 2018-07-17

*`"Por lo que existen valores np.nan en la información."`*

# **`1.1.2.- Extracción de datos Actuales con API CoinGecko `**

Se inicia con la extracción de los datos Actuales con API CoinGecko, el procedimiento se encuentra ubicado en el archivo  *`"1_extraccion_de_datos.ipynb"`* del repositorio. 

Se utiliza la función *`"get_coins_markets()"`* para obtener datos recientes de las criptomonedas, esto con la finalidad de comprender mejor la situación actual de las diferentes monedas. Para la extracción de la data histórica se realizan los siguientes pasos:
+	Se especifica el precio en USD
+	Se especifica la lista de monedas que contienen los id de cada una. 

Una vez hecha la extracción de datos, se obtiene el csv: *`"coin_markets_df"`* con la siguiente información, la cual se especifica a detalle en el pdf anexo.

+	id
+	symbol
+	name
+	current_price
+	market_cap
+	market_cap_rank
+	fully_diluted_valuation
+	total_volume
+	high_24h
+	low_24h
+	price_change_24h
+	price_change_percentage_24h
+	market_cap_change_24h
+	market_cap_change_percentage_24h
+	circulating_supply
+	total_supply
+	max_supply
+	ath
+	ath_change_percentage
+	ath_date
+	atl
+	atl_change_percentage
+	atl_date
+	roi



# **`1.2.1- EDA: Análisis Histórico de los Datos`**

Se inicia con el análisis histórico de los datos, el cual se encuentra ubicado en el archivo  *`"2_EDA_precio_vol_marketcap_historico.ipynb"`* del repositorio. Los csv utilizados están ubicados en la carpeta  *`"csv_monedas"`*


***Precio***	

Se realiza un análisis de precios históricos en USD, tanto individualmente (para cada moneda) como una comparación entre ellas. Para la realización del EDA se agrupan los datos de manera anual. Una vez hecho esto, se siguen los siguientes pasos:

+ 1.- Se obtiene la gráfica de toda la data histórica para cada una de las monedas. Esto para tener una idea más clara y poder visualizar los cambios en el precio de la criptomoneda a lo largo del tiempo. (Análisis de precios históricos)
+ 2.- Se crea una función que devuelve los outliers en forma de diccionario, del cual la key representa el año y value la cantidad de outliers encontrados en dicho año. Además de eso, devuelve los límites superior e inferior de los bigotes. 
+ 3.- Para cada año (2018,2019,2020,2021,2022,2023) se calcula el precio promedio, la variación, el mínimo y el máximo. Calcular la variación de los datos nos ayuda a identificar los patrones de (volatilidad en el precio)
+ 4.- Se grafican los resultados obtenidos en el punto 3 para cada una de las monedas, para poder observar visualmente la existencia de la relación entre precio, volumen y market cap. A cada pie de gráfico se le agrega una descripción.
+ 5.- Una vez hecho el EDA para cada moneda se procede a realizar la comparación entre ellas, es decir, se busca obtener 4 gráficos que comparen el promedio, la variación, el mínimo y el máximo entre estos 10 tokens. 
+ 6.- Se calcula la matriz de correlación para cada una de las 10 monedas (variables por moneda: precio, market_cap y volumen)


***Marketcap***	

Con el dataframe: *`"df_market"`*, que contiene toda la información con respecto a la capitalización de mercado (de los 10 tokens) se hace un análisis de Tendencias de Capitalización de Mercado. Es decir, se busca un momento en los que ciertos tokens experimentaron un aumento o disminución significativa en su capitalización. Para poder realizar lo anterior, se realiza la comparación entre tokens graficando los promedios por año de market_cap para cada moneda.  


***Volumen de transacción***	

Con el dataframe: *`"df_volumen"`*, que representa la cantidad total de esa criptomoneda que se ha comprado/vendido en un mercado durante un período de tiempo, se hace un análisis de Tendencias de Volumen. Es decir, se busca un momento en los que ciertos tokens experimentaron un aumento o disminución significativa en su compra/venta. Para poder realizar lo anterior, se realiza la comparación entre tokens graficando los promedios por año de market_cap para cada moneda. 

***KPI: Retorno de inversión (ROI)***


Calcular el Retorno de inversión nos permite evaluar la rentabilidad de una inversión en relación con su costo inicial, es decir, nos ayuda a determinar cuánto hemos ganado o perdido en relación con la inversión inicial. Calcular el ROI para las diferentes monedas nos puede ayudar a saber cuál ha tenido un mejor desempeño en términos de rentabilidad. 

Se crea una función para calcular el ROI (Retorno de la Inversión) de todas las monedas con los siguientes pasos:
+ 1.- Se busca el valor inicial , es decir el primer precio registrado hace 5 años.
+ 2.- Se busca el valor final, es decir el último precio registrado de nuestro dataset, en este caso el que pertenece a la fecha 16-08-2023.
+ 3.-Se calcula la gancia como la diferncia entre el valor final y el valor inicial
+ 4.- La ganancia se divide por el valor inicial y se multiplica por cien para calcular el procentaje. 
+ 5.- Se grafican los valores obtenidos. 

***KPI: Crecimiento de Capitalización/Mercado/Market Cap***


Es una métrica utilizada en el análisis de criptomonedas para evaluar cómo ha evolucionado el valor total de mercado de una criptomoneda o del mercado en su conjunto a lo largo del tiempo. Al comparar el crecimiento de la capitalización de una criptomoneda en particular con otras criptomonedas o con el mercado en general, es posible evaluar qué activos digitales están ganando tracción y cuáles están rezagados en términos de adopción y demanda

Muestra tanto los valores absolutos iniciales y finales de la capitalización de mercado como el porcentaje de crecimiento correspondiente para cada token.
+ 1.- Se busca el valor inicial correspondiente a la columna market_cap , es decir el primer volumen histórico registrado.
+ 2.- Se busca el valor final correspondiente a la columna market_cap,  en este caso el que perteneciente a la fecha 16-08-2023.
+ 3.-Se calcula el crecimiento como la difrencia entre los valores obtenidos en los puntos anteriores, divididos por el valor inicial
+ 4.- El crecimiento  se multiplica por cien para calcularse en procentaje. 
+ 5.- Se grafican los valores obtenidos. 


# **`1.2.2- EDA: Análisis Actual de los datos`**

Se inicia con el análisis histórico de los datos, el cual se encuentra ubicado en el archivo  *`"3_EDA_situacion_actual.ipynb"`* del repositorio. Para el análisis de precios actual (USD) se utiliza el dataframe *`"coin_markets_df"`*. Se realizan los siguientes procedimientos:


***Rendimiento de diferentes tokens en términos de precio***

Se compara el precio (USD) de todas las monedas. Lo anterior puede indicar 2 cosas, la primera identificar cuáles de los tokens muestran un mejor rendimiento en comparación con los demás, y la segunda indicar tokens que están recibiendo un mayor interés o demanda en ese día.


 ***KPI: Cambio diario de precio y su porcentaje***  

+ 1.- Se calcula el cambio de precio absoluto, es decir la resta del precio actual y el precio más bajo registrado en 24h.
+ 2.- Se calcula el cambio porcentual, es decir el cambio de precio absoluto dividido por wl precio más bajo registrado en 24 h
+ 3.- Se calcula el porcentaje y se grafica. 



***KPI: Porcentaje de suministro circulante***

Se calcula una nueva columna que indica el porcentaje de suministro circulante con respecto al suministro total, es decir, el porcentaje de monedas que actualmente están en el mercado. 

***KPI: Liquidez o relación Volumen-Capitalización***

+ 1.- Se calcula la capitalización de mercado, es decir el precio total del suministro circulante
+ 2.- Se calcula la relación entre el volumen y la capitalización del mercado. Se guarda en la columna relacion_volumen_capitalizacion['relacion_vol_mc']
+ 3.- Se grafica dicha columna. 




# <h1 align=center> **CONCLUSIONES EDA**

Después de realizar el análisis exploratorio de los datos, se llegan a las siguientes conclusiones:

# **`Análisis Histórico de los Datos`**

***Outliers***

Los outliers encontrados corresponden a los picos en el análisis histórico de precios por lo que se conservan dentro del análisis. 


***Precio***	

* El precio promedio anual más alto lo tiene lo tiene Numeraire.
* El precio promedio anual más bajo lo tiene lo tiene Insure y Everipedia.
* Todas las monedas aumentaron su precio promedio en 2021, sin embargo, después de ese pico casi todas bajaron su precio promedio excepto Render, el cual incluso ha aumentado.
* El precio mínimo más bajo lo tiene Everipedia e Insure
* Todas las monedas aumentaron su precio mínimo en 2021.
* Numeraire es la monena que posee el precio mínimo más alto
La variabilidad en las monedas ha permanecido casi estable para todas a través del tiempo. Sin embargo, todas poseen un pico en el año 2021, lo cual se relaciona con el aumento en el precio de todas las monedas.La moneda con mayor desviación estandar pertenece a Numeraire. Después de ese pico en 2021, la variabilidad ha ido decreciendo lo que significa que el precio se ha ido estabilizando, es decir ha ido disminuyendo la variación de este. 
* El precio máximo más bajo lo tiene Singularitynet e Insure
* Todas las monedas aumentaron su precio máximo en 2021 y posterior a ese pico, el precio máximo de todas las monedas disminuyó.
* Numeraire es la monena que posee el precio máximo más alto

***Marketcap***	

+ El token que tienen una capitalización de mercado consistentemente alta en comparación con otros es Render. En el año 2022 Render supera a los demás tokens en términos de capitalización, significa que el valor total de ese token en circulación es significativamente mayor y más estable en el tiempo en comparación con los valores de capitalización de mercado de los demás. 
+ Todas las monedas (Excepto Render) poseen el pico más alto en el año 2021 y después decaen con respecto al número de unidades en circulación. 

***Volumen de transacción***	

+ En el año 2021, todas las monedas presentan un aumento en el promedio anual de volumen de transacción. Sin embargo, sólo Render siguió creciendo continuamente. Las demás monedas presentan un descenso en dicho volumen para 2022. 

+ La única moneda que presentó un aumento significativo en su volumen de un año a otro (en este caso 2022-20223) es Singularitynet. Superando a todas las demás monedas.Un aumento repentino en el volumen puede ser un indicativo de que algo importante está ocurriendo con respecto a esa criptomoneda. Si nos fijamos en el precio de Singularitynet vemos que de 2022 a 2023 aumentó lo que podría sugerir que los inversores están comprando.

***KPI: Retorno de inversión (ROI)***

El ROi se calcula en el supuesto de haber comprado de cualquiera de las monedas, un único token, al inicio de su ciclo de vida, es decir en el año 2018.
+ Las únicas monedas que presentan un retorno de inversión positivio son: Render, Ocean y Akash 
+ La moneda que posee el retorno de inversión más alto es Render. 
+ La moneda que posee el retorno de inversión más bajo es Insure. 


***KPI: Crecimiento de Capitalización/Mercado/Market Cap***


+ Las monedas que presentan un crecimiento negativo en la capitalización de mercado son: insure y fetch_ai. 
+ La moneda que presenta el mayor crecimiento en la capitalización de mercado es Render con un valor de 96562.644159.


En resumen, todas las monedas experimentaron un aumento en sus precios y volúmenes de transacción en 2021, seguido de una disminución en la variabilidad de los precios y una estabilización de los precios en general. Render se destacó por su consistente alta capitalización de mercado y crecimiento continuo en volumen de transacción. Singularitynet también experimentó un aumento significativo en el volumen de transacción, lo que sugiere un mayor interés de los inversores y la posibilidad de eventos importantes relacionados con la moneda.

# **`Análisis Actual de los Datos`**

***Rendimiento de diferentes tokens en términos de precio***


+ El token que poseen el precio más alto es Numeraire
+ El token que posee el precio más bajo es INSURE

 ***KPI: Cambio diario de precio y su porcentaje***  


+ El token que presenta el porcentaje de cambio de precio más alto en las últimas 24 h, el día 23 de agosto del 2023 es para el token Insure. Un alto cambio diario de precio podría indicar una mayor posibilidad de ganancias, pero también un mayor riesgo de pérdidas.
+ El token que presenta el porcentaje de cambio más bajo en las últimas 24 h, el día 23 de agosto del 2023 es para el token Numerarire


***KPI: Porcentaje de suministro circulante***


+ Las monedas cuyo suministro total está en circulación son: IQ,Akash. Si todos los tokens están en circulación, podría haber una percepción de escasez entre los inversores.

+ Las monedas cuyo porcentaje circulante es menor al total son: inSure DeFi (30.072482) y Ocean Protoco (30.782045)

+ Para el token Akash , se puede apreciar que el suministro circulante es mayor al suministro total pero menor al suministro_max. Esto podría indicar una estrategia de liberación gradual de tokens, un enfoque en la escasez percibida y un equilibrio entre el control del equipo y la influencia del mercado.

***KPI: Liquidez o relación Volumen-Capitalización***


+ Los activos "SingularityNET" y "Fetch.ai" tienen relaciones altas (0.13). Esto sugiere que hay un alto nivel de actividad de compra y venta en el mercado para ese activo, es decir, los inversores pueden comprar o vender grandes cantidades de ese activo sin afectar significativamente su precio.

+ Por otro lado, "inSure DeFi" tiene una relación baja (0.002808), esto podría sugerir que hay menos transacciones ocurriendo en el mercado, lo que podría dificultar la ejecución de operaciones grandes sin afectar el precio. En un mercado con baja liquidez, incluso operaciones relativamente pequeñas pueden tener un impacto más significativo en el precio.

+ El activo "Render" tiene una relación intermedia (alrededor de 0.05), lo que indica una actividad de negociación moderada en relación con su capitalización de mercado.
 

 En resumen, el análisis de diversos tokens en términos de precio y rendimiento, se destaca  Numeraire que tiene el precio más alto y INSURE el más bajo. El cambio diario de precio en 23 de agosto de 2023, INSURE experimentó el mayor cambio en las últimas 24 horas. IQ y Akash tienen todo su suministro en circulación, creando una sensación de escasez, mientras que inSure DeFi y Ocean Protocol tienen menos en circulación. Akash muestra un suministro circulante estratégico. En términos de liquidez, SingularityNET y Fetch.ai tienen actividad alta, inSure DeFi baja, y Render está en el medio.