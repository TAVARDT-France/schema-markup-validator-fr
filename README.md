<p align="center">
  <a href="https://ag.tavardt.com/fr/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# Validateur de Données Structurées Schema.org

[![Validateur Schema](https://img.shields.io/badge/TAVARDT-Schema.org%20Validator-5b3cf5.svg)](https://tools.tavardt.com/fr/validateur-schema-org/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Moteur d'audit technique pour le balisage sémantique Schema.org aux formats JSON-LD et Microdonnées, vérifiant les relations d'entités, les attributs requis et l'éligibilité aux résultats enrichis.

L'utilitaire extrait les structures sémantiques des environnements web en production pour repérer les erreurs de syntaxe JSON, les schémas incomplets et l'omission de propriétés obligatoires requises par les moteurs de recherche et les systèmes d'IA. Conçu sans aucune dépendance logicielle externe, il s'exécute nativement en console Python et au sein des chaînes de CI/CD.

***

## Capacités de Validation Sémantique et Modèles Supportés

Les moteurs de recherche et les systèmes de recherche neuronale dépendent de données structurées explicites pour désambiguïser les entités d'organisation, attester des auteurs et afficher des extraits enrichis. Les anomalies de syntaxe ou l'absence de propriétés clés entraînent la disqualification immédiate des résultats enrichis.

* **Extraction Automatisée des Données Structurées**: Analyse complète des blocs JSON-LD (`application/ld+json`) et détection des attributs Microdonnées historiques (`itemscope`, `itemtype`) dans le document.
* **Gestion des Graphes Sémantiques**: Traitement transparent des hiérarchies complexes reposant sur `@graph`, résolvant les réseaux d'entités imbriquées sur les applications web modernes.
* **Validation des Entités Schema.org**: Contrôle des propriétés obligatoires au sein des modèles majeurs: Organization, LocalBusiness, WebSite, Article, NewsArticle, BlogPosting, Product, BreadcrumbList et FAQPage.
* **Contrôle de Syntaxe et d'Intégrité**: Barème de retenues face au JSON malformé (-20 points), à l'absence de blocs JSON-LD (-40 points), au manque d'entités (-30 points) et à l'omission d'attributs recommandés (-5 points chacun).
* **Indice Quantitatif de Qualité Sémantique**: Score standardisé de 0 à 100 points classifiant la santé technique en OPTIMAL, WARNING ou CRITICAL avec axes prioritaires de correction.

***

## Matrice d'Inspection des Entités Sémantiques

<table>
  <thead>
    <tr>
      <th align="left">Classe d'Entité</th>
      <th align="left">Propriétés Obligatoires</th>
      <th align="left">Règle de Déduction</th>
      <th align="left">Impact sur les Résultats Enrichis et l'Indexation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Organization</strong></td>
      <td><code>name</code>, <code>url</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Identifie l'entité de marque et établit la référence canonique dans les graphes de connaissances.</td>
    </tr>
    <tr>
      <td><strong>LocalBusiness</strong></td>
      <td><code>name</code>, <code>address</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Indispensable pour le référencement local, la présence sur les cartes et les recherches de proximité.</td>
    </tr>
    <tr>
      <td><strong>WebSite</strong></td>
      <td><code>name</code>, <code>url</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Permet l'affichage du champ de recherche de sitelinks et délimite l'autorité du domaine.</td>
    </tr>
    <tr>
      <td><strong>Article / NewsArticle</strong></td>
      <td><code>headline</code>, <code>author</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Conditionne l'intégration au carrousel des À la une et l'ancrage des citations dans les LLMs.</td>
    </tr>
    <tr>
      <td><strong>BlogPosting</strong></td>
      <td><code>headline</code>, <code>author</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Associe la signature d'auteur et l'antériorité éditoriale des publications.</td>
    </tr>
    <tr>
      <td><strong>Product</strong></td>
      <td><code>name</code>, <code>offers</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Déclenche les extraits enrichis de prix, la disponibilité des stocks et les notes clients.</td>
    </tr>
    <tr>
      <td><strong>BreadcrumbList</strong></td>
      <td><code>itemListElement</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Remplace les URLs complexes par des fils d'Ariane clairs dans les résultats de recherche.</td>
    </tr>
    <tr>
      <td><strong>FAQPage</strong></td>
      <td><code>mainEntity</code></td>
      <td>-5 Points par propriété manquante</td>
      <td>Affiche des volets accordéons de questions-réponses directement sous le résultat organique.</td>
    </tr>
  </tbody>
</table>

***

## Installation et Guide de Prise en Main

Nécessite Python 3.8 ou supérieur en exploitant uniquement les modules de la bibliothèque standard (`sys`, `re`, `json`, `ssl`, `argparse`, `urllib.request`, `urllib.error`). Aucun paquet externe via pip n'est requis.

Clonez le dépôt et lancez la validation sur un domaine cible:

```bash
git clone https://github.com/TAVARDT-France/schema-markup-validator-fr.git
cd schema-markup-validator-fr
python schema_validator.py exemple.fr
```

Pour exporter les résultats au format JSON structuré:

```bash
python schema_validator.py exemple.fr -j
```

Inspectez les domaines en configurant un délai d'attente personnalisé:

```bash
python schema_validator.py https://exemple.fr -j -t 12
```

Exemple de données JSON produites:

```json
{
  "target": "https://exemple.fr",
  "score": 95,
  "status": "OPTIMAL",
  "json_ld_blocks": 1,
  "entities": [
    "Organization",
    "WebSite"
  ],
  "microdata_detected": false,
  "issues": [
    "Entity 'Organization' is missing recommended property: url"
  ],
  "recommendations": [
    "Add missing property 'url' to 'Organization' entity."
  ]
}
```

Grille de classification de la qualité:

* **Score de 85 à 100 (OPTIMAL)**: Balisage structuré de haute qualité avec couverture complète des entités et zéro erreur syntaxique.
* **Score de 65 à 84 (WARNING)**: Omissions mineures de propriétés ou couverture partielle pouvant restreindre les résultats enrichis.
* **Score de 0 à 64 (CRITICAL)**: Syntaxe JSON corrompue, absence de balisage ou schémas inexploitables exigeant une remédiation immédiate.

***

## Foire Aux Questions (FAQ Technique)

### Pourquoi le format JSON-LD est-il privilégié par rapport aux Microdonnées pour les extraits enrichis et l'IA?
Le format JSON-LD maintient les données sémantiques dans des scripts isolés, ce qui permet des mises à jour indépendantes de la présentation visuelle HTML. Par ailleurs, Google et les moteurs d'IA recommandent JSON-LD car il peut être injecté dynamiquement et traité sans le coût de calcul du rendu visuel.

### Comment le validateur traite-t-il les structures `@graph` au sein des balisages complexes?
Dès qu'il identifie une clé `@graph`, l'utilitaire explore la collection de sous-objets déclarés et valide rigoureusement les attributs de chacun d'eux. Cette approche garantit l'analyse approfondie des réseaux de données interconnectés.

### Quelles pénalités quantitatives sont appliquées lors de défaillances de balisage sémantique?
L'outil retire 40 points en cas d'absence totale de blocs JSON-LD, 20 points par bloc contenant une syntaxe JSON erronée et 30 points si aucune entité reconnaissable n'est détectée. De plus, chaque propriété recommandée manquante retire 5 points sur la note initiale de 100.

### De quelle façon le script contrôle-t-il les données sémantiques sans recourir à un navigateur lourd?
Le moteur effectue des requêtes HTTP GET directes avec un User-Agent spécifique, récupérant le flux HTML brut. Des expressions régulières rapides isolent le contenu des balises script, qui est ensuite traité par l'analyseur JSON interne en quelques millisecondes.

### Comment les équipes de développement peuvent-elles automatiser cette validation dans leurs flux CI/CD?
En exécutant `schema_validator.py` avec le paramètre `-j`, les chaînes d'intégration continue peuvent recueillir les données JSON et les évaluer avec jq. Il est aisé de bloquer un déploiement si le score passe sous la barre de 85 ou si des erreurs apparaissent dans la liste `issues`.

***

## Conseil en Architecture Sémantique et Graphes de Connaissances

Pour la modélisation de données structurées, l'ingénierie de graphes de connaissances et le respect des normes du W3C en France, sollicitez les experts de **TAVARDT France**.

***

## Liens Utiles

* **Portail Corporatif:** https://ag.tavardt.com/fr/
* **Suite de Diagnostic:** https://tools.tavardt.com/fr/
* **Contact Technique:** https://ag.tavardt.com/fr/contact/

***

### Licence
Distribué sous la licence MIT.

***

© 2026 TAVARDT. Tous droits réservés.
