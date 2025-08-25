# 📊 Análise de Voos -- SQL Project

Este projeto tem como objetivo explorar e analisar o dataset
**`airlines_flights_data`**, que contém informações sobre voos,
companhias aéreas, preços, horários, origem/destino, número de escalas e
classes de viagem.

As consultas foram desenvolvidas em **SQL** e executadas no **SQLite**
para responder perguntas de negócio comuns no setor aéreo.

------------------------------------------------------------------------

## 🗂️ Estrutura do Projeto

-   `airlines_flights_data.csv` → Dataset utilizado para as análises\
-   `Questionario 1.sql` → Script SQL com as consultas

------------------------------------------------------------------------
📈 Distribuição de voos por faixa de horário de saída

Mostra em que horários do dia acontecem mais voos, algo que pode interessar tanto passageiros quanto companhias aérea

<img width="600" height="371" alt="chart" src="https://github.com/user-attachments/assets/9bbfd551-d3a2-40ea-866c-38a81593e06f" />

------------------------------------------------------------------------

## 🛠️ Perguntas Respondidas com SQL

1.  **Preço médio por companhia aérea**

    ``` sql
    SELECT airline, ROUND(AVG(price), 2) AS preco_medio 
    FROM airlines_flights_data 
    GROUP BY airline;
    ```

2.  **Top 5 voos mais caros**

    ``` sql
    SELECT flight, price 
    FROM airlines_flights_data
    ORDER BY price DESC 
    LIMIT 5;
    ```

3.  **Número de voos por faixa de horário de saída**

    ``` sql
    SELECT departure_time, COUNT(*) AS total_voos
    FROM airlines_flights_data
    GROUP BY departure_time
    ORDER BY total_voos DESC;
    ```

4.  **Comparação do preço médio entre voos diretos e com escalas**

    ``` sql
    SELECT stops, ROUND(AVG(price), 2) AS preco_medio 
    FROM airlines_flights_data
    GROUP BY stops
    ORDER BY preco_medio;
    ```

5.  **Voos mais caros por companhia aérea**

    ``` sql
    SELECT airline, MAX(price) AS preco_max 
    FROM airlines_flights_data
    GROUP BY airline
    ORDER BY preco_max DESC;
    ```

6.  **Top 3 destinos mais frequentes a partir de Delhi**

    ``` sql
    SELECT source_city, destination_city, COUNT(destination_city) AS destino 
    FROM airlines_flights_data
    WHERE source_city = 'Delhi'
    GROUP BY destination_city
    ORDER BY destino DESC
    LIMIT 3;
    ```

7.  **Média de preço por classe e companhia aérea**

    ``` sql
    SELECT class, airline, ROUND(AVG(price), 2) AS preco_medio 
    FROM airlines_flights_data
    GROUP BY class, airline;
    ```

8.  **Companhias com preço médio acima da média geral**

    ``` sql
    SELECT airline, ROUND(AVG(price), 2) AS preco_medio
    FROM airlines_flights_data
    GROUP BY airline
    HAVING AVG(price) > (SELECT AVG(price) FROM airlines_flights_data)
    ORDER BY preco_medio DESC;
    ```

------------------------------------------------------------------------

## 🚀 Tecnologias Utilizadas

-   **SQL (SQLite)**
-   **Dataset CSV**
-   **Análise Exploratória de Dados**

------------------------------------------------------------------------

## 📌 Conclusão

Este projeto mostra como **SQL pode ser usado para extrair insights
valiosos de dados de aviação**, respondendo perguntas como:\
- Quais companhias aéreas têm maior custo médio?\
- Qual o horário com mais voos?\
- Para onde Delhi envia mais passageiros?
