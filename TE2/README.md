# TE2

## Type? Valeur? Affichage?

1. Littéraux constants

Pour la ligne de code suivante, sélectionnez l’option qui correspond à son type, sa valeur, ce qu'elle affiche

On suppose que le compilateur utilise le modèle de donnée ``LLP64``, i.e, avec ``int`` et ``long`` codés sur 32 bits et ``long long`` sur 64

```cpp
auto v = 10'0'0000'000'00; 
cout << v << endl;
```

<details>
<summary>Solution</summary>

long long int, 100000000000, 100000000000

</details>


2. Pour la ligne de code suivante, sélectionnez l’option qui correspond à son type, sa valeur, ce qu'elle affiche.

On suppose que le compilateur utilise le modèle de donnée ``LLP64``, i.e, avec ``int`` et ``long`` codés sur 32 bits et ``long long`` sur 64

```cpp
auto v = 0x12AL; 
cout << v << endl;
```

<details>
<summary>Solution</summary>

long int, 298, 298

</details>


3. Pour la ligne de code suivante, sélectionnez l’option qui correspond à son type, sa valeur, ce qu'elle affiche.

On suppose que le compilateur utilise le modèle de donnée ``LLP64``, i.e, avec ``int`` et ``long`` codés sur 32 bits et ``long long`` sur 64

```cpp
auto v = 0xaeg; 
cout << v << endl;
```

<details>

Ne compile pas

<summary>Solution</summary>

</details>

## Flux

4. Fichiers input/output

Modifiez le programme en C++ du template pour faire ce qui suit :

* Lire de la console un nom de fichier d'entrée et sortie (aucun message n'est fourni à l'utilisateur)
* Si le fichier entrée n'existe pas, afficher le message "Error d'ouverture du fichier : nom_du_fichier" et arrêter l'exécution
* Lire le contenu du fichier entrée, s'il existe
* Créer un nouveau fichier de sortie avec le nom donné. Si le fichier existe, écraser son contenu.
* Parcourir le fichier d'entrée pour convertir le text à majuscules. Sauver le text dans le fichier sortie
* Parcourir le fichier de sortie et afficher le contenu à la console ligne par ligne.

Exemple d'execution (le fichier input est déjà fourni):

```cpp
/src/input.txt
/src/output.txt
HELLO
WORLD
THIS
IS
TE2
```

```cpp
/src/main.cpp

#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::string inputFileName, outputFileName;

    // Lire les noms de fichiers de la console
    
    
    // Vérifier que le fichier entrée existe


    std::string line;
    while (std::getline(file, line)) {
        std::cout << line << std::endl;
    }

    file.close();
    return 0;
}
```

```
/src/input.txt

hello
world
this
is
te2
```

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <cctype> // For toupper function

int main() {
    std::string inputFileName, outputFileName;

    // Ask user for file names
    //std::cout << "Enter the name of the input file: ";
    std::getline(std::cin, inputFileName);
    // std::cout << "Enter the name of the output file: ";
    std::getline(std::cin, outputFileName);

    // Check if input file exists
    std::ifstream inputFile(inputFileName);
    if (!inputFile.is_open()) {
        std::cerr << "Error d'ouverture du fichier : " << inputFileName;
        return 1;
    }

    // Open output file
    std::ofstream outputFile(outputFileName);

    std::string line;
    while (std::getline(inputFile, line)) {
        // Convert each character in line to uppercase
        for (char &ch : line) {
            ch = std::toupper(ch);
        }
        outputFile << line << std::endl;
    }

    inputFile.close();
    outputFile.close();

    // Reopen the output file for reading
    std::ifstream outputRead(outputFileName);
    while (std::getline(outputRead, line)) {
        std::cout << line << std::endl; // Print each line to the console
    }
    outputRead.close();

    return 0;
}
```

</details>



## Types arithmétiques

5. Analyse d'un Nombre à Virgule Flottante

Écrivez un programme en C++ qui réalise les tâches suivantes :

* Lire de la console un nombre à virgule flottante sand donner un message à l'utilisateur (vous pouvez supposer que le nombre sera en notation décimale standard).
* Afficher les composants suivants du nombre saisi :
	* Le signe du nombre exprimé en text (Positif ou Négatif).
	* La mantisse normalisée en base 10.
	* L'exposant en base 10, en supposant que le nombre est exprimé en notation scientifique (par exemple, pour ``123.45``, la notation scientifique est ``1.2345 x 10^2``, donc l'exposant est 2).

Exemple d'execution pour une entrée ``314.59``

```
314.59
Signe: Positif
Mantisse normalisée en base 10: 3.1459
Exposant en base 10: 2
```


```cpp
#include <iostream>
#include <cmath>
#include <string>

int main() {
    double number;
    
    std::cin >> number;

    // Vérifier le signe


    // Calculer la mantisse normalisée en base 10


    // Calculer l'exposant en base 10

    
    // Imprimer résultats
    std::cout << "Signe: " << sign << std::endl;  //retourne Positif ou Negatif
    std::cout << "Mantisse normalisée en base 10: " << mantissa << std::endl;
    std::cout << "Exposant en base 10: " << exponent << std::endl;

    return 0;
}
```

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <cmath>
#include <string>

int main() {
    double number;
    //std::cout << "Entrez un nombre à virgule flottante: ";
    std::cin >> number;

    // Check the sign of the number
    std::string sign = (number >= 0) ? "Positif" : "Négatif";

    // Get the absolute value for mantissa and exponent calculation
    double absNumber = std::abs(number);

    // Calculate mantissa and exponent for scientific notation
    int exponent = (absNumber != 0) ? static_cast<int>(std::floor(std::log10(absNumber))) : 0;
    double mantissa = absNumber / std::pow(10.0, exponent);

    // Display results
    std::cout << "Signe: " << sign << std::endl;
    std::cout << "Mantisse normalisée en base 10: " << mantissa << std::endl;
    std::cout << "Exposant en base 10: " << exponent << std::endl;

    return 0;
}
```

