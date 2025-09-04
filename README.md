import pandas as pd

df = pd.read_csv("Lien vers le fichier")
df.drop_duplicates(inplace=True)
df.fillna("Non renseigné", inplace=True)
df['date'] = pd.to_datetime(df['date'], errors='coerce')
