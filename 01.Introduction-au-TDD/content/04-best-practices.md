# Bonnes pratiques et conseils pour le TDD

Maintenant que vous avez vu comment implémenter le TDD étape par étape, il est essentiel de comprendre comment le pratiquer efficacement. Dans ce chapitre, nous allons explorer les bonnes pratiques et partager des conseils pour tirer le meilleur parti du TDD tout en évitant les pièges courants.

---

## Rédaction des tests : l'art de la précision

### 1. Un test = un cas précis
Chaque test doit couvrir un seul cas d'utilisation ou scénario. Cela garantit que les échecs sont faciles à diagnostiquer. Par exemple, au lieu de tester plusieurs comportements dans un seul test, divisez-les en plusieurs tests unitaires.

**Exemple :**
```typescript
test('addition de nombres positifs', () => {
  expect(addition(2, 3)).toBe(5);
});

test('addition de nombres négatifs', () => {
  expect(addition(-2, -3)).toBe(-5);
});
```
Cela vous permet de savoir précisément quelle partie de votre code pose problème en cas d'échec.

### 2. Donnez des noms explicites à vos tests
Les noms de tests doivent décrire clairement ce que vous testez. Évitez les noms vagues comme `test1` ou `fonctionnalité`, et préférez des descriptions complètes et lisibles.

**Bon exemple :**
```typescript
test('should throw an error if parameters are not numbers', () => {
  expect(() => addition(2, '3' as any)).toThrow('Les paramètres doivent être des nombres');
});
```
Des noms explicites facilitent la compréhension du comportement attendu pour d'autres développeurs ou pour vous-même, des mois plus tard.

---

## Progression : avancer étape par étape

### 1. Commencez simple
Lorsque vous démarrez une nouvelle fonctionnalité, concentrez-vous sur le cas le plus simple. Une fois ce cas validé, vous pouvez ajouter des tests pour des scénarios plus complexes.

**Exemple :** Pour un validateur de mot de passe :
1. Testez d'abord la longueur minimale.
2. Ajoutez ensuite les règles pour les majuscules.
3. Enfin, vérifiez la présence de chiffres.

Cela évite de se perdre dans des détails inutiles dès le départ et garantit une progression naturelle.

### 2. Ajoutez de la complexité progressivement
N'essayez pas de tout implémenter d'un coup. Le cycle **Red, Green, Refactor** vous encourage à construire votre fonctionnalité morceau par morceau, tout en validant chaque étape avec des tests.

---

## Itérations courtes : ne sautez pas les étapes

Le TDD repose sur une discipline stricte. Il peut être tentant de sauter une étape (par exemple, implémenter directement sans écrire de tests), mais cela va à l'encontre de la méthode.

1. **Toujours commencer par un test qui échoue (Red)** : Cela garantit que votre test est valide et pertinent.
2. **Écrivez juste assez de code pour passer le test (Green)** : Ne sur-développez pas à ce stade.
3. **Refactorisez après avoir validé vos tests** : Vous avez alors la confiance nécessaire pour améliorer votre code.

---

## Évitez le sur-test : restez pragmatique

Un piège courant pour les débutants est de vouloir tout tester. Si certains tests sont essentiels, d'autres peuvent devenir une charge inutile et ralentir le développement.

### Conseils pour éviter le sur-test :
1. **Ne testez pas ce qui appartient à des librairies externes.**
   - Exemple : Vous n'avez pas besoin de tester que `Array.prototype.map` fonctionne correctement.

2. **Concentrez-vous sur le comportement, pas sur les implémentations internes.**
   - Testez ce que votre code doit faire, et non comment il le fait. Cela rend vos tests plus résilients aux changements.

3. **Supprimez les tests obsolètes.**
   - Si un test n’est plus pertinent ou teste un cas non critique, envisagez de le retirer pour éviter des maintenances inutiles.

---

## Outils utiles pour le TDD avec TypeScript

Voici une liste d'outils qui peuvent grandement faciliter la pratique du TDD en TypeScript :

### 1. **Jest**
- **Rôle** : Framework de test complet qui permet d'écrire des tests unitaires, d'intégration et même des snapshots.
- **Pourquoi c'est intéressant** :
  - Supporte TypeScript grâce au preset `ts-jest`.
  - Rapide et facile à configurer.
  - Inclut un mode watch qui relance automatiquement les tests lors des modifications de code.

### 2. **ts-jest**
- **Rôle** : Un preset pour utiliser TypeScript avec Jest.
- **Pourquoi c'est intéressant** :
  - Permet de tester directement du code TypeScript sans transpiler en JavaScript au préalable.
  - Simplifie la configuration et l'exécution des tests TypeScript.

### 3. **ESLint**
- **Rôle** : Linter pour détecter les erreurs et garantir la cohérence du code.
- **Pourquoi c'est intéressant** :
  - Vous aide à repérer des erreurs dans votre code avant même d'écrire des tests.
  - Assure une bonne qualité de code, ce qui rend les tests plus faciles à maintenir.

### 4. **Prettier**
- **Rôle** : Outil de formatage de code.
- **Pourquoi c'est intéressant** :
  - Facilite la lecture et l’écriture du code en appliquant un style uniforme.
  - Réduit les frictions dans les revues de code.

### 5. **Mock Service Worker (MSW)**
- **Rôle** : Simule les appels réseau pour tester des fonctionnalités qui dépendent d’APIs.
- **Pourquoi c'est intéressant** :
  - Permet de tester des scénarios complexes sans dépendre d’une API réelle.
  - Réduit les temps d’exécution des tests.

### 6. **Coverage intégrée de Jest**
- **Rôle** : Fournit des rapports sur la couverture de test.
- **Pourquoi c'est intéressant** :
  - Vous aide à visualiser les parties du code qui ne sont pas couvertes par vos tests.
  - Identifie rapidement les zones à risque.

---

## Résumé des bonnes pratiques

1. **Un test = un cas précis** : Soyez clair et concis.
2. **Noms explicites** : Vos tests doivent raconter une histoire compréhensible.
3. **Itérations courtes** : Ne sautez pas les étapes du cycle **Red, Green, Refactor**.
4. **Progresser par étapes** : Commencez par des cas simples, ajoutez de la complexité progressivement.
5. **Évitez le sur-test** : Testez uniquement ce qui est nécessaire.
6. **Utilisez les bons outils** : Des outils comme Jest, ts-jest ou MSW simplifient et enrichissent votre workflow TDD.

En suivant ces bonnes pratiques et en utilisant ces outils, vous optimiserez vos tests tout en assurant la qualité et la maintenabilité de votre code.
Dans le prochain chapitre, je vais vous donner des conseils pour appliquer le TDD au quotidien et comment progresser dans le domaine.

