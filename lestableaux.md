
# Les tableaux

## Déclaration d'un tableau et allocation de mémoire

Les tableaux sont des types **référence**.

### Déclaration d'un tableau
```csharp
Type[] nomTab; // nomTab fait référence à un tableau
```

### Allocation de l'espace mémoire d'un tableau
```csharp
nomTab = new Type[Taille]; // Taille indique le nombre d'éléments
```

**Exemple :**
```csharp
string[] prenoms; // Déclaration d'un tableau de string
prenoms = new string[3]; // Le tableau contient 3 éléments
```

**Note :** Pour récupérer la taille du tableau, utilisez `nomTab.Length`.

## Déclaration, allocation et initialisation de valeur

Il est possible de déclarer et allouer l'espace en même temps :
```csharp
Type[] NomTab = new Type[Taille];
```

**Exemple :**
```csharp
string[] prenoms = new string[3];
```

Une fois le tableau déclaré, nous pouvons initialiser ses valeurs (insertion) :
```csharp
prenoms[0] = "Titi"; // On commence à l'index 0
prenoms[1] = "Tata";
prenoms[2] = "Toto"; // Dernier index : Length-1
```

Il est aussi possible de déclarer, allouer et initialiser en même temps :
```csharp
float[] valeurs = new float[] {2.5f, 0.3f, 5.9f};
```
ou simplement :
```csharp
float[] valeurs = {2.5f, 0.3f, 5.9f};
```

## Tableaux avec des cellules de types différents

Il est possible de créer des tableaux ayant des cellules de types différents. Le type de base de ces tableaux doit être `object`.

Une cellule de type `object` peut recevoir une valeur de n'importe quel type :
```csharp
object[] tab = new object[3];
tab[0] = 12;
tab[1] = 1.2;
tab[2] = "Message";
```

## La libération mémoire d'un tableau

La libération mémoire d'un tableau se fait automatiquement par le ramasse-miettes (Garbage Collector).

Un tableau cesse d'exister :
- Lorsqu'on quitte le bloc dans lequel il est déclaré.
- Lorsqu'on assigne une nouvelle valeur (y compris `null`) à la variable référence qui désigne le tableau.

**Exemple :**
```csharp
float[] reels = {2.5f, 0.3f, 5.9f};
reels = new float[] {3.9f, 1.256f, 425.68f};
reels = null;
```

## La copie d'un tableau

La copie d'un tableau est en fait une copie de sa référence.

**Exemple :**
```csharp
int[] t1 = {2, 3, 4};
int[] t2; // t2 contient la valeur « null »
t2 = t1; // t1 et t2 font référence au même tableau
```

Ainsi, si vous modifiez la première valeur de `t1` :
```csharp
t1[0] = 5;
```

La valeur de `t2` sera maintenant `{5, 3, 4}`. Nos deux variables permettent d'accéder au même contenu.

### Exemple avec deux tableaux de tailles différentes
```csharp
int[] t1 = {2, 3, 4};
int[] t2 = new int[100];
t2 = t1; // t1 et t2 font référence au même tableau
```

Dans ce cas, `t2` fait référence à la zone mémoire contenant le tableau de trois éléments, et la zone mémoire contenant les 100 cellules est signalée comme "à libérer". Le ramasse-miettes (Garbage Collector) la libérera lorsque nécessaire.

## Faire une véritable copie d'un tableau

Pour faire une véritable copie d'un tableau, il existe deux méthodes :
- La méthode `CopyTo()`
- La méthode `Clone()`

### La copie d'un tableau avec la méthode `CopyTo()`

```csharp
int[] t1 = {2, 3, 4};
int[] t2 = new int[10]; // Toutes les valeurs de t2 sont à 0 par défaut
t1.CopyTo(t2, 0); // Fais la copie à partir de l'index 0
```

Après la copie, `t1` contient `{2, 3, 4}` et `t2` contient `{2, 3, 4, 0, 0, 0, 0, 0, 0, 0}`.

### La copie d'un tableau avec la méthode `Clone()`

```csharp
int[] t1 = {2, 3, 4};
int[] t2; // t2 = null
t2 = (int[])t1.Clone(); // Fais la copie de t1 dans t2
t1[0] = 100;
```

Après la copie, nous avons deux tableaux distincts :
- `t1 = {100, 3, 4}`
- `t2 = {2, 3, 4}`

## Les listes (List)

Il existe en C# une classe nommée `List` dont l'utilisation est similaire aux tableaux mais plus simple. Les listes sont des conteneurs dynamiques, ce qui élimine la notion de taille fixe des tableaux.

- **Count** permet de connaître le nombre d'éléments actuels dans la liste (pas de `Length`).
- Les méthodes **Add**, **Remove**, **RemoveAt** et **Clear** permettent d'ajouter et supprimer des éléments.

Une liste est une **classe générique** (une collection), ce qui signifie qu'elle peut contenir différents types d'éléments.

**Exemple d'utilisation :**
```csharp
List<string> mesChaines = new List<string>() {
    "chaine1", "chaine2", "chaine2", "chaine3", "chaine4", "chaine5"
};

mesChaines.Remove("chaine2");
mesChaines.RemoveAt(0);
mesChaines.Add("chaine6");

foreach (string item in mesChaines) {
    Console.WriteLine(item);
}

mesChaines.Clear();
```

## Les Tuples

Le **tuple** permet de regrouper des données de types différents. C'est ce qu'on appelle du **packing**.

Pour le définir, on met plusieurs types entre parenthèses :
```csharp
(double, int, string) t1 = (4.5, 3, "test");
```

Contrairement aux listes et tableaux, les données d'un tuple sont **non modifiables** et identifiées par des noms (par défaut `ItemX`). Il est possible de renommer les éléments du tuple :
```csharp
(double MonDouble, int MonInt, string MonString) t2 = t1;
```

### Exemple de Tuple

```csharp
// Affectation (packing)
(double, int, string) t10 = (4.5, 3, "test");

// Autre notation :
ValueTuple<double, int, string> t1 = (4.5, 3, "test");

Console.WriteLine($"Tuple with elements {t1.Item1} and {t1.Item2}.");
Console.WriteLine(t1.Item3);

// Unpacking
(double monDouble, int monInt, string monString) = t1;
var (monDouble2, monInt2, monString2) = t1;

// Renommage
(double MonDouble, int MonInt, string MonString) t2 = t1;
Console.WriteLine($"Tuple with elements {t2.MonDouble} and {t2.MonInt}.");
Console.WriteLine(t2.Item3);
Console.WriteLine(t2.MonString);
```


