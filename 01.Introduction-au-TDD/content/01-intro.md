# Introduction au Test-Driven Development (TDD)

Le Test-Driven Development (TDD) est une approche de développement logiciel qui consiste à écrire les tests avant le code de production. Cette méthode, popularisée par Kent Beck, fait partie intégrante des pratiques du Clean Code et de l'Extreme Programming.

## Les trois lois du TDD

1. **Première loi** : Vous ne devez pas écrire de code de production avant d'avoir écrit un test unitaire qui échoue.
2. **Deuxième loi** : Vous ne devez pas écrire plus de tests unitaires qu'il n'en faut pour faire échouer le test - l'impossibilité de compiler est un échec.
3. **Troisième loi** : Vous ne devez pas écrire plus de code de production qu'il n'en faut pour faire passer le test qui échoue.

## Le cycle Red-Green-Refactor

Le TDD suit un cycle simple mais puissant :

### 🔴 Red
- Écrire un test qui échoue
- Le test doit échouer pour une bonne raison
- Vérifier que le test échoue comme prévu

### 💚 Green
- Écrire le minimum de code pour faire passer le test
- Ne pas se soucier de l'élégance du code à ce stade
- Vérifier que tous les tests passent

### 🔄 Refactor
- Améliorer le code sans changer son comportement
- S'assurer que tous les tests continuent de passer
- Éliminer la duplication et améliorer la lisibilité

## Avantages du TDD

1. **Design orienté utilisateur** : En écrivant d'abord les tests, vous vous concentrez sur l'interface et l'utilisation de votre code.
2. **Code plus propre** : Le TDD vous pousse naturellement vers un code modulaire et faiblement couplé.
3. **Documentation vivante** : Les tests servent de documentation toujours à jour sur le comportement attendu du code.
4. **Confiance** : Une suite de tests complète vous permet de refactorer sans crainte.

## Dans le prochain chapitre...

Nous allons mettre en pratique ces concepts en développant une fonction simple en suivant l'approche TDD. Vous verrez comment le cycle Red-Green-Refactor s'applique concrètement.