</details>


## Struct, Enum

6. Système de Gestion de Bibliothèque

Écrivez un programme en C++ pour simuler un système de gestion de bibliothèque simple. Votre programme doit utiliser struct et enum pour réaliser les tâches suivantes :

* Information sur le Livre (struct) :

	* Créez une struct nommée Livre avec les champs suivants : titre (string), auteur (string), langue (string) et annee (entier).

* Statut du Livre (enum) :

	* Définissez un enum nommé StatutLivre avec les valeurs possibles suivantes : DISPONIBLE, EMPRUNTE, RESERVE.

* Fonctionnalité du Programme :

	* Votre programme doit permettre la lecture d'un nouveau livre depuis la console en entrant les paramètres dans l'ordre suivant :
	
		* titre
		* auteur
		* langue
		* annee
		* statut

	* Ensuite, le programme imprime les informations du Livre dans la console comme ceci (les valeurs sont lues à partir des différentes structures) :

		* Titre du Livre :
		* Auteur du Livre :
		* Langue du Livre :
		* Année du Livre :
		* Statut :

Exemple d'execution :

```
Entrez le titre du livre: Cien Años de Soledad
Entrez l'auteur du livre Entrez la langue du livre: Grabriel Garcia Marquez
Entrez l'année du livre: 1965
Entrez le statut du livre (0 pour DISPONIBLE, 1 pour EMPRUNTE, 2 pour RESERVE): 2
Titre du Livre : Cien Años de Soledad
Auteur du Livre : Grabriel Garcia Marquez
Langue du Livre : Español
Année du Livre : 1965
Statut : EMPRUNTE
```


```cpp
#include <iostream>
#include <string>
#include <utility>

// Définition de la structure Livre


// Définition de l'enum StatutLivre


int main() {

    // Lecture des informations du livre - compléter les variables qui correspondent aux structures de données 
    std::cout << "Entrez le titre du livre: ";
    std::getline(std::cin, ???);
    std::cout << "Entrez l'auteur du livre: ";
    std::getline(std::cin, ???);
    std::cout << "Entrez la langue du livre: ";
    std::getline(std::cin, ???);
    std::cout << "Entrez l'année du livre: ";
    std::cin >> ???;
    std::cout << "Entrez le statut du livre (1 pour DISPONIBLE, 2 pour EMPRUNTE, 3 pour RESERVE): ";
    std::cin >> ???;
    
    // Affichage des informations du livre - compléter les variables correctes
    std::cout << "Titre du Livre : " << ??? << std::endl;
    std::cout << "Auteur du Livre : " << ??? << std::endl;
    std::cout << "Langue du Livre : " << ??? << std::endl;
    std::cout << "Année du Livre : " << ??? << std::endl;
    std::cout << "Statut : ";
    // Rajouter la logique pour afficher DISPONIBLE ou EMPRUNTE ou RESERVE
    std::cout << std::endl;

    return 0;
}
```

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
#include <utility>

// Définition de la structure Livre
struct Livre {
    std::string titre;
    std::string auteur;
    std::string langue;
    int annee;
};

// Définition de l'enum StatutLivre
enum StatutLivre { DISPONIBLE=1, EMPRUNTE, RESERVE };

// Fonction principale
int main() {
    Livre nouveauLivre;
    StatutLivre statutLivre;
    int statut;

    // Lecture des informations du livre
    std::cout << "Entrez le titre du livre: ";
    std::getline(std::cin, nouveauLivre.titre);
    std::cout << "Entrez l'auteur du livre: ";
    std::getline(std::cin, nouveauLivre.auteur);
    std::cout << "Entrez la langue du livre: ";
    std::getline(std::cin, nouveauLivre.langue);
    std::cout << "Entrez l'année du livre: ";
    std::cin >> nouveauLivre.annee;
    std::cout << "Entrez le statut du livre (1 pour DISPONIBLE, 2 pour EMPRUNTE, 3 pour RESERVE): ";
    std::cin >> statut;
    statutLivre = static_cast<StatutLivre>(statut);

    // Affichage des informations du livre
    std::cout << "Titre du Livre : " << nouveauLivre.titre << std::endl;
    std::cout << "Auteur du Livre : " << nouveauLivre.auteur << std::endl;
    std::cout << "Langue du Livre : " << nouveauLivre.langue << std::endl;
    std::cout << "Année du Livre : " << nouveauLivre.annee << std::endl;
    std::cout << "Statut : ";
    switch (statutLivre) {
        case DISPONIBLE: std::cout << "DISPONIBLE"; break;
        case EMPRUNTE: std::cout << "EMPRUNTE"; break;
        case RESERVE: std::cout << "RESERVE"; break;
    }
    std::cout << std::endl;

    return 0;
}
```

</details>