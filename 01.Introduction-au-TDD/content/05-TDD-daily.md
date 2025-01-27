# Implémenter le TDD au quotidien

Le **Test-Driven Development (TDD)** est une méthodologie puissante, mais l'adopter dans un projet en cours, en particulier une codebase legacy, peut sembler un défi insurmontable. Cependant, même dans un tel contexte, il est possible d'intégrer le TDD progressivement et efficacement. Ce chapitre explore les difficultés, les avantages, et propose un plan d'action concret pour surmonter ces obstacles.

---

## La réalité d’une codebase legacy

Lorsqu’on travaille sur un projet legacy, il n’est pas rare de se retrouver face à une base de code :
- Non couverte par des tests.
- Complexe, avec des dépendances peu claires.
- Écrite avec des versions obsolètes de Node.js ou des librairies dépréciées.

Ajoutez à cela un backlog chargé de **bugs à corriger** et de **features urgentes** à livrer, et le simple fait de proposer d'ajouter des tests peut sembler impossible. Personnellement, je sais à quel point cette situation peut être frustrante. La pression des délais et l'absence de tests peuvent donner l'impression que chaque modification est un saut dans le vide.

---

## Les petites actions pour un grand impact

La clé pour améliorer une codebase legacy n'est pas de tout réécrire ou de basculer immédiatement au TDD complet. Au contraire, ce sont **les petites actions régulières** qui finissent par transformer une base de code.

### Pourquoi éviter de "tout brûler" ?
1. **Le coût pour le business** : Une réécriture totale demande du temps, des ressources, et peut retarder la livraison de nouvelles fonctionnalités. Pour l'équipe technique, cela peut sembler tentant, mais le business voit rarement l'intérêt immédiat.
2. **Les risques** : Une réécriture implique de potentiellement introduire de nouveaux bugs dans un système déjà stable (même s'il est chaotique).

### Une approche équilibrée
- **Progresser par petites étapes** : Chaque bug corrigé ou fonctionnalité ajoutée peut être une opportunité pour introduire des tests.
- **Ne pas imposer le TDD de force** : Adaptez la méthodologie aux contraintes du projet et aux priorités business.
- **Communiquer sur les bénéfices** : Montrez en quoi les tests réduisent les bugs en production et accélèrent les livraisons futures.

---

## Plan d’action pour intégrer le TDD dans un projet legacy

Voici un plan concret pour améliorer progressivement une codebase legacy avec le TDD, en partant d’un projet JavaScript utilisant une vieille version de Node.js :

### 1. **Diagnostiquer l’état du projet**
- Identifiez les zones critiques et fréquemment modifiées du code.
- Notez les parties les plus complexes ou risquées, car elles bénéficieront le plus des tests.
- Vérifiez quelles versions de Node.js et des librairies sont utilisées. Si elles sont trop anciennes, planifiez des mises à jour progressives.

### 2. **Configurer un environnement minimal pour les tests**
Même avec une version obsolète de Node.js, vous pouvez souvent introduire un framework de test moderne comme **Mocha**, **Jest** ou **Vitest**.

#### Étapes :
1. Installez une librairie compatible avec votre version de Node.js (exemple : Mocha pour les environnements plus anciens).
   ```bash
   npm install --save-dev mocha chai
   ```
2. Créez un dossier pour vos tests :
   ```bash
   mkdir tests
   ```
3. Configurez un script de test dans `package.json` :
   ```json
   {
     "scripts": {
       "test": "mocha tests/**/*.js"
     }
   }
   ```

### 3. **Introduire des tests unitaires progressivement**
- **Focus sur les "opportunités"** : Chaque fois que vous travaillez sur un bug ou une nouvelle fonctionnalité, écrivez des tests avant de modifier le code existant.
- **Débuter par les cas simples** : Testez les fonctions pures ou les utilitaires avant d'aborder les parties plus complexes.

#### Exemple : Ajouter un test pour une fonction utilitaire existante
Fichier : `utils.js`
```javascript
function add(a, b) {
  return a + b;
}
module.exports = { add };
```

Test : `tests/utils.test.js`
```javascript
const { add } = require('../utils');
const { expect } = require('chai');

describe('add', () => {
  it('should return the sum of two numbers', () => {
    expect(add(2, 3)).to.equal(5);
  });
});
```

### 4. **Écrire des tests pour les zones critiques**
- Identifiez les fonctions ou modules les plus utilisés ou les plus risqués.
- Ajoutez des tests pour ces zones afin de sécuriser vos prochaines modifications.

### 5. **Automatiser progressivement**
- Configurez des tests à exécuter automatiquement lors des commits grâce à des outils comme **Husky**.
- Intégrez les tests dans une pipeline CI/CD si possible (par exemple avec GitHub Actions).

### 6. **Former et impliquer l’équipe**
- Partagez votre approche avec vos collègues.
- Organisez des sessions pour montrer les bénéfices concrets des tests : moins de stress, moins de bugs, meilleure collaboration.
- Encouragez l'équipe à suivre une démarche similaire sur leurs tâches.

---

## Pourquoi le TDD aide aussi le business

Pour les équipes techniques, les avantages du TDD sont clairs : un code plus fiable, plus maintenable et moins de régressions. Mais pour le business, ces bénéfices doivent être traduits en **valeur métier** :

1. **Réduction des bugs en production** : Moins de temps passé à corriger des problèmes critiques signifie plus de temps pour livrer de nouvelles fonctionnalités.
2. **Livraisons plus rapides** : Avec des tests automatisés, les changements peuvent être déployés avec plus de confiance et moins d'approbations manuelles.
3. **Coût total réduit** : Un code plus fiable coûte moins cher à maintenir sur le long terme.

---

## Résumé

Adopter le TDD dans un projet legacy peut sembler difficile, mais c'est faisable grâce à des actions régulières et progressives :
- **Diagnostiquez l’état actuel** et commencez par les zones critiques.
- **Ajoutez des tests progressivement**, en vous concentrant sur les nouvelles fonctionnalités et les bugs.
- **Impliquez l'équipe** et montrez les bénéfices concrets pour réduire les résistances.

DAns le prochain chapitre, nous conclurons ce tutoriel et je vous donnerais des astuces et des ressources pour aller plus loin.

