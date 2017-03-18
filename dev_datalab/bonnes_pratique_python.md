
# Sommaire des bonnes pratique de développement en python

## En générale : les règles générales à adopter dès le début 

- Un code doit être fait pour les autres et non pour soir même.
- Un code simple est mieux qu'un code fonctionnel (mais difficile à comprendre).
- Préférer le beau du laid.
- Face à l’ambiguïté, ne pas se laisser tenter à deviner.
- Explicite est mieux que implicite
- Tout le monde peut réparer le code de tout le monde. 
- Corriger chaque "fenêtre cassée" (mauvaise conception, mauvaise décision, ou mauvais code) ** dès qu'elle est découverte **.
- Mieux vaut maintenant que jamais
- Testez impitoyablement. Ecrire des documents pour les nouvelles fonctionnalités.
- Encore plus important que Test-Driven Development - * Human-Driven Development *

## En particulier

### Style

Suivez [PEP 8] [], quand sensible.

#### Nommer

- Variables, fonctions, méthodes, paquets, modules
    - `lower_case_with_underscores`
- Classes et exceptions
    - `CapWords`
- Méthodes protégées et fonctions internes
    - `_single_leading_underscore (self, ...)`
- Méthodes privées
    - `__double_leading_underscore (self, ...)`
- Constantes
    - `ALL_CAPS_WITH_UNDERSCORES`

###### Principes directeurs généraux

Évitez les variables à une lettre (en particulier `l`,` O`, `I`).

* Exception *: En blocs très courts, lorsque le sens est clairement visible du contexte immédiat

**Bien**
Python
Pour e dans les éléments:
    E.mutate ()
......

Éviter l'étiquetage redondant.

**Oui**
Python
Import audio

Core = audio.Core ()
Controller = audio.Controller ()
......

**Non**
Python
Import audio

Core = audio.AudioCore ()
Controller = audio.AudioController ()
......

Préfère la notation inverse.

**Oui**
Python
Elements = ...
Elements_active = ...
Elements_defunct = ...
......

**Non**
Python
Elements = ...
Active_elements = ...
Defunct_elements ...
......

Évitez les méthodes getter et setter.

**Oui**
Python
Person.age = 42
......

**Non**
Python
Person.set_age (42)
......

#### Indentation

Utilisez 4 espaces - jamais les onglets. Assez dit.

Importations ####

Importez des modules entiers au lieu de symboles individuels dans un module. Par exemple, pour un module `canteen` qui possède un fichier` canteen / sessions.py`,

**Oui**

Python
Cantine d'importation
Import canteen.sessions
Des sessions d'importation de cantine
......

**Non**

Python
From canteen import get_user # Symbole de la cantine / __ init__.py
From canteen.sessions import get_session # Symbole de cantine / sessions.py
......

* Exception *: Pour le code tiers où la documentation dit explicitement d'importer des symboles individuels.

* Justification *: Evite les importations circulaires. Voir [ici] (https://sites.google.com/a/khanacademy.org/forge/for-developers/styleguide/python#TOC-Imports).

Mettez toutes les importations en haut de la page avec trois sections, chacune séparée par une ligne vide, dans cet ordre:

1. Importations de systèmes
2. Importations tierces
3. Importations d'arbres sources locales

* Raison *: Indique clairement d'où provient chaque module.

#### Documentation

Suivez les directives de docstring [PEP 257] []. [ReStructured Text] (http://docutils.sourceforge.net/docs/user/rst/quickref.html) et [Sphinx] (http://sphinx-doc.org/) peuvent aider à faire respecter ces normes.

Utilisez des docstrings à une ligne pour des fonctions évidentes.

Python
"" "Renvoie le chemin d'accès de` `foo``." ""
......

Les chaînes de caractères multilignes

- Ligne récapitulative
- Cas d'utilisation, le cas échéant
- Args
- Type de retour et sémantique, sauf si «None» est renvoyé

Python
"" "Former un modèle pour classer Foos et Bars.

Usage::

    >>> import klassify
    >>> données = [("vert", "foo"), ("orange", "bar")]
    >>> classifier = klassify.train (données)

: Param train_data: Liste des tuples de la forme `` (color, label) ``.
: Rtype: A: class: `Classifier <Classifier>`
"" "
......

Remarques

- Utilisez des mots d'action («Retour») plutôt que des descriptions («Retours»).
- Document `__init__` méthodes dans le docstring pour la classe.

Python
Classe Personne (objet):
    - Une simple représentation d'un être humain.

    : Param nom: Une chaîne, le nom de la personne.
    : Param age: Un int, l'âge de la personne.
    "" "
    Def __init __ (nom, prénom, âge):
        Self.name = name
        Self.age = âge
......

##### Sur les commentaires

Utilisez-les avec parcimonie. Préférez la lisibilité du code à l'écriture de beaucoup de commentaires. Souvent, les petites méthodes sont plus efficaces que les commentaires.

*Non*

Python
# Si le signe est un stop
Si sign.color == 'rouge' et sign.sides == 8:
    Arrêtez()
......

*Oui*

Python
Def is_stop_sign (signer):
    Return sign.color == 'rouge' et sign.sides == 8

Si is_stop_sign (signe):
    Arrêtez()
......

Lorsque vous écrivez des commentaires, n'oubliez pas: "Strunk et blanc s'appliquent." - [PEP 8] []

#### Longueur des lignes

Ne pas le stress sur elle. 80-100 caractères est très bien.

Utilisez des parenthèses pour les suites de lignes.
