# [![Misskey](https://github.com/syuilo/misskey/blob/master/assets/title.png?raw=true)](https://github.com/syuilo/misskey) on [![Aiko](/assets/logo.png)](https://github.com/acid-chicken/aiko)

Aiko is an alternative back-end server for Misskey.

## Build

Just 4 steps.

### 1. clone repository

```bash
git clone --recursive https://github.com/acid-chicken/aiko.git
```

### 2. apply patch

```bash
cp -R lib/misskey src/Misskey
ls -1 diff | grep -v \.d$ | xargs -I% sh -c 'ed src/Misskey/'%' < diff/'%
for x in de-DE en-US fr-FR ja-JP ja-KS pl-PL es-ES nl-NL zh-CN ko-KR
do ed src/Misskey/locales/$x.yml < diff/locales.d
done
```

### 3. build client

```bash
cd src/Misskey
yarn install
NODE_ENV=production yarn run build
cd ../..
cp -R src/Misskey/built/client/assets src/Aiko/wwwroot
```

### 4. run server

```bash
dotnet run --project src/Aiko
```
