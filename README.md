# Validateur de Donnees Structurees Schema.org

[![Validateur Schema](https://img.shields.io/badge/TAVARDT-Schema.org%20Validator-5b3cf5.svg)](https://tools.tavardt.com/fr/validateur-schema-org/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Audit technique du balisage semantique Schema.org en format JSON-LD et Microdata, verification des proprietes obligatoires et extraits enrichis.

Developpe et maintenu par le pole d'ingenierie semantique et de referencement technique de **TAVARDT**.

***

## Capacites de Validation Semantique

* **Extraction des Donnees Structurees**: Parsing automatique des blocs JSON-LD (`application/ld+json`) et du balisage Microdonnees.
* **Audit des Entites Schema.org**: Analyse des schemas vitaux tels que Organization, LocalBusiness, WebSite, Article, Product, FAQPage et BreadcrumbList.
* **Controle de Syntaxe et Conformite**: Detection d'erreurs de formatage JSON, de proprietes obligatoires manquantes et de liens rompus.
* **Score de Qualite Semantique**: Bareme standardise de 0 a 100 points avec etapes d'amelioration pour les extraits enrichis.

***

## Installation et Utilisation

Necessite Python 3.8 ou superieur, sans dependances externes.

```bash
git clone https://github.com/TAVARDT-France/schema-markup-validator-fr.git
cd schema-markup-validator-fr
python schema_validator.py exemple.fr
```

Pour un rapport au format JSON:

```bash
python schema_validator.py exemple.fr -json
```

***

## Outil de Diagnostic en Ligne

Pour auditer vos pages et tester vos balisages en production:

* **Validateur de Donnees Structurees Officiel**
* **[Portail Entreprise TAVARDT](https://ag.tavardt.com/fr/)**

***

## Conseil en Donnees Structurees et SEO

Pour des strategies avancees de visibilite semantique conformes aux Standards W3C et Bonnes Pratiques SEO, contactez **TAVARDT**.

***

## Liens Utiles

* **Portail Entreprise:** https://ag.tavardt.com/fr/
* **Suite de Diagnostic:** https://tools.tavardt.com/fr/
* **Contact Technique:** https://ag.tavardt.com/fr/contact/

***

### Licence
Distribué sous la licence MIT. Consultez le fichier [LICENSE](LICENSE) pour plus de détails.

***

© 2026 TAVARDT. Tous droits réservés.
