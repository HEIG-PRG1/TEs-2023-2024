# TE4

## généricité, iterators

1. Que produit ce code ?

## Fonction

```cpp
template<typename Iterator>
typename Iterator::value_type somme_elements(Iterator debut, Iterator fin) {
    typename Iterator::value_type somme = 0;
    for (Iterator it = debut; it != fin; ++it) {
        somme += *it;
    }
    return somme;
}
```

## Vectors

```cpp
std::vector<std::string> mots = {"Hello", " ", "World", "!", " Have", " a", " nice", " day!"};
```

## Appel à la fonction

```cpp
cout << somme_elements(mots.begin() + 2, mots.end() - 2);
```
<details>
<summary>Solution</summary>

```cpp
"World! Have a nice"
```

</details>


2. Que produit ce code ?

## Fonction

```cpp
template<typename Iterator>
typename Iterator::value_type somme_elements(Iterator debut, Iterator fin) {
    typename Iterator::value_type somme = 0;
    for (Iterator it = debut; it != fin; ++it) {
        somme += *it;
    }
    return somme;
}
```

## Vectors

```cpp
std::array<double, 6> temperatures = {15.5, 20.1, 23.4, 18.9, 16.7, 14.3};
```

## Appel à la fonction

```cpp
cout << somme_elements(temperatures.end() - 3, temperatures.end());
```

<details>
<summary>Solution</summary>

```cpp
49.9
```

</details>


3. Que produit ce code ?

## Fonction

```cpp
template<typename Iterator>
typename Iterator::value_type somme_elements(Iterator debut, Iterator fin) {
    typename Iterator::value_type somme = 0;
    for (Iterator it = debut; it != fin; ++it) {
        somme += *it;
    }
    return somme;
}
```

## Vectors

```cpp
vector<int> nombres_simples{10, 20, 30, 40, 50, 60};
```

## Appel à la fonction

```cpp
cout << somme_elements(nombres_simples.begin() + 2, nombres_simples.begin() + 5);
```

<details>
<summary>Solution</summary>

```cpp
120
```

</details>


## Généricité

4. Que produit ce code ?

```cpp
template <typename T>
T max_value(T a, T b) {
   return (a > b ? a : b);
}

int main() {
   unsigned int e = 5;
   char f = 'f'; 
   // la valeur ASCII de f est 102
   cout << max_value<char>(f, e) << " / " << max_value<unsigned int>(f, e);
}
```

<details>
<summary>Solution</summary>

```cpp
f / 102
```

</details>


5. Que produit ce code ?

```cpp
template <typename T>
T difference(T a, T b) {
   return (a - b);
}

int main() {
   int   x = 5;
   float y = 2.3f;
   cout << difference<int>(x, y) << " / " << difference<float>(x, y);
}
```

<details>
<summary>Solution</summary>

```
3 / 2.7
```

</details>


## Analyse de temperatures (avec iterators, avec algorithm>)

6. Considérant les déclarations suivantes et une matrice représentant les températures relevées sur une semaine :

```cpp
using Data = double;
using Serie = vector<Data>;
using Matrice = vector<Serie>;

const Matrice temperatures {
    {15.5, 20.1, 23.4, 19.0, 16.2}, // Lundi
    {17.1, 20.3, 22.2, 21.1, 18.4}, // Mardi
    {16.0, 19.5, 21.5, 20.0, 17.5}, // Mercredi
    {14.5, 18.0, 22.8, 20.5, 19.0}  // Jeudi
};
```

Écrire le code générique nécessaire afin de créer une fonction qui calcule La température maximale pour chaque jour.

La fonction doit être templatisée pour fonctionner avec n'importe quel type de données numériques et retourner un vecteur contenant les résultats pour chaque série de données.

Exemple de sortie attendue :

```
tempMaximales: [23.4, 22.2, 21.5, 22.8]
```

***Important :***

- ***Utiliser*** la librairie ``<algorithm>` dans cet exercice.
- Utiliser la généricité autant que possible afin de maximiser la réutilisation de la fonction créée.


<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using Data = double;
using Serie = std::vector<Data>;
using Matrice = std::vector<Serie>;

template <typename T>
std::vector<T> calculerMaxima(const Matrice& temperatures) {
    std::vector<T> tempMaximales;
    for (const auto& jour : temperatures) {
        auto it = std::max_element(jour.begin(), jour.end());
        tempMaximales.push_back(*it);
    }
    return tempMaximales;
}

int main() {
    const Matrice temperatures {
        {15.5, 20.1, 23.4, 19.0, 16.2},
        {17.1, 20.3, 22.2, 21.1, 18.4},
        {16.0, 19.5, 21.5, 20.0, 17.5},
        {14.5, 18.0, 22.8, 20.5, 19.0}
    };

    auto tempMaximales = calculerMaxima<Data>(temperatures);
    std::cout << "tempMaximales: ";
    for (const auto& temp : tempMaximales) {
        std::cout << temp << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

</details>


## Analyse de temperatures (avec iterators, sans algorithm>)

7. Considérant les déclarations suivantes et une matrice représentant les températures relevées sur une semaine :

```cpp
using Data = double;
using Serie = vector<Data>;
using Matrice = vector<Serie>;

const Matrice temperatures {
    {15.5, 20.1, 23.4, 19.0, 16.2}, // Lundi
    {17.1, 20.3, 22.2, 21.1, 18.4}, // Mardi
    {16.0, 19.5, 21.5, 20.0, 17.5}, // Mercredi
    {14.5, 18.0, 22.8, 20.5, 19.0}  // Jeudi
};
```

Écrire le code générique nécessaire afin de créer une fonction qui calcule La température maximale pour chaque jour.

La fonction doit être templatisée pour fonctionner avec n'importe quel type de données numériques et retourner un vecteur contenant les résultats pour chaque série de données.

Exemple de sortie attendue :

```
tempMaximales: [23.4, 22.2, 21.5, 22.8]
```

***Important :***

- ***Ne pas utiliser*** la librairie <algorithm> dans cet exercice.
- Utiliser la généricité autant que possible afin de maximiser la réutilisation de la fonction créée.



<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <vector>

using Data = double;
using Serie = std::vector<Data>;
using Matrice = std::vector<Serie>;

template <typename T>
std::vector<T> calculerMaxima(const Matrice& temperatures) {
    std::vector<T> tempMaximales;
    for (const auto& jour : temperatures) {
        T maxTemp = *jour.begin();
        for (auto it = jour.begin(); it != jour.end(); ++it) {
            if (*it > maxTemp) {
                maxTemp = *it;
            }
        }
        tempMaximales.push_back(maxTemp);
    }
    return tempMaximales;
}

int main() {
    const Matrice temperatures {
        {15.5, 20.1, 23.4, 19.0, 16.2},
        {17.1, 20.3, 22.2, 21.1, 18.4},
        {16.0, 19.5, 21.5, 20.0, 17.5},
        {14.5, 18.0, 22.8, 20.5, 19.0}
    };

    auto tempMaximales = calculerMaxima<Data>(temperatures);
    std::cout << "tempMaximales: ";
    for (const auto& temp : tempMaximales) {
        std::cout << temp << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

</details>


