# Implémentation concrète du TDD en TypeScript

Dans ce chapitre, nous allons mettre en pratique les concepts de **Test-Driven Development (TDD)** en utilisant **TypeScript**. Nous couvrirons les étapes nécessaires pour configurer un projet TDD-ready, puis détaillerons chaque étape du cycle **Red, Green, Refactor** à travers des exemples clairs et précis.

---

## Préparer un projet TDD-ready

Avant de commencer, nous devons configurer un environnement de développement adapté pour pratiquer le TDD en TypeScript.

### 1. Installer les librairies nécessaires
Voici les outils et dépendances dont nous aurons besoin :
- **TypeScript** : Le langage principal.
- **Jest** : Un framework de test populaire.
- **ts-jest** : Un preset qui permet à Jest de comprendre TypeScript.
- **eslint** et **prettier** : Pour garantir une bonne qualité de code.

#### Commande pour installer les dépendances :
```bash
npm install --save-dev typescript jest ts-jest @types/jest eslint prettier
```

### 2. Initialiser le projet
Créez un nouveau projet Node.js et configurez les fichiers nécessaires.

#### Étape 1 : Initialiser le projet Node.js
```bash
npm init -y
```

#### Étape 2 : Configurer TypeScript
Générez un fichier `tsconfig.json` :
```bash
ts-jest config:init
```
Assurez-vous que votre `tsconfig.json` inclut les chemins suivants pour Jest :
```json
{
  "compilerOptions": {
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true
  }
}
```

#### Étape 3 : Configurer Jest
Ajoutez un fichier de configuration Jest `jest.config.js` :
```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
};
```

### 3. Structurer les fichiers
Adoptez une architecture claire :
```
.
├── src/
│   ├── index.ts
│   ├── __tests__/
│   │   └── example.test.ts
├── jest.config.js
├── package.json
├── tsconfig.json
```
- **src/** : Contient le code source.
- **__tests__/** : Contient les fichiers de tests.
- Les fichiers de tests suivent la convention : `*.test.ts`.

---

## Étape 1 : Le Red

La première étape du cycle TDD consiste à écrire un test qui échoue. L'objectif est de formaliser ce que la fonctionnalité est censée faire avant même de commencer à l'implémenter. Ce test met en lumière les attentes et les cas d'erreurs éventuels.

### Pourquoi c'est important
Commencer par le test permet de :
- Définir clairement le comportement attendu.
- Identifier les cas limites dès le départ.
- Se concentrer uniquement sur ce qui est nécessaire.

Imaginons que nous souhaitions implémenter une fonction `addition(a, b)` qui retourne la somme de deux nombres.

#### Test initial (échec attendu) :
Dans `src/__tests__/example.test.ts` :
```typescript
test('addition de deux nombres', () => {
  const result = addition(2, 3);
  expect(result).toBe(5);
});
```

Quand vous exécutez les tests :
```bash
npm test
```
Le test échoue car la fonction `addition` n'existe pas encore.

---

## Étape 2 : Le Green

Dans cette étape, nous écrivons le code minimum pour que le test passe. L'idée est de se concentrer sur la solution la plus simple possible.

Cette approche évite de sur-développer et garantit que chaque fonctionnalité répond directement aux besoins définis par les tests.

Dans `src/index.ts`, implémentons la fonction `addition` :
```typescript
export function addition(a: number, b: number): number {
  return a + b;
}
```

Modifions ensuite le test pour importer la fonction :
```typescript
import { addition } from '../index';

test('addition de deux nombres', () => {
  const result = addition(2, 3);
  expect(result).toBe(5);
});
```
Quand vous relancez les tests, ils passent avec succès.

---

## Étape 3 : Le Refactoring

Le refactoring consiste à améliorer la qualité et la lisibilité du code sans modifier son comportement. Les tests garantissent que le code fonctionne toujours après ces modifications.

Le refactoring permet d'améliorer la maintenabilité du code et de réduire la dette technique.

### Exemple
Nous pourrions ajouter une vérification supplémentaire pour s'assurer que les paramètres sont des nombres :
```typescript
export function addition(a: number, b: number): number {
  if (typeof a !== 'number' || typeof b !== 'number') {
    throw new Error('Les paramètres doivent être des nombres');
  }
  return a + b;
}
```

Ajoutons un test pour valider ce cas :
```typescript
test('lance une erreur si les paramètres ne sont pas des nombres', () => {
  expect(() => addition(2, '3' as any)).toThrow('Les paramètres doivent être des nombres');
});
```

---

## Résumé et exemple final

Dans ce chapitre, nous avons :
- Préparé un projet TypeScript pour le TDD.
- Suivi le cycle **Red, Green, Refactor** pour implémenter une fonction simple.

### Exemple complet
Voici à quoi ressemble notre projet final :

#### `src/index.ts`
```typescript
export function addition(a: number, b: number): number {
  if (typeof a !== 'number' || typeof b !== 'number') {
    throw new Error('Les paramètres doivent être des nombres');
  }
  return a + b;
}
```

#### `src/__tests__/example.test.ts`
```typescript
import { addition } from '../index';

test('addition de deux nombres', () => {
  const result = addition(2, 3);
  expect(result).toBe(5);
});

test('lance une erreur si les paramètres ne sont pas des nombres', () => {
  expect(() => addition(2, '3' as any)).toThrow('Les paramètres doivent être des nombres');
});
```

Maintenant que vous savez comment implémenter des tests simples avec Typescript, nous allons voir quelques bonnes pratiques en TDD qui vous permettront d'écrire du code toujours plus robuste.