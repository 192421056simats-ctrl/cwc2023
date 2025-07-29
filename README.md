import streamlit as st
import mysql.connector
import pandas as pd

# Connect to MySQL (change to your details)
db = mysql.connector.connect(
    host="localhost",       # 'localhost' or cloud DB host
    user="root",
    password="WJ28@krhps",
    database="cc"
)

st.title("🏏 CWC 2023 – Orange & Purple Cap Leaders")

# Query: Orange Cap
query_orange = """
SELECT 
    player AS Player,
    SUM(runs) AS Runs
FROM innings
WHERE bat_or_bowl = 'bat'
GROUP BY player
ORDER BY Runs DESC
LIMIT 10;
"""
df_orange = pd.read_sql(query_orange, con=db)
st.subheader("🟠 Orange Cap – Top 10 Run Scorers")
st.table(df_orange)

# Query: Purple Cap
query_purple = """
SELECT 
    player AS Player,
    SUM(wkts) AS Wickets
FROM innings
WHERE bat_or_bowl = 'bowl'
GROUP BY player
ORDER BY Wickets DESC
LIMIT 10;
"""
df_purple = pd.read_sql(query_purple, con=db)
st.subheader("🟣 Purple Cap – Top 10 Wicket Takers")
st.table(df_purple)
