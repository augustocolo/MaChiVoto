![OpenElectionCompass](https://github.com/augustocolo/MaChiVoto/blob/master/public/Ma-chi-voto-open-graph.png)

Welcome to the repository for Ma Chi Voto?, a Voting Advice Application developed in partnership with [Will Media](https://willmedia.it/elezioni-politiche-2022/), a leading social-media newspaper in Italy. The website was designed to help users determine their level of agreement with each political party during the Italian general elections in September 2022. The VAA is based upon [Open Election Compass](https://github.com/open-election-compass) by Till Sanders.

## Development

Install the project and it's dependencies using the package manager of your choice:

```sh
git clone git@github.com:open-election-compass/client.git
cd client
npm ci
```

### Compile for development with HMR

```sh
npm run dev
```

### Compiles and minify for production

```sh
npm run build:demo # Build demo
npm run build:lib # Build the actual library / client
npm run build:nuxt # Build the Nuxt.js module
npm run build # runs all builds sequentially
```

### Run tests

```sh
npm run test:unit
npm run test:e2e
npm run test # run all both test suites sequentially
```

### Run linting

```sh
npm run lint # run ESLint
npm run lint:style # run Stylelint
```
