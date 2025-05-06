# Solar-Monitor-Shelly-Pro3-EM

Ce script est un petit utilitaire conçu pour suivre la production d'énergie solaire, calculer les économies réalisées grâce à la consommation solaire et estimer la réduction de CO₂ évitée, tout en intégrant la gestion des tarifs Tempo. Il peut être utilisé avec un compteur Shelly pour mesurer la production et la consommation d'énergie, et il peut également récupérer des informations de tarifs Tempo via MQTT.

Fonctionnalités principales :
    Suivi de la production et consommation d'énergie solaire :
    Le script récupère régulièrement l'état du compteur Shelly (type em:0) pour mesurer la production solaire (énergie produite) et la consommation (énergie utilisée du réseau).
    Il suit également l'énergie injectée dans le réseau et l'énergie autoconsommée (utilisée directement par la maison).
    Calcul des économies et du CO₂ évité :
    Le script calcule les économies réalisées en fonction de l'énergie autoconsommée et du tarif Tempo actuel (heures pleines ou heures creuses).
    Il calcule également le CO₂ évité en fonction de la production d'énergie solaire, en supposant que chaque kWh produit permet d'éviter 0,06 kg de CO₂.

Utilisation des tarifs Tempo :
Le tarif varie selon la zone (Bleu, Blanc, Rouge), et selon si l'heure est en heures pleines (HP) ou heures creuses (HC). Le tarif est automatiquement ajusté à chaque période.
Le script récupère la zone Tempo actuelle via MQTT (chaque fois que la zone est mise à jour sur le topic tempo/jour_couleur).

Réinitialisation journalière :
Le script réinitialise les données (énergie produite, injectée, autoconsommée, économies et CO₂) chaque jour à minuit, ce qui permet de suivre la consommation et la production sur une base quotidienne.

Affichage des données :
Le script affiche régulièrement un résumé des informations suivantes :
Zone Tempo actuelle
Production solaire
Consommation réseau
Autoconsommation et injection réseau
Économies réalisées (en euros)
CO₂ évité

Configuration MQTT :
Le script utilise un serveur MQTT pour recevoir les mises à jour de la zone Tempo. Chaque fois que le message de zone Tempo change, il met à jour la zone active.

Comment utiliser ce script :
Pré-requis :
Ce script est conçu pour être utilisé avec un compteur Shelly (ex. em:0) qui mesure la production et la consommation d'énergie.
Un serveur MQTT doit être configuré pour recevoir les messages sur le topic tempo/jour_couleur. Ce serveur pourra être connecté à un service de gestion des tarifs Tempo (ou utilisé pour recevoir ces informations d'une autre source).
Vous devez disposer d'une clé API pour obtenir les prévisions météo si vous souhaitez l'intégrer, bien que cette partie ne soit pas strictement nécessaire pour la partie énergie.

Configuration :
Vous devez modifier les paramètres suivants dans le script :
La clé API météo (si vous activez la fonction météo).
La configuration du serveur MQTT et du topic de la zone Tempo (ce dernier peut être lié à un service comme Hivemq Cloud).

Fonctionnement :

Le script fonctionne de manière autonome, en récupérant les informations sur l'énergie, les économies et le CO₂ chaque minute.
Les résultats sont affichés régulièrement dans la console, avec des mises à jour sur les économies réalisées et l'impact environnemental.

Exemple de sortie (logs) :
markdown
Copy
Edit
====== Suivi énergie (Tempo) ======
📅 Zone Tempo : Bleu
☀️  Solaire : 120.0 W
⚡️ Réseau : -50.0 W
🔋 Produite : 120.00 Wh
🏠 Autoconsommée : 80.00 Wh
🔁 Injectée : 40.00 Wh
💰 Économie : 0.012 €
🌱 CO₂ évité : 0.005 kg
===================================
Points à personnaliser :
Vous pouvez personnaliser les zones Tempo et les tarifs si nécessaire (ex. si vous utilisez un autre fournisseur de tarifs).

Le code météo est optionnel mais peut être activé pour afficher des informations supplémentaires.

Résumé :
Ce script est conçu pour aider à la gestion de l'énergie solaire à domicile en calculant automatiquement les économies et la réduction de CO₂ en fonction de la production d'énergie solaire, tout en tenant compte des tarifs Tempo et en intégrant des informations sur la zone Tempo via MQTT. Il fournit un suivi détaillé de la consommation d'énergie, des économies, et de l'impact environnemental, tout en réinitialisant les données chaque jour.
