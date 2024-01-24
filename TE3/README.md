# TE3

## vector resize

1. Que se passe-t-il après l'execution de ce code ?

```cpp
std::vector<int> vec;
vec.resize(4, 10);
```

<details>
<summary>Solution</summary>

Le vecteur contient 4 éléments, tous égaux à 10

</details>


## substr

2. Que retourne le code suivant ?

```cpp
std::string str = "abcdef" 
std::cout << str.substr(2)
```

<details>
<summary>Solution</summary>

```cpp
cdef
```

</details>


## tableaux

3. Considérer le fragment de code suivant :

```cpp
int myArray[5] = {1, 2, 3, 4, 5};
std::vector<int> myVector;
// Votre code pour copier les éléments de myArray dans myVector
```

Quel serait le code nécessaire pour copier les éléments de myArray dans myVector ?

<details>
<summary>Solution</summary>

```cpp
for (int i = 0; i < 5; ++i) {
    myVector.push_back(myArray[i]);
}
```

</details>


## string et chaine de caractères

4. Écrivez un fragment de code en C++ (uniquement les lignes nécessaires) pour :

	* **Initialiser** une nouvelle chaîne ``std::string`` nommée ``newString`` en conservant uniquement les caractères ``"llo"`` **à partir de la chaîne** ``std::string originalString = "Hello World!";``
	* **Initialiser** une autre chaîne ``std::string nommée`` anotherString **à partir d'une chaîne de caractères constante** ``const char* cStyleConstString = "Example";`` en utilisant les 4 premiers caractères.

<details>
<summary>Solution</summary>

```cpp
std::string originalString = "Hello World!";
std::string newString(originalString, 2, 3);  // newString = "llo"

const char* cStyleConstString = "Example";
std::string anotherString(cStyleConstString, 4);  // anotherString = "Exam"
```

</details>


## Tableaux

5. Vector Fusion!

Compléter le code donné pour écrire un programme en C++ qui fusionne deux vecteurs de manière efficace et conforme à certaines contraintes.

**Voici les détails :**

* Vous disposerez de deux ``std::vector<int>` : un nommé ``vecteurTrie`, contenant une séquence triée d'entiers, et un autre nommé ``vecteurNonTrie``, contenant des entiers non triés.
* Votre objectif est de fusionner ``vecteurNonTrie`` dans ``vecteurTrie``. La fusion doit être réalisée de telle manière que ``vecteurTrie`` reste trié après l'ajout des éléments de ``vecteurNonTrie`.

**Contraintes :**

* L'utilisation des **itérateurs**, des **fonctions de l'en-tête <algorithm>**, ou de **toute autre bibliothèque non standard** est **interdite**.

**Exemple d'execution** 

Pour les deux vecteurs suivants :

```cpp
vecteurTrie = [2, 5, 23, 35, 59, 88, 101]

vecteurNonTrie = [42, 7, 25, 1]
```

le sortie du code est la suivante :

```
1 2 5 7 23 25 35 42 59 88 101
```

```cpp
/src/main.cpp

#include <iostream>
#include <vector>
#include <span>

// Fonction(s) a implémenter
//
//

int main() {
    std::vector<int> vecteurTrié = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39}; 
    std::vector<int> vecteurNonTrié = {4, 22, 18, 30};

    fusionnerVecteurs(vecteurTrié, vecteurNonTrié);

    
    for (int i : vecteurTrié) {
        std::cout << i << " ";
    }

    return 0;
}
```

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <vector>
#include <span> //pas nécessaire

// Fonction pour insérer un élément dans le vecteur trié à la position correcte
void insererTrie(std::vector<int>& v, int nombre) {
    int i;
    for (i = 0; i < v.size(); ++i) {
        if (nombre < v[i]) {
            break;
        }
    }

    // Décaler les éléments pour créer un espace pour le nouvel élément
    v.insert(v.begin() + i, nombre);
}

// Fonction pour fusionner deux vecteurs, où 'n' est fusionné dans 'v'
void fusionnerVecteurs(std::vector<int>& v, const std::vector<int>& n) {
    for (int nombre : n) {
        insererTrie(v, nombre);
    }
}

int main() {
    std::vector<int> vecteurTrié = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39}; // Vecteur trié
    std::vector<int> vecteurNonTrié = {4, 22, 18, 30}; // Vecteur non trié

    fusionnerVecteurs(vecteurTrié, vecteurNonTrié); // Fusionner 'vecteurNonTrié' dans 'vecteurTrié'

    // Imprimer le vecteur fusionné
    for (int i : vecteurTrié) {
        std::cout << i << " ";
    }

    return 0;
}
```

</details>


6. Analyseur de Fréquence des Mots

**Objectif :** Implémenter un ensemble de fonctions pour analyser la fréquence des mots dans un texte donné.

**Contexte**

On vous fournit un corpus de texte (sous forme de ``const char*`). Votre tâche consiste à implémenter des fonctions qui analysent ce texte pour déterminer la fréquence de chaque mot. Un mot est défini comme une séquence de caractères séparés par des espaces. La ponctuation doit être ignorée.

