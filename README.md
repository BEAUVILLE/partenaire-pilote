# DIGIYLYFE — PARTENAIRE PILOTE 30 JOURS

## Correction du 17 juillet 2026

La première version envoyait une colonne `city` directement dans la table Supabase `partners`.

La table existante ne possède pas cette colonne, ce qui produisait :

```text
PGRST204
Could not find the 'city' column of 'partners' in the schema cache
```

La version corrigée ne suppose plus la structure de la table.

Avant chaque premier envoi, elle :

1. lit le schéma PostgREST public du projet Supabase ;
2. détecte les colonnes réellement présentes dans `partners` ;
3. adapte les données du formulaire aux colonnes compatibles ;
4. regroupe toutes les informations dans une colonne de détails disponible ;
5. refuse proprement l’envoi si une colonne obligatoire inconnue manque.

## Fichier à publier

```text
DIGIYLYFE_PARTENAIRE_PILOTE_30_JOURS_CORRIGE.html
```

Il peut être renommé :

```text
index.html
```

## Contrôle après remplacement

1. Vider ou recharger fortement la page publique.
2. Faire une inscription de test.
3. Vérifier l’apparition de la ligne dans `partners`.
4. Vérifier dans la console les messages :
   - `Colonnes Supabase détectées`
   - `Payload adapté au schéma`
5. Supprimer la ligne de test.

## Erreurs possibles après cette correction

### 401 ou 403

La structure est correcte, mais la règle RLS bloque l’insertion publique.

### 400 avec colonne obligatoire

La table impose une colonne obligatoire sans valeur par défaut. Le message affichera son nom exact.

### Table invisible dans le schéma

La table `partners` n’est pas exposée par l’API PostgREST ou n’est pas dans le schéma public.

## Sécurité

La page utilise uniquement la clé publique `anon`.

Ne jamais placer une clé `service_role` dans le HTML public.

Le public doit pouvoir créer une demande, mais ne doit pas pouvoir lire, modifier ou supprimer les demandes des autres professionnels.
