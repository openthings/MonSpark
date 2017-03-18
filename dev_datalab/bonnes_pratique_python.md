
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

Quelques règles extraites à partir de [PEP 8].

#### 1. Nommage

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
Pour e dans les éléments:
    E.mutate ()
```

Éviter l'étiquetage redondant.

**Oui**
```
Import audio

Core = audio.Core ()
Controller = audio.Controller ()
```

**Non**
```
Import audio

Core = audio.AudioCore ()
Controller = audio.AudioController ()
```

Préférer la notation inverse.

**Oui**
```
Elements = ...
Elements_active = ...
Elements_defunct = ...
```

**Non**
```
Elements = ...
Active_elements = ...
Defunct_elements ...
```

Évitez les méthodes getter et setter.

**Oui**
```
Person.age = 42
```
**Non**
```
Person.set_age (42)
```

#### 2. Indentation

Utilisez 4 espaces - jamais les tabulations.

Importations ####

Importez des modules entiers au lieu de symboles individuels dans un module. 
Par exemple, pour un module `canteen` qui possède un fichier `canteen/sessions.py`,

**Oui**

```
import canteen
import canteen.sessions
from canteen import sessions
```

**Non**

```
from canteen import get_user  # Symbol from canteen/__init__.py
from canteen.sessions import get_session  # Symbol from canteen/sessions.py
```

Mettez tous les imports en haut de la page avec trois sections, chacune séparée par une ligne vide, dans cet ordre:

1. Importations de systèmes
2. Importations tierces
3. Importations de branches de sources locales

#### 3. Documentation
Une seule ligne (docstrings) par fonction

```
"""Retourne le chemin d'accès de ``foo``."""
```
......

Les chaînes de caractères multilignes

- Ligne récapitulative
- Cas d'utilisation, le cas échéant
- Args
- Type de retour et sémantique, sauf si «None» est renvoyé

```
Classe Personne (objet):
    - Une simple représentation d'un être humain.

    : Param name: Une chaîne, le nom de la personne.
    : Param age: Un int, l'âge de la personne.
    "" "
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Outils de documentation, ou comment transformer automagiquement un code-source bien documenté en une documentation fonctionnelle: 
- Les directives de docstring [PEP 257]. 
- ReStructured Text (http://docutils.sourceforge.net/docs/user/rst/quickref.html) et 
- [Sphinx] (http://sphinx-doc.org/)

##### Sur les commentaires

Utilisez-les avec parcimonie. Préférez la lisibilité du code à l'écriture de beaucoup de commentaires. Souvent, les petites méthodes sont plus efficaces que les commentaires.

*Non*
```
if sign.color == 'red' and sign.sides == 8:
    stop()
```

*Oui*
```
def is_stop_sign(sign):
    return sign.color == 'red' and sign.sides == 8

if is_stop_sign(sign):
    stop()
```

#### Longueur des lignes

80-100 caractères c'est très bien.

Utilisez des parenthèses pour les suites de lignes.
```
wiki = (
    "bla bla bla ..."
    "bla blo blo ..."
    "bli bli bli ..."
)
```
### Développement piloté par les tests
Le Test Driven Development est une méthode de programmation qui permet d’éviter des bugs a priori plutôt que de les résoudre a posteriori. Ce n’est pas une méthode propre à Python, elle est utilisée très largement par les programmeurs professionnels.

Le cycle préconisé par TDD comporte cinq étapes :

1. écrire un premier test ;
2. vérifier qu’il échoue (puisque le code qu’il teste n’existe pas encore), afin de s’assurer que le test est valide et exécuté ;
3. écrire un code minimal pour passer le test ;
4. vérifier que le test passe correctement ;
5. éventuellement « réusiner » le code (refactoring), c’est-à-dire l’améliorer (rapidité, lisibilité) tout en gardant les mêmes fonctionnalités.

Diviser pour mieux régner: chaque fonction, classe ou méthode est testée indépendemment. Ainsi, lorsqu’un nouveau morceau de code ne passe pas les tests qui y sont associés, il est certain que l’erreur provient de cette nouvelle partie et non des fonctions ou objets que ce morceau de code utilise. On distingue ainsi hiérarchiquement:

1. Les tests unitaires vérifient individuellement chacune des fonctions, méthodes, etc.
2. Les tests d’intégration évaluent les interactions entre différentes unités du programmes.
3. Les tests système assurent le bon fonctionnement du programme dans sa globalité.

Il est essentiel de garder tous les tests au cours du développement, ce qui permet de les réutiliser lorsque l’on veut compléter ou améliorer une partie du code. Si le nouveau code passe toujours les anciens test, on est alors sûr de ne pas avoir cassé les fonctionnalités précédentes.
```
import unittest
import os
import mock


def simple_urandom(length):
    return 'f' * length


class TestRandom(unittest.TestCase):
    @mock.patch('os.urandom', side_effect=simple_urandom)
    def test_urandom(self, urandom_function):
        assert os.urandom(5) == 'fffff'
 ```       
**Attention** : Prendre l'habitude de tester toute fonction développé. Mais attention d'en faire une obssession.

#### Tests unitaires
... TODO 

#### Tests fonctionnels
 ... TODO 

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