**Exigences**

Utilisez ``std::vector et std::string` (ou des tableaux de caractères, ``const char*, std::string_view``) pour manipuler les données. Implémentez les fonctions suivantes :

* ``nettoyer_entree`` : Cette fonction retourne un ``std::string``. Elle doit supprimer la ponctuation et convertir tous les caractères en minuscules pour une comparaison cohérente.
* ``diviser_en_mots`` : Cette fonction prend l'entrée nettoyée et retourne un ``std::vector<std::string>``. Elle divise la chaîne d'entrée en mots individuels.
* ``compter_frequence_des_mots`` : Cette fonction prend le vecteur de mots et retourne un ``std::vector<std::pair<std::string, int>>`. Elle compte la fréquence de chaque mot unique et stocke le mot avec sa fréquence dans la paire.

**Contraintes :**

* L'utilisation des **itérateurs**, des **fonctions de l'en-tête <algorithm>**, ou de **toute autre bibliothèque non standard** est **interdite**.

**Exemple d'entrée** 

```cpp
const char* texte = "Bonjour le monde ! Le monde est plein de merveilles. Explorez le monde.";
```

**Résultat Attendu**

```
bonjour - 1
le - 3
monde - 3
est - 1
plein - 1
de - 1
merveilles - 1
explorez - 1
```

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <cctype>
#include <utility>

// Nettoyer l'entrée
std::string nettoyer_entree(????) {
    // Implémenter la fonction qui nettoie le texte_brut en enlevant la ponctuation  
    // et en convertissant en minuscules
}

// Diviser la chaîne de caractères en mots
std::vector<std::string> diviser_en_mots(????) {
    // Implémenter la fonction qui prend le texte nettoyé et le divise en mots individuels
}

// Compter la fréquence des mots
std::vector<std::pair<std::string, int>> compter_frequence_des_mots(?????) {
    // Implémenter la fonction qui prend un vecteur de mots et compte la fréquence de 
    // chaque mot unique.
    // Retourner un vecteur de paires, chaque paire contenant un mot et sa fréquence.
    // Les mots doivent être retournés dans l'ordre de leur apparition dans le texte.
}

// Fonction principale pour tester
int main() {
    const char* texte = "Bonjour le monde! Le monde est plein de merveilles. Explorez le monde.";
    std::string texte_nettoye = nettoyer_entree(texte);
    std::vector<std::string> mots = diviser_en_mots(texte_nettoye);
    std::vector<std::pair<std::string, int>> frequence = compter_frequence_des_mots(mots);

    for (const auto& paire : frequence) {
        std::cout << paire.first << " - " << paire.second << std::endl;
    }

    return 0;
}
```

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <cctype>
#include <utility>

// Nettoie l'entrée en enlevant la ponctuation et en convertissant en minuscules
std::string nettoyer_entree(const std::string_view texte_brut) {
    std::string texte_propre;
    for (char caractere : texte_brut) {
        if (std::isalpha(caractere)) {
            texte_propre.push_back(std::tolower(caractere));
        } else if (caractere == ' ') {
            texte_propre.push_back(caractere);
        }
    }
    return texte_propre;
}

// Divise la chaîne de caractères en mots
std::vector<std::string> diviser_en_mots(const std::string& texte) {
    std::vector<std::string> mots;
    std::string mot_temp;
    for (char caractere : texte) {
        if (caractere == ' ') {
            if (!mot_temp.empty()) {
                mots.push_back(mot_temp);
                mot_temp.clear();
            }
        } else {
            mot_temp.push_back(caractere);
        }
    }
    if (!mot_temp.empty()) {
        mots.push_back(mot_temp);
    }
    return mots;
}

// Compte la fréquence des mots sans les trier par fréquence
std::vector<std::pair<std::string, int>> compter_frequence_des_mots(const std::vector<std::string>& mots) {
    std::vector<std::pair<std::string, int>> frequence;
    for (const std::string& mot : mots) {
        bool trouve = false;
        for (auto& paire : frequence) {
            if (paire.first == mot) {
                paire.second++;
                trouve = true;
                break;
            }
        }
        if (!trouve) {
            frequence.push_back({mot, 1});
        }
    }
    return frequence;
}

// Fonction principale pour tester
int main() {
    const char* texte = "Bonjour le monde! Le monde est plein de merveilles. Explorez le monde.";
    std::string texte_nettoye = nettoyer_entree(texte);
    std::vector<std::string> mots = diviser_en_mots(texte_nettoye);
    std::vector<std::pair<std::string, int>> frequence = compter_frequence_des_mots(mots);

    for (const auto& paire : frequence) {
        std::cout << paire.first << " - " << paire.second << std::endl;
    }

    return 0;
}
```

</details>
