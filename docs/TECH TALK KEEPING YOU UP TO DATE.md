# Tech talk: Keeping you up to date 👩‍💻👨‍💻

### A RECURRING WORKSHOP

We have seen a lot of workshops covering the usual hot topics - Data Science, Machine Learning, Deep Learning, Full Stack Dev. Albeit these are important courses to have workshops, I feel like there are many new developements out there, that many aren't even aware about.

🤔 When was the last time you heard about a workshop which talks about latest libraries or technologies which you can adopt and change how you work?

I propose to introduce this concept to GDSC. Let's breakdown how I wish this to go about.

### Possible topics :
As the title says, we will introduce new technologies, AI based applications, Python libraries to the participants. Let me give some examples:

- AI tools: ControlNet for AI art generation, GitHub CoPilot, chatpdf, contents AI tool, Bard v/s ChatGPT 
- Python libraries: Polars, Streamsync, Foilum
- Talks: Is AI ethical, Benefits of web scraping

*and so much more!*

### How to decide the topic :
** We could have a schedule. Or even hold a poll on Instagram (or even Threads! *sad twitter noises*), this way our social media handles can get more attention.

### Hosting the workshop: 
The duration of the workshop will be relatively short compared to regular ones - say an hour at most. It will be a presentation and hands-on format. We could rotate the host through the tech team.

### Do I have experience doing this? : 
Glad you asked, I do! I got the opportunity to do a presentation at Emirates in front of the RO heads and staff. I introduced Polars library to my line manager, and he was happy to see a possible replacement of Pandas. Here's the link to my presentation: [Introducing Polars.pdf - Google Drive](https://drive.google.com/file/d/1yR7pIU3On_yzlDBxHv8aWZlyidgyecNq/view?usp=sharing). I even had a live demostration showing the difference in syntax and speed. I even had a opportunity to have a discussion about GitHub. For this, I encouraged my peers to join me and we demostrated the many benefits of collaborating on the platform.

### An example workshop :

comparision in speed and difference in syntax

Using a 5.8 million rows and 31 columns : Flights.csv standard to compare speeds

```python
# %%
#LIBRARY IMPORTS
import polars as pl
import pandas as pd

# %%
#PANDAS
df_pandas = pd.read_csv("flights.csv")

# %%
#POLARS
df_polars = pl.read_csv('flights.csv')

# %% [markdown]
# ### FILTERING DATA

# %%
#PANDAS
df_pandas = pd.read_csv("flights.csv")
df_pandas = df_pandas[(df_pandas['MONTH'] == 12) &
        (df_pandas['ORIGIN_AIRPORT'] == 'SEA') &
        (df_pandas['DESTINATION_AIRPORT'] == 'DFW')]

print(df_pandas)

# %%
#POLARS EAGER EXECUTION
df = pl.read_csv('flights.csv').filter(
     (pl.col('MONTH') == 12) &
     (pl.col('ORIGIN_AIRPORT') == 'SEA') &
     (pl.col('DESTINATION_AIRPORT') == 'DFW'))
display(df)

# %%
# LAZY EXECUTION (SCAN_CSV)
df = pl.scan_csv('flights.csv').filter(
        (pl.col('MONTH') == 12) &
        (pl.col('ORIGIN_AIRPORT') == 'SEA') &
        (pl.col('DESTINATION_AIRPORT') == 'DFW')).collect()
display(df)
# %%
import pandas as pd
import polars as pl

# %%
# Pandas DataFrame
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'Pet':['Cat','Fish','Dog'],
        'Car':['Toyota','Lexus','Nissan']}
df = pd.DataFrame(data)
print(df)

# %%
# Polars DataFrame
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'Pet':['Cat','Fish','Dog'],
        'Car':['Toyota','Lexus','Nissan']}
df_pl = pl.DataFrame(data)
print(df_pl)

# %%
# Pandas
df[['Name', 'Car']]

# %%
# The above code will run with Polars as well,
# but the correct way in Polars is:
df_pl.select(pl.col(['Name', 'Car']))

# %%
# Pandas
df.query('Age > 25')

# %%
# Polars
df_pl.filter(pl.col('Age') > 25)

# %%
# Pandas
df["Age_mul_10"] = df["Age"] * 10

df

# %%
# Polars
df_pl.with_columns([(pl.col("Age") * 10).alias("Age_mul_10")])

# Polars for multiple columns
# df.with_columns([(pl.col("col") * 10).alias("new_col"), ...])

# %%
# Pandas
df.groupby('Name')['Age'].agg('mean')

# %%
# Polars
# df.groupby('col1').agg([pl.col('col2').mean()]) # As suggested in Polars docs
df_pl.groupby('Name').agg([pl.mean('Age')]) # Shorter
```