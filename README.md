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

# Explication :

Idea taken from ImKennyYip js :
git@github.com:ImKennyYip/2048.git -- https://github.com/ImKennyYip/2048

Building of svelteKit project :
npm init svelte@next

Launch app into the browser :
npm run dev -- --open

To build it in production :
npm run build

Routing system : 
root “/”
rép todos “/todos”

Building games routes “/games” in existant menu.

Building a component for 2048 game. 

Installing modal package

npm i svelte-simple-modal

Lifecycle component :

onMount() -> launch when the component is mounting

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

# Les avantages :

Le poids et la vitesse de chargement
Un des gros avantages du framework Svelte est, comme son nom l’indique, son poids très léger. En effet, une fois le code compilé, l’application pèse 3 à 4 fois moins qu’avec une compilation sous React ou VueJs.

un benchmark révèle que le framework est 35 fois plus rapide que React et 50 fois plus que VueJs.

En fait, Svelte veut vous permettre de réduire vos lignes de code pour que vos programmes restent lisibles. Et c’est réussi ! En moyenne, pour une fonction, le framework JavaScript aura besoin de 40% de lignes en moins que React.

Le créateur de Svelte, Rich HARRIS, explique qu’il n’a pas voulu inclure de DOM virtuel pour la simple raison que cela représentait une couche de plus à exécuter lors du chargement de l’application.

Le DOM n’est donc plus manipulé directement par l’auteur du programme, mais par le framework JavaScript directement.
