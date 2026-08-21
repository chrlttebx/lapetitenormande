LA PETITE NORMANDE — GUIDE DU SITE
====================================

CONTENU DU DOSSIER
-------------------
- index.html        → le site complet (tout est dans ce seul fichier)
- images/logo.png    → votre logo (déjà intégré)
- images/            → dossier où ajouter vos photos


1. AJOUTER VOS PHOTOS
-----------------------
Ouvrez le dossier "images" et ajoutez vos photos avec EXACTEMENT ces noms
(remplacez les fichiers, ou ajoutez-les s'ils n'existent pas encore) :

  hero.jpg        → grande photo de la maison (page d'accueil)
  salon.jpg, cuisine.jpg, chambre1.jpg, chambre2.jpg, sdb.jpg, terrasse.jpg
                  → photos du carrousel "pièces de la maison"
  galerie1.jpg à galerie6.jpg
                  → galerie photo de la section "La maison"
  planches.jpg, port.jpg, casino.jpg
                  → photos de la section "Trouville & Deauville"

Tant qu'une photo n'est pas ajoutée, un joli bandeau rayé avec le nom
de la pièce s'affiche à la place (aucune image cassée à l'écran).

Vous pouvez aussi ajouter davantage de photos au carrousel ou à la
galerie : dans index.html, cherchez les blocs "MODIFIABLE ICI" et
copiez/collez un bloc <figure>...</figure> ou <div class="ph-img">...</div>
supplémentaire, en changeant le nom du fichier et la légende.


2. MODIFIER LES TEXTES
------------------------
Tous les textes affichés sur le site (français ET anglais) se trouvent
regroupés dans index.html, dans la zone :

    const I18N = { fr: {...}, en: {...} }

Chaque ligne a la forme :  "clé": "texte affiché"
Modifiez uniquement la partie entre guillemets après les deux-points,
en gardant bien les guillemets et la virgule à la fin de la ligne.

Exemple :
  "hero.subtitle":"Une maison de charme..."   →   à remplacer par votre texte


