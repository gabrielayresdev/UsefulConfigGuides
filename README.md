# UsefulConfigGuides
Guias para configurar diversas tecnologias


## Tecnologias 

- [Jest + React Testing Library em projeto React + TS criado com Vite](#jest--react-testing-library-em-projeto-criado-com-vite)



### Jest + React Testing Library em projeto criado com Vite

```console

    npm i ts-node -D
    npm i @types/jest -D


    npm i @swc/core @swc/jest -D
```

Mudar a propriedade transform no jest.config para 

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

Caso esteja usando arquivos de estilo, mudar a propriedade moduleNameMapper para

```js
    moduleNameMapper: {
        "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
        "<rootDir>/__mocks__/fileMock.js",
        "\\.(css|less|scss|sass)$": "identity-obj-proxy",
    },
```

```console 
    npm i @testing-library/react @testing-library/jest-dom @testing-library/user-event -D
```

Criar o arquivo setup.ts com o código 

```js
    @import 'testing-library/jest-dom'
```

Mudar a propriedade setupFilesAfterEnv do arquivo jest.config com o path do arquivo setup.ts 

```js 
    setupFilesAfterEnv: ["<rootDir>/src/tests/setup.ts"],
```

================================= EOF =================================