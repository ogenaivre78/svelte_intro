# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm init svelte@next

# create a new project in my-app
npm init svelte@next my-app
```

> Note: the `@next` is temporary

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

Explication :

Reprise d’un repo js :
git@github.com:ImKennyYip/2048.git

Création d’un projet svelteKit :
npm init svelte@next

Lancer l’application dans un browser :
npm run dev -- --open

Pour builder l’application en production :
npm run build

Système de routing avec gesetion de l’arborescence des fichiers dans le répertoire routes
racine “/”
rép todos “/todos”

Création d’une route games “/games” intégré dans le menu de l’appli d’origine.

Création d’un composant du jeu inséré dans une section, elle même inséré dans une modale installé via un package.

svelte-simple-modal

Cycle de vie des composants :

onMount() -> permet de lancer des fonctions au chargement du composant

Les variables déclarées sont par défaut réactives au différent changement d’état au fil des réactions aux divers événements.

Déclaration d’un event system keyboard :
<svelte:window on:keydown={handleKeydown} />

Boucle sur des tableaux :
{#each board as row, r}

Balise style dans chaque composant qui permet d’avoir un css personnalisé pour ce composant uniquement

Possibilité de créer du css général

Possibilité de configurer facileement le projet avece du typescript, du tailwind, scss etc,
tout cela très bien expliqué avec la documentation svelte

Réactivité d’une variable par rapport à une autree :
$: classTile = updateTile(num);
dans le composant Tile, chaque tuile est mise à jour dynamiquement dès que lee tablea de matrice est mis à jour suite à un changement de direction

Gestion du state avec des variables locales visible uniquement dans le composant, possibilité d’exposer des variables vers les parents ou de les envoyer vers les composants enfants

possiblité de gérer un state globale dans un context, le state sera visible dans tous les composants enfants

possibilité de gérer un state visible dans toute l’application avec la création d’un store
