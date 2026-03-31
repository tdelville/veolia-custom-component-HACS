# Veolia

[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]
[![License][license-shield]](LICENSE)

[![hacs][hacsbadge]][hacs]
[![Project Maintenance][maintenance-shield]][user_profile]


J'ai créé un Fork depuis le projet https://github.com/kugan49/veolia-custom-component-HACS car il n'est plus maintenu et archivé ; mais merci à lui d'avoir fait tout le boulot!
Le fait qu'il soit archivé semblait poser un problème lors de l'ajout du dépot personnalisé dans HACS.
De plus l'ajout de l'intégration était impossible dans la version 2026.3.4 de HA ; c'est corrigé.
Je ne promets pas de maintenir le projet, mais à minima de régler les micro-problèmes du genre, qui empêche de fonctionner dans une version récente de HA.

Info importante / rappel : cette intégration ne fonctionne que si vous accéder à voter espace client via https://www.service.eau.veolia.fr/ (ancien site, amis qui est toujours en vigueur me concernant/dans ma commune).
Si vous acccéder à l'espace client via https://www.eau.veolia.fr/, alors il faut utiliser plutôt cette intégration HACS : https://github.com/Jezza34000/homeassistant_veolia.


![logo][logoimg]

**Ce composant configurera les plates-formes suivantes.**

Platform | Description
-- | --
`sensor` | Affichez la consommation quotidienne et mensuelle ainsi que la dernière valeur d'index de l'API Veolia. Ce sensor est de type enregie, il apparaitra donc dans le tableau de bord Energie


![appareil][appareilimg]

![daily_consumption][daily_consumptionimg]

![monthly_consumption][monthly_consumptionimg]


## Installation

### HACS

Recommandé car vous recevrez des notifications de mises à jour

[![Ouvrez votre instance Home Assistant et ouvrez ce référentiel dans la boutique communautaire Home Assistant.][my_hacs_badge]][my_ha_link]

Si le lien ci-dessus ne fonctionne pas, suivez ces étapes :
*  Ajoutez ce référentiel https://github.com/tdelville/veolia-custom-component-HACS/ à HACS en tant que « Dépôts personnalisés » avec la catégorie « Intégration ».  Cette option se trouve dans le menu ⋮
* Installer l'intégration depuis HACS
* Redémarrez Home Assistant

### Manuellement

* Extrayez le fichier Zip dans le répertoire `custom_components`
* Redémarrez Home Assistant

## La configuration se fait dans l'interface utilisateur

Remplissez simplement votre nom d'utilisateur et votre mot de passe lors de l'ajout de l'intégration

Si vous avez plusieurs compteurs, vous pouvez renseigner la référence abonnement pour récupérer les bon résultats.
Si vous ne la renseignez pas, le premier abonnement sera automatiquement selectionné.

La référence abonnement se trouve dans l'onglet `Gérer votre Espace Personnel` dans la section `Mes Contrats`, sous la colonne `Références`

Vous pouvez ajouter autant d'intégration que de compteur à suivre.


## Ajoutez une carte apexcharts pour afficher l'attribut d'historique

Vous pouvez utiliser [apexcharts-card](https://github.com/RomRider/apexcharts-card)

```yaml

type: custom:apexcharts-card
graph_span: 1month
header:
  show: true
  title: ApexCharts-Card
  show_states: true
  colorize_states: true
series:
  - entity: sensor.veolia_daily_consumption
    type: column
    data_generator: |
      return entity.attributes.historyConsumption.map((val, index) => {
        return [new Date(val[0]).getTime(), val[1]];
      });

```

![apexchartsimg]


## Remerciement spécial

Un grand merci à [@Pulpyyyy](https://github.com/Pulpyyyy), qui m'a beaucoup aidé dans la recherche du fonctionnement de l'API

<!---->
***

[commits-shield]: https://img.shields.io/github/commit-activity/y/tdelville/veolia-custom-component-HACS.svg?style=for-the-badge
[commits]: https://github.com/tdelville/veolia-custom-component-HACS/commits/master
[hacs]: https://hacs.xyz
[hacsbadge]: https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge
[my_hacs_badge]: https://my.home-assistant.io/badges/hacs_repository.svg
[my_ha_link]: https://my.home-assistant.io/redirect/hacs_repository/?owner=tdelville&repository=veolia-custom-component-HACS&category=integration
[logoimg]: images/logo.png
[appareilimg]: images/appareil.png
[daily_consumptionimg]: images/daily_consumption.png
[monthly_consumptionimg]: images/monthly_consumption.png
[apexchartsimg]: images/apexcharts-card_example.png
[license-shield]: https://img.shields.io/github/license/tdelville/veolia-custom-component-HACS.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/maintainer-%40kugan49-blue.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/tdelville/veolia-custom-component-HACS.svg?style=for-the-badge
[releases]: https://github.com/tdelville/veolia-custom-component-HACS/releases
[user_profile]: https://github.com/tdelville
