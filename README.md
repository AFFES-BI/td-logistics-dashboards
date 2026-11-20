# td-logistics-dashboards

## Tableau de bord

[Ouvrir les tableaux de bord](https://affes-bi.github.io/td-logistics-dashboards/)

Ces trois tableaux de bord présentent un même réseau logistique (3 entrepôts existants :
Paris, Lyon, Lille ; 20 villes françaises) vu par trois responsables qui prennent trois
décisions différentes : réduire le CO2 (RSE), maîtriser les coûts (opérations) et
décider d'ouvrir ou de fermer un entrepôt (stratégie). Les chiffres sont calculés à
partir de `data/cities.csv` par `scripts/compute_kpis.py`, puis recalculés à la demande
par une GitHub Action. La demande est estimée à partir de la population (proxy, pas des
volumes réels), avec un facteur de 0,10 kg CO2e par tonne-km.

## Réflexions

[Consulter mes réponses au TD](REFLECTIONS.md)
