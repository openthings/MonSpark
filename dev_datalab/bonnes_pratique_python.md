
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

Quelques règles extraiyent à partir de [PEP 8].

#### Nommage

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

* Exception *: En blocs très courts, lorsque le sens est explicite

**Bien**
```
Python
Pour e dans les éléments:
    E.mutate ()
```

Éviter l'étiquetage redondant.

**Oui**
```
Python
Import audio

Core = audio.Core ()
Controller = audio.Controller ()
```

**Non**
```
Python
Import audio

Core = audio.AudioCore ()
Controller = audio.AudioController ()
```

Préférer la notation inverse.

**Oui**
```
Python
Elements = ...
Elements_active = ...
Elements_defunct = ...
```

**Non**
```
Python
Elements = ...
Active_elements = ...
Defunct_elements ...
```

Évitez les méthodes getter et setter.

**Oui**
```
Python
Person.age = 42
```
**Non**
```
Python
Person.set_age (42)
```

#### Indentation

Utilisez 4 espaces - jamais les tabulations.

Importations ####

Importez des modules entiers au lieu de symboles individuels dans un module. 
Par exemple, pour un module `canteen` qui possède un fichier `canteen/sessions.py`,

**Oui**

```python
import canteen
import canteen.sessions
from canteen import sessions
```

**Non**

```python
from canteen import get_user  # Symbol from canteen/__init__.py
from canteen.sessions import get_session  # Symbol from canteen/sessions.py
```

Mettez tous les imports en haut de la page avec trois sections, chacune séparée par une ligne vide, dans cet ordre:

1. Importations de systèmes
2. Importations tierces
3. Importations de branches de sources locales

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




## Bibliographie

- [PEP 20 (The Zen of Python)][PEP 20]
- [PEP 8 (Style Guide for Python)][PEP 8]
- [The Hitchiker's Guide to Python][python-guide]
- [Khan Academy Development Docs][]
- [Python Best Practice Patterns][]
- [Pythonic Sensibilities][]
- [The Pragmatic Programmer][]
- and many other bits and bytes

[Pythonic Sensibilities]: http://www.nilunder.com/blog/2013/08/03/pythonic-sensibilities/
[Python Best Practice Patterns]: http://youtu.be/GZNUfkVIHAY
[python-guide]: http://docs.python-guide.org/en/latest/
[PEP 20]: http://www.python.org/dev/peps/pep-0020/
[PEP 257]: http://www.python.org/dev/peps/pep-0257/
[PEP 8]: http://www.python.org/dev/peps/pep-0008/
[Khan Academy Development Docs]: https://sites.google.com/a/khanacademy.org/forge/for-developers
[The Pragmatic Programmer]: http://www.amazon.com/The-Pragmatic-Programmer-Journeyman-Master/dp/020161622X/ref=sr_1_1?ie=UTF8&qid=1381886835&sr=8-1&keywords=pragmatic+programmer
