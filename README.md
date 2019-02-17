# CasparCG Vue based HTML graphics boilerplate

A boilerplate to develop HTML templates for CasparCG using the Vue framework.

## Project setup
```
git clone https://github.com/baltedewit/casparcg-vue-boilerplate.git
cd casparcg-vue-boilerplate
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```
Open `http://localhost:8080` in a browser or send `CG 1 ADD http://localhost:8080/index.html 1` to CasparCG.

### Compiles and minifies for production
```
yarn run build
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Developing for the browser

Note that your browser and the renderer in CasparCG will be different! Both 2.1.0.NRK and 2.2.0 run on Chromium 63 and they are configured in a different way than your normal browser. (E.g. web security features are disabled, webgl is disabled by default, hardware acceleration is disabled by default) You can attach debugging tools to the renderer in CasparCG, but you will lose the ability to use Vue devtools. Development will most likely be a combination of testing code and logics in Chrome and testing visual output in CasparCG.
