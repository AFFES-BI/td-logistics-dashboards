# Réflexions — TD5 Dashboards : trois rôles, trois KPI, un réseau logistique

## Avant de commencer

**Réflexion 1 (prédiction, écrite avant de construire quoi que ce soit).** Je prédis
que c'est le **responsable des opérations / coûts** qui sera le plus en désaccord avec
les deux autres. Le responsable RSE (distances longues = CO2) et le planificateur
réseau (distance moyenne à la population) ont tous deux intérêt à ce que le réseau
change, par exemple en ouvrant un entrepôt qui rapproche les villes du sud. Le
responsable coûts, lui, voit surtout qu'un entrepôt de plus ajoute du stockage et des
coûts fixes, et sera tenté de ne rien changer. *(Je reviendrai dessus après l'étape 10.)*

## Stage 1 — Données et hypothèses

**Réflexion 2.** L'hypothèse que je défendrais le moins bien est la **population
comme proxy de la demande** (50 t/an pour 1 000 habitants). Le facteur CO2 a une
fourchette officielle citée (≈0,047 à 0,12 kg CO2e/t·km) et 0,10 s'y situe : on peut
le sourcer. Les coûts (0,12 EUR/t·km et 40 EUR/t/an) sont explicitement non sourcés,
mais ils ne changent que des euros. Le proxy de demande, lui, multiplie **tous** les
chiffres des trois dashboards, et il est inventé : population municipale (Paris
intra-muros, pas l'agglomération) sans aucun lien prouvé avec des tonnages réels.
Face à un client, c'est celui qui s'effondre le plus vite.

## Stage 2 — Trois KPI à partir d'un seul script

**Réflexion 3.** Prenons les KPI **CO2/coût** d'un côté et **distance réseau** de
l'autre, pour **Lille**. Dans la vue CO2 et la vue coût, Lille affiche 0 kg de CO2 et
0 EUR de transport : c'est l'entrepôt « parfait », ou « inutile » selon le point de vue,
et seul son stockage (466 196 EUR/an) reste à son compte. Ces deux KPI poussent donc
vers « on peut la fermer, on ne perd presque rien ». La vue réseau dit l'inverse :
fermer Lille fait passer la distance moyenne pondérée de 168,04 km à 174,43 km, car ses
233 098 habitants devraient alors être servis depuis Paris. Même entrepôt, deux
décisions opposées : un entrepôt peut être invisible dans une vue « routes servies »
tout en réduisant la distance totale, parce qu'il sert son propre marché local.

## Stage 4 — Visualisation pour la décision

**Réflexion 4.** Je ne recommanderais pas la route n°1 telle quelle. Dans mon top 10,
**Marseille ← Lyon** arrive en tête avec 1 211 830 kg de CO2/an (277,6 km). Deux choses
me font hésiter. D'abord, ce n'est pas la plus longue route : Bordeaux ← Lyon fait
435,8 km mais seulement 570 471 kg. Marseille est première surtout parce que sa
« demande » est énorme (873 076 habitants x 50 t/1 000 hab.), donc elle dépend
entièrement du proxy de population, qui n'est pas une vraie donnée de tonnage. Ensuite,
Marseille est aussi un site candidat à un entrepôt : consolider cette route n'aurait pas
le même sens si on ouvre un entrepôt sur place, ce qui la ferait presque disparaître.
Je vérifierais d'abord les vrais volumes et la distance routière (les distances sont à
vol d'oiseau, la route réelle est plus longue) avant d'en parler au responsable RSE.

**Réflexion 5.** L'entrepôt le plus cher est **Lyon** : 13 476 013 EUR/an, dont 5 687 061
EUR de transport et 7 788 952 EUR de stockage. Je tirerais d'abord le levier
**transport**. Le chiffre qui me convainc est le coût par tonne : 69,21 EUR à Lyon contre
50,91 EUR à Paris et 40,00 EUR à Lille. Le stockage vaut 40 EUR/tonne partout, il ne
peut donc pas expliquer l'écart ; les 29,21 EUR/t de plus à Lyon (contre 10,91 EUR/t à
Paris) viennent entièrement du transport. Le stockage est le plus gros poste en valeur
absolue, mais seulement parce que Lyon traite beaucoup de tonnes, pas parce qu'il est
mal géré.

## Stage 4 — Réseau

**Réflexion 6.** Je recommande d'**ouvrir Marseille**. C'est le scénario qui fait
baisser le plus la distance moyenne pondérée : 168,04 km (situation actuelle) -> 115,03
km avec Marseille, contre 139,89 km avec Bordeaux ; fermer Lille donne 174,43 km, donc
pire. Le caveat du dashboard (ni le capex, ni le coût de sortie du bail, ni la valeur
stratégique de Lille vers la Belgique et le Royaume-Uni) **baisse ma confiance** sans
changer ma conclusion : je dirais « Marseille d'abord », mais comme hypothèse à valider
par une étude de capex, pas comme décision. Deux limites supplémentaires : une part
importante du gain vient de Marseille elle-même (873 076 habitants, passés de 277,6 km
à 0 km), donc du proxy de population ; et Marseille ne réduit pas le pire cas (435,8
km, Bordeaux servie depuis Lyon), alors que Bordeaux le ferait passer à 382,3 km.
*Retour sur la Réflexion 1 :* j'avais prédit que le responsable coûts serait le plus en
désaccord. C'était **en partie faux** : la route la plus chère en transport est
Marseille ← Lyon (1 454 195 EUR), donc la vue coût pointe elle aussi vers Marseille.
Le vrai désaccord se joue sur **Lille** : les vues CO2 et coût la trouvent « sans
problème, voire fermable », et le planificateur réseau est celui qui la défend.

## Stage 6 — Quatrième graphique (capstone)

**Réflexion 7.** J'ai étendu le **dashboard CO2** avec un nuage de bulles : la distance
à l'entrepôt en x, la demande estimée (tonnes/an) en y, et la taille de la bulle
proportionnelle au CO2 de la ville. Il répond à une question que le top 10 en barres et
la carte ne tranchent pas : une route émet-elle beaucoup parce qu'elle est **longue**
(on peut agir sur le trajet) ou parce que la ville est **grosse** (on ne peut agir que
sur le volume ou le mode de transport) ? Exemple lu sur le graphique : Marseille émet le
plus (1 211 830 kg) avec 277,6 km mais 43 654 t/an, alors que Bordeaux, plus loin
(435,8 km), n'a que 13 090 t/an et émet moins de la moitié (570 471 kg). Le choix du
type : il faut croiser **deux variables numériques** et en lire une troisième, ce que ne
permet ni une barre (une seule mesure), ni un camembert (parts d'un total, pas de
relation), ni la carte (où, mais pas pourquoi). Le nuage de points est le graphique fait
pour voir si deux variables expliquent une troisième.
