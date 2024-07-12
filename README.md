# Configurar o Jest no NEXT 14 (INICIANTES)

## primeiro inicie um projeto next

### [Iniciar Next.js](https://nextjs.org/docs/getting-started/installation)

- ~~~bash
    npx create-next-app@latest 
    ~~~

se quiser seguir passo a passo para ==> [Instalar o Jest](https://nextjs.org/docs/app/building-your-application/testing/jest) 

- ~~~bash
    npm install -D jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom
    ~~~
- ~~~bash
    npm init jest@latest
    ~~~
    1. yes
    2. yes
    3. jsdom
    4. no
    5. v8
    6. no



troque o jest.config.ts por isso:

~~~typescript
    import type { Config } from 'jest'
import nextJest from 'next/jest.js'
 
const createJestConfig = nextJest({
  // Provide the path to your Next.js app to load next.config.js and .env files in your test environment
  dir: './',
})
 
// Add any custom config to be passed to Jest
const config: Config = {
  coverageProvider: 'v8',
  testEnvironment: 'jsdom',
  // Add more setup options before each test is run
  setupFilesAfterEnv: ['<rootDir>/jest.setup.ts'],
  preset: 'ts-jest',
}
 
// createJestConfig is exported this way to ensure that next/jest can load the Next.js config which is async
export default createJestConfig(config)
~~~

#### installe este pacote:

* ~~~bash
    npm i ts-jest
    ~~~

#### crie um arquivo  ```jest.setup.ts``` e coloque isto:

* ~~~bash
    import '@testing-library/jest-dom'
    ~~~
#### adicione no ```scripts``` dentro do  ```package.json``` :
* ~~~bash
    "test": "jest",
    "test:watch": "jest --watch"
    ~~~

#### installe este pacote:

* ~~~bash
    npm i ts-node -D
    ~~~

## Dentro da pasta src crie a pasta ```__tests__```
* dentro dela pode criar seus arquivos de testes Ex: ```page.spect.tsx``` ou ```page.test.tsx```

#### instale este pacote
* ~~~bash
    npm i @types/jest -D
    ~~~
#### instale este pacote
* ~~~bash
    npm i -D eslint-plugin-jest-dom eslint-plugin-testing-library
    ~~~

### no arquivo ```.eslintrc.json``` adicione este dois: 

 * ~~~json
    "extends": [
        "next/core-web-vitals",
        "plugin:jest-dom/recommended",
        "plugin:testing-library/react"
    ]
    ~~~
### de um restar no eslint
 1. precione ```ctrl + shift + p```
 2. digite: eslint restart
