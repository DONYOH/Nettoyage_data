import pandas as pd
import os

# === Chemin du fichier source ===
fichier_source = "Lien vers le fichier"

# === Entrées utilisateur ===
colonne_cible = input("Entrez le nom de la colonne à nettoyer (sensible à la casse) : ").strip()
valeur_a_supprimer = input("Entrez la valeur ou le mot-clé à supprimer : ").strip()

# === Chargement du fichier ===
df = pd.read_excel(fichier_source)

# Vérifier si la colonne existe
if colonne_cible not in df.columns:
    print(f"❌ La colonne '{colonne_cible}' n'existe pas dans le fichier.")
    print("Colonnes disponibles :", list(df.columns))
else:
    # Nettoyage : suppression des lignes contenant la valeur
    df = df[~df[colonne_cible].astype(str).str.contains(rf"{valeur_a_supprimer}", na=False)]

    # Répertoire et nom du fichier de sortie
    repertoire_source = os.path.dirname(fichier_source)
    nom_fichier_source = os.path.splitext(os.path.basename(fichier_source))[0]
    fichier_sortie = os.path.join(repertoire_source, f"{nom_fichier_source}_nettoye.xlsx")

    # Sauvegarde du fichier nettoyé
    df.to_excel(fichier_sortie, index=False)

    print(f"✅ Fichier nettoyé enregistré avec succès : {fichier_sortie}")