3. MODIFIER LE PRIX SELON LES SAISONS ET VOTRE E-MAIL
----------------------------------------------------------
Cherchez, toujours dans index.html, le bloc :

    const CONFIG = {
      ...
      hostEmail: "contact@lapetitenormande.fr",
      ...
      pricePerNight: 150,
      pricingPeriods: [
        { label:"Haute saison (juillet-août)", start:"2026-07-01", end:"2026-08-31", price:220 },
        { label:"Vacances de printemps",       start:"2026-04-04", end:"2026-04-20", price:180 },
        { label:"Fêtes de fin d'année",        start:"2026-12-19", end:"2027-01-04", price:200 }
      ],
      ...

- hostEmail       → votre vraie adresse e-mail (entre guillemets)
- pricePerNight   → le prix "par défaut", utilisé pour toutes les dates qui
                     ne sont dans AUCUNE période ci-dessous (basse saison)
- pricingPeriods  → la liste de vos saisons avec un prix différent. Le
                     calendrier choisit automatiquement le bon prix selon
                     les dates sélectionnées par le client, et fait le
                     total correctement même si le séjour chevauche
                     plusieurs saisons.

Pour CHAQUE période :
  label  → juste pour vous repérer, n'apparaît pas sur le site
  start  → date de début (incluse), format AAAA-MM-JJ
  end    → date de fin (incluse), format AAAA-MM-JJ
  price  → prix par nuit pendant cette période

Vous pouvez ajouter autant de périodes que vous voulez (copiez une ligne
{ ... }, changez les valeurs, et n'oubliez pas la virgule entre chaque
période sauf après la dernière). Vous pouvez aussi en supprimer si vous
préférez un prix unique toute l'année (laissez juste la liste vide : []).

Exemple concret : un client réserve du 30 juillet au 3 août 2026 (4 nuits,
toutes en haute saison à 220€) → le site affichera 880€ automatiquement.
S'il réserve du 29 juin au 2 juillet (à cheval sur deux saisons), le site
calcule le bon prix nuit par nuit et additionne le tout, sans que vous
ayez rien à faire.


4. GÉRER LE CALENDRIER (dates déjà réservées)
------------------------------------------------
C'est VOUS, et vous seul(e), qui mettez à jour les dates réservées.

Toujours dans le bloc CONFIG, la liste :

    blockedDates: [
      "2026-07-14", "2026-07-15", "2026-07-16"
    ]

Quand une réservation est confirmée par vos soins, ajoutez chaque nuit
réservée au format AAAA-MM-JJ, séparée par une virgule. Par exemple,
pour bloquer du 10 au 13 août 2026 :

    blockedDates: [
      "2026-08-10", "2026-08-11", "2026-08-12"
    ]

(Le jour de départ n'a pas besoin d'être bloqué : un client peut arriver
le jour où un autre repart.)

Pensez à enregistrer le fichier après modification.


5. COMMENT FONCTIONNE UNE RÉSERVATION
-----------------------------------------
1. Le client choisit ses dates et son nombre de voyageurs sur le site.
2. Il remplit ses coordonnées et clique sur "Envoyer la demande".
3. Sa messagerie s'ouvre automatiquement avec un e-mail pré-rempli
   adressé à VOTRE adresse (celle définie dans hostEmail), reprenant
   toutes les informations (dates, nuits, prix, voyageurs, contact).
4. Il vous suffit d'envoyer cet e-mail depuis sa boîte mail.
5. Vous recevez la demande, vous répondez pour confirmer, PUIS vous
   ajoutez les dates dans "blockedDates" (étape 4 ci-dessus) pour
   qu'elles n'apparaissent plus disponibles sur le site.

Note : cette méthode (lien "mailto") ne nécessite aucune configuration
ni compte externe. Le seul prérequis est que le visiteur ait une
messagerie configurée sur son ordinateur/téléphone. Si vous souhaitez
un jour un envoi 100% automatique sans ouvrir de messagerie (via un
service comme EmailJS), c'est possible à ajouter plus tard.


6. METTRE LE SITE EN LIGNE
------------------------------
Ce site est un site "statique" : pas besoin de serveur compliqué.
Options simples et gratuites/peu chères :
  - Netlify (glisser-déposer le dossier sur netlify.com/drop)
  - GitHub Pages
  - Votre hébergeur web habituel (via FTP), en uploadant le dossier
    complet (index.html + le dossier images) à la racine.

Vous pouvez aussi simplement ouvrir index.html en double-cliquant
dessus pour prévisualiser le site sur votre ordinateur avant publication.


7. CHANGER LA LANGUE PAR DÉFAUT / EN AJOUTER
------------------------------------------------
Le site propose Français et Anglais. Le bouton "FR / EN" en haut à
droite permet de basculer à tout moment. Si vous souhaitez ajouter une
autre langue plus tard, dites-le moi : la structure du fichier est
prête à en accueillir d'autres.


8. PHOTO OU VIDÉO EN FOND DE LA PAGE D'ACCUEIL
---------------------------------------------------
Dans le bloc CONFIG, la ligne :

    heroType: "photo",

- Laissez "photo" pour utiliser l'image images/hero.jpg (comme avant)
- Mettez "video" pour utiliser une vidéo à la place : ajoutez un fichier
  nommé exactement "hero.mp4" dans le dossier images. La vidéo se lance
  automatiquement, en boucle, sans son (comme sur la plupart des sites
  d'hébergement). Gardez une vidéo assez légère (quelques secondes en
  boucle, pas un film entier) pour que le site reste rapide à charger.


9. PHOTOS QUI S'AGRANDISSENT AU CLIC
-----------------------------------------
Rien à faire ! Toutes les photos du site (carrousel, galerie, région)
s'agrandissent automatiquement quand un visiteur clique dessus. Ça
fonctionne dès qu'une vraie photo a été ajoutée (voir point 1).


10. VOYAGEURS : ADULTES / ENFANTS AVEC ÂGE
-----------------------------------------------
Le sélecteur de voyageurs propose maintenant :
- un compteur "Adultes" (18 ans et plus)
- un compteur "Enfants" (moins de 18 ans) — pour chaque enfant ajouté,
  un menu apparaît pour préciser son âge exact
- le total est limité à 7 personnes (message d'alerte au-delà)

Ces informations sont automatiquement incluses dans l'e-mail de demande
de réservation que vous recevez. Rien à configurer.


11. ONGLET "AVIS" (avec note sur 5)
----------------------------------------
Un nouvel onglet "Avis" a été ajouté en bas du site, avec :
- la note moyenne affichée en haut (calculée automatiquement)
- les avis déjà publiés, sous forme de petites cartes
- un formulaire pour que les visiteurs laissent une note (1 à 5 étoiles)
  et un commentaire

FONCTIONNEMENT : comme pour les réservations, un visiteur qui envoie un
avis fait s'ouvrir sa messagerie avec un e-mail pré-rempli à VOTRE
adresse. C'est vous qui décidez de publier ou non cet avis.

Pour publier un avis validé, ajoutez-le dans le bloc CONFIG, dans la
liste "reviews" :

    reviews: [
      { name:"Claire M.", rating:5, text:"Maison magnifique..." },
      { name:"Nouveau client", rating:4, text:"Le texte de son avis ici" }
    ]

- name   → le nom à afficher
- rating → une note de 1 à 5
- text   → le commentaire (entre guillemets)

Les avis publiés s'affichent désormais dans un carrousel qui défile
horizontalement (comme les photos des pièces), avec des flèches ← → pour
naviguer. Vous pouvez donc en ajouter autant que vous voulez sans jamais
surcharger la page.

N'oubliez pas la virgule entre chaque avis, sauf après le dernier.
La note moyenne en haut de la section se recalcule toute seule.


Besoin d'aide pour une modification plus poussée (nouvelle section,
nouvelle langue, système de paiement en ligne, envoi d'e-mail
automatique, avis publiés automatiquement sans validation...) ?
Revenez vers moi avec ce fichier, je pourrai l'ajuster.
