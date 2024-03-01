### NPM

Versioning
major.minor.patch
express 4.17.3

Manual package update

```bash
npm outdated
npm update
```

Automatic minor/patch update

```bash
express ^4.17.3
caret updates minor

express ~4.17.3
tiled updates patch
```

npm - how to list outdated global packages
```
npm outdated -g
```


npm - how to update all global packages
```
npm update -g
```

npm - how to update a specific global package
```
npm update -g <package name>
```

How to update all global packages to the latest version:
```
npx npm-check --global --update-all
```
