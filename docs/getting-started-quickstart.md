# Quickstart

1) Get Bük
> ##### Github

> Version controlling your documents

* If you need to version control your documents, we recommend you to [fork](https://help.github.com/articles/fork-a-repo/) this repository and then sync it whenever a new release becomes available.
* Or you can also simply change the remote after creating an empty repo on your github account: 
```shell
git clone https://github.com/hang-up/buk.git buk
cd buk
npm install
git remote set-url origin https://github.com/YOUR OWN USER NAME/buk.git
```

> ##### NPM
Bük is also available on NPM. However, in the current state, it cannot be considered as a 'dependency' per se. As such, you will need to extract it from `/node_modules` after installing from NPM.

```shell
npm install buuk

# move buuk out of node_modules
mv node_modules/buuk . && cd buuk  && npm install

# change remote if version control is needed
git remote set-url origin https://github.com/YOUR OWN USER NAME/buk.git
```
---

2) Drop your markdown files in `docs`.
3) Update `manifest.json`
4) `npm run build`

**Refer to Usage/manifest.json to learn more about file naming conventions.** 

---
## Scripts

```
 npm run dev
```
Will serve a local version of Bük on `localhost:8080` with hot module replacement (HMR) + dev friendly errors output.

```
 npm run build
```
Will compile all markdown files referenced inside the manifest and output optimized assets in `dist`.
Serve from this folder if need be.