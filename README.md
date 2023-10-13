# UsefulConfigGuides
Guias para configurar diversas tecnologias


## Tecnologias 

- [Jest + React Testing Library em projeto React + TS criado com Vite](#jest--react-testing-library-em-projeto-criado-com-vite)
- [Storybook em projeto Vite](#storybook-em-projeto-vite)



### Jest + React Testing Library em projeto criado com Vite

```console
    npm i jest -D

    npx jest --init
```

Realizar as configurações iniciais: yes / yes / jsom / no / v8 / yes

```console

    npm i ts-node -D
    npm i @types/jest -D


    npm i @swc/core @swc/jest -D
```

Mudar a propriedade transform no _jest.config_ para 

```js 
    transform: {
        "^.+\\.(t|j)sx?$": [
            "@swc/jest",
            {
            jsc: {
                parser: {
                syntax: "typescript",
                tsx: true,
                decorators: true,
                },
                keepClassNames: true,
                transform: {
                legacyDecorator: true,
                decoratorMetadata: true,
                react: {
                    runtime: "automatic",
                },
                },
            },
            module: {
                type: "es6",
                noInterop: false,
            },
            },
        ],
    },
```

Caso esteja usando arquivos de estilo, intalar identity-obj-proxy 

```console
    npm i identity-obj-proxy -D
```

e mudar a propriedade moduleNameMapper no arquivo _jest.config_ para

```js
    moduleNameMapper: {
        "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
        "<rootDir>/src/test/__mocks__/fileMock.ts",
        "\\.(css|less|scss|sass)$": "identity-obj-proxy",
    },
```

Criar uma pasta _\_\_mocks___ dentro da pasta test, e criar uma arquivo _\_\_fileMock.ts___ com o código

```js
    module.exports = {};
```


```console 
    npm i @testing-library/react @testing-library/jest-dom @testing-library/user-event jest-environment-jsdom -D
```

Criar o arquivo _setup.ts_ com o código 

```js
    import 'testing-library/jest-dom'
```

Mudar a propriedade setupFilesAfterEnv do arquivo _jest.config_ com o path do arquivo setup.ts 

```js 
    setupFilesAfterEnv: ["<rootDir>/src/tests/setup.ts"],
```

================================= EOF =================================

### Storybook em projeto Vite

Inicie o storybook com
```console
     npx storybook init --builder @storybook/builder-vite --use-npm
```

E aceite a instalação da dependência __storybook__

Caso queira mudar o tema do storybook, adicione o arquivo manager.js na pasta storybook e digite o seguinte código: 

```js
    import { addons } from "@storybook/addons";
    import { themes } from "@storybook/theming";
    
    addons.setConfig({
      themes: themes.dark,
    });
```
O arquivo main.ts deve conter o seguinte código: 

```js
import type { StorybookConfig } from "@storybook/react-vite";

const config: StorybookConfig = {
  stories: ["../src/components/**/*.stories.tsx"],
  staticDirs: ["../src/assets"],
  addons: [
    "@storybook/addon-links",
    "@storybook/addon-essentials",
    "@storybook/addon-onboarding",
    "@storybook/addon-interactions",
    "@storybook/addon-designs",
    "@storybook/addon-a11y",
  ],
  framework: {
    name: "@storybook/react-vite",
    options: {},
  },
  docs: {
    autodocs: true,
  },
};
export default config;
```

O arquivo preview.ts deve importar os estilos globais no começo do códgio

================================= EOF =================================

