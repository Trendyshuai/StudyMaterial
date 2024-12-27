# React Tips

## 1.Install nvm
Switch between different nodejs versions.

[Download website.](https://github.com/coreybutler/nvm-windows/releases/)

## 2.Configure proxy and mirror

In order to download fast.

Config file in <u>C:\Users\\**USERNAME**\AppData\Roaming\nvm\setting.txt</u>

Append this text in setting.txt file:

```
node_mirror: https://npmmirror.com/mirrors/node/
npm_mirror: https://npmmirror.com/mirrors/npm/
```

## 3.Install Nodejs

* Install Nodejs

```powershell
nvm install [version]
```
-version:

`latest` is the latest version of Nodejs.

`lts` is the latest stable version of Nodejs.

`22.5.0` is specified verison.

* Use Nodejs

```powershell
nvm use [version]
```

## 4.Configure proxy and mirror of NPM

Config file in <u>C:\Users\\**USERNAME**\\.npmrc</u>

```
registry=https://registry.npmmirror.com
```

If you used the proxy of company.

you need append this text in .npmrc

```
strict-ssl=false
proxy=http://USERNAME:PASSWORD@PROXY-DOMAIN.com:PORT/
```
`Tips:`

## 5.Create React framework

* create react framework use vite.

```
npm create Vite@latest hello-world -- --template react
```

* install dependency

```
cd hello-world
npm install
```

* run react

```
npm run dev
```

