# DIGIYLYFE — PARTENAIRE PILOTE 30 JOURS

Page publique d’inscription destinée aux professionnels souhaitant tester DIGIYLYFE pendant 30 jours à partir de l’activation réelle de leur fiche.

## Fichiers

```text
DIGIYLYFE_PARTENAIRE_PILOTE_30_JOURS.html
README.md
```

## Offre pilote

Le programme est ouvert à un maximum de 50 activations pilotes.

Chaque professionnel retenu peut recevoir :

- une fiche professionnelle personnalisée ;
- une carte de visite digitale ;
- un QR personnel ouvrant sa fiche ;
- ses moyens de contact directs ;
- 30 jours d’essai offerts ;
- 0 % de commission DIGIY.

Le mot « fondateur » n’est pas utilisé. La participation ne donne aucune part de propriété, aucun droit social et aucun pouvoir de décision dans DIGIYLYFE.

## Activités proposées

```text
DRIVER
LOC
RESA
MARKET
BUILD
JOBS
EXPLORE
CARNET
AUTRE
```

## Fonctionnement

```text
Visiteur
   ↓
Formulaire public
   ↓
Demande enregistrée
   ↓
Vérification DIGIYLYFE
   ↓
Création manuelle de la fiche
   ↓
Validation du professionnel
   ↓
Activation de la fiche et du QR
   ↓
Début des 30 jours offerts
```

Aucune fiche n’est publiée automatiquement.

## Réception des demandes

La page utilise le projet Supabase DIGIY existant et tente d’ajouter les demandes dans la table :

```text
partners
```

Champs envoyés :

```text
full_name
phone
city
preferred_module
notes
status
```

Valeur initiale du statut :

```text
pre_registered
```

Les informations complémentaires sont regroupées dans `notes` au format JSON.

## Coût technique

La page n’utilise :

- aucune API OpenAI ;
- aucune API WhatsApp ;
- aucune API Meta ;
- aucun service de paiement ;
- aucun abonnement supplémentaire.

Elle utilise seulement Supabase pour recevoir les demandes. Le coût dépend donc uniquement des limites du projet Supabase déjà utilisé par DIGIYLYFE.

## Sécurité et contrôle

La clé présente dans la page est une clé publique `anon`, jamais une clé privée `service_role`.

La table `partners` doit être protégée par des règles RLS adaptées. Le public doit pouvoir uniquement créer une demande conforme. Il ne doit pas pouvoir :

- lire les autres demandes ;
- modifier une demande existante ;
- supprimer une demande ;
- consulter des données internes.

Ne jamais placer une clé `service_role` dans un fichier HTML public.

## Test obligatoire avant publication

Effectuer une demande de test avec de fausses informations professionnelles contrôlées.

Vérifier :

1. que le formulaire confirme l’envoi ;
2. qu’une nouvelle ligne apparaît dans `partners` ;
3. que le statut est `pre_registered` ;
4. que `preferred_module` contient le bon module ;
5. que les détails sont présents dans `notes` ;
6. qu’un visiteur public ne peut pas lire les autres demandes ;
7. que l’affichage fonctionne sur téléphone.

Supprimer ensuite la demande de test.

## Comportement en cas de panne

Lorsque l’envoi échoue, la demande est conservée temporairement dans le `localStorage` du navigateur du visiteur.

Clé utilisée :

```text
digiy_pilot_pending_v1
```

Le visiteur peut ensuite utiliser le bouton de nouvel essai.

Cette sauvegarde locale ne remplace pas la réception Supabase.

## Publication

Le fichier peut être renommé avant publication :

```text
partenaire-pilote.html
```

Exemple de lien depuis la vitrine :

```html
<a href="partenaire-pilote.html">Tester DIGIYLYFE pendant 30 jours</a>
```

Ne pas publier le cockpit interne de prospection sur la vitrine publique.

## Règles commerciales

- Les 30 jours commencent à l’activation réelle de la fiche.
- L’inscription reste une demande soumise à validation.
- Le professionnel fournit ses informations, ses photos et ses contenus.
- Les tournages, montages, impressions et campagnes spéciales sont séparés.
- La présence DIGIYLYFE ne garantit pas un nombre de clients.
- À la fin de l’essai, le professionnel choisit une offre payante ou la mise en pause de sa fiche.

## Doctrine DIGIYLYFE

> Le terrain garde la main.

> Paiement direct au professionnel.

> 0 % de commission DIGIY.

> L’humain valide avant publication.
