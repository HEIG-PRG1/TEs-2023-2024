# TE1

## 1. Qu'affichent les codes suivants ? 

1.1

```cpp
cout << 4 / 5 * 5. / 3. << " "
<< ( 5 / 3 ) * ( 3.0 / 2 ) << " "
<< 7. / 2. * 2 / 7;
```

<details>
<summary>Solution</summary>

```cpp
0  1.5  1
```

</details>

1.2

```cpp
int result = 0;
for (int a = 1; a <= 2; ++a) {
    for (int b = 0; b < a; ++b) {
        result += a;
    }
}
cout << result;
```

<details>
<summary>Solution</summary>

```cpp
5
```

</details>

1.3

```cpp
int x = 8, y = 12;
int outcome = ( x > y ) ? x + y : y - x;
cout << outcome;
```

<details>
<summary>Solution</summary>

```cpp
4
```

</details>

1.4

```cpp
int i = 5;
do {
    cout << i << " ";
    i++;
} while (i < 5);
```

<details>
<summary>Solution</summary>

```cpp
5
```

</details>

1.5

```cpp
int i = 5;
while (i < 5) {
    cout << i << " ";
    i++;
}

```

<details>
<summary>Solution</summary>

```cpp
pas de sortie
```

</details>

1.6

```cpp
#include <iostream>
using namespace std;

bool increment(int& k) {
    k++;
    return true;
}

int main() {
    int m = 0;
    bool result = 4 > 2 || increment(m);
    cout << result << " " << m;
    return 0;
}
```

<details>
<summary>Solution</summary>

```cpp
1 0
```

</details>

1.7

```cpp
for (int j = 1; j < 10; ++j) {
    switch (j) {
        case 1: cout << "W";
        case 2: cout << "X"; break;
        case 3: cout << "Y";
        default: cout << "Z";
    }
cout << "-";
}
```

<details>
<summary>Solution</summary>

```cpp
WX-X-YZ-Z-Z-Z-Z-Z-Z-
```

</details>

1.8

```cpp
string str;
int i = 0;
for (char c = 'D'; c >= 'B'; c--) {
    str = (c+i) + str;
    i++;
}
cout << str;
```

<details>
<summary>Solution</summary>

```cpp
DDD
```

</details>


## De quels types sont les expressions suivantes ?

2.1

```cpp
'B' - 3
```
<details>
<summary>Solution</summary>

```cpp
int
```

</details>


2.2

```cpp
'X' / 2.5
```
<details>
<summary>Solution</summary>

```cpp
double
```

</details>

2.3

```cpp
3.5 + 7
```
<details>
<summary>Solution</summary>

```cpp
double
```

</details>

2.4

```cpp
7 != 7.0
```
<details>
<summary>Solution</summary>

```cpp
bool
```

</details>

2.5

```cpp
3 > 2 && 4 < 5
```
<details>
<summary>Solution</summary>

```cpp
bool
```

</details>


## 3. Indiquez avec "oui" ou "non" si les codes suivants compilent

3.1

```cpp
int a = 10;
const int* p1 = &a;
*p1 = 20;
```
<details>
<summary>Solution</summary>

Non : ne devrait pas compiler car on ne peut pas modifier une valeur à travers un pointeur vers un const.

</details>

3.2

```cpp
const int b = 15;
const int* p2 = &b;
```
<details>
<summary>Solution</summary>

Oui

</details>


3.3

```cpp
int d = 30;
int* const p3 = &d;
int e = 40;
p3 = &e;
```
<details>
<summary>Solution</summary>

Non : ne devrait pas compiler car p3 est un pointeur constant et son adresse ne peut pas être changée.

</details>

3.4

```cpp
const int f = 50;
int* p4 = &f;
```
<details>
<summary>Solution</summary>

Non : ne devrait pas compiler car on ne peut pas pointer un pointeur int vers une mémoire immuable.

</details>

3.5

```cpp
int j = 80;
const int* k = &j;
k = nullptr;
```
<details>
<summary>Solution</summary>

Oui : compile. Le pointeur pointe vers un int const, mais le pointeur lui-même n'est pas constant.

</details>


## Les 4 saisons

Complétez le programme ci-dessous pour qu'il affiche la saison (retournée par une fonction) sur la base du numéro de mois saisi par l'utilisateur. La fonction doit être spécifiée après main. Le mois est saisi sous forme de nombre entre 1 et 12 et le programme affiche :

* "hiver" si le mois est dans l'intervalle [12, 2],
* "printemps" si le mois est dans l'intervalle [3, 5],
* "été" si le mois est dans l'intervalle [6, 8],
* "automne" si le mois est dans l'intervalle [9, 11],
* et "mois invalide" pour les valeurs hors de ces plages.

On suppose que l’utilisateur saisit uniquement des entiers.

Avec ``if`` :

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

// Function specification after main
string getSeason(int mois);

int main() {
    int mois = 0;
    cin >> mois;

    cout << getSeason(mois);
    return EXIT_SUCCESS;
}

string getSeason(int mois) {
    if( mois == 12 || mois <= 2 ){
        return "hiver";
    }else if( mois <= 5 ){
        return "printemps";
    }else if( mois <= 8 ){
        return "été";
    }else if( mois <= 11 ){
        return "automne";
    }else{
        return "mois invalide";
    }
}
```
</details>

Avec ``switch` :

<details>
<summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

// Function specification after main
string getSeason(int mois);

int main() {
    int mois = 0;
    cin >> mois;

    cout << getSeason(mois);
    return EXIT_SUCCESS;
}

string getSeason(int mois) {
    switch (mois) {
        case 12:
        case 1:
        case 2:
            return "hiver";
        case 3:
        case 4:
        case 5:
            return "printemps";
        case 6:
        case 7:
        case 8:
            return "été";
        case 9:
        case 10:
        case 11:
            return "automne";
        default:
            return "mois invalide";
    }
}
```
</details>
