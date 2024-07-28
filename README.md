# Configuração de Next.js 14 com TypeScript e Jest

Este guia fornece instruções passo a passo para configurar um projeto Next.js 14 com TypeScript, incluindo a configuração do Jest e React Testing Library para testes.

## Pré-requisitos

- Node.js (versão 14 ou superior)
- npm (normalmente vem com Node.js)

## Passo 1: Criar um novo projeto Next.js com TypeScript

```bash
npx create-next-app@latest meu-projeto
cd meu-projeto
```

Selecione as seguintes opções durante a criação do projeto:
- Would you like to use TypeScript? › Yes
- Would you like to use ESLint? › Yes
- Would you like to use Tailwind CSS? › (Sua preferência)
- Would you like to use `src/` directory? › Yes
- Would you like to use App Router? › Yes
- Would you like to customize the default import alias? › No

## Passo 2: Instalar dependências de teste

```bash
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @types/jest jest-environment-jsdom
```

## Passo 3: Configurar o Jest

Crie um arquivo `jest.config.js` na raiz do projeto:

```javascript
const nextJest = require('next/jest')

const createJestConfig = nextJest({
  dir: './',
})

const customJestConfig = {
  setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],
  testEnvironment: 'jest-environment-jsdom',
  moduleNameMapper: {
    '^@/components/(.*)$': '<rootDir>/src/components/$1',
    '^@/pages/(.*)$': '<rootDir>/src/pages/$1',
  },
}

module.exports = createJestConfig(customJestConfig)
```

## Passo 4: Criar arquivo de setup do Jest

Crie um arquivo `jest.setup.js` na raiz do projeto:

```javascript
import '@testing-library/jest-dom'
```

## Passo 5: Atualizar tsconfig.json

Adicione as seguintes linhas ao seu `tsconfig.json`:

```json
{
  "compilerOptions": {
    "types": ["jest", "@testing-library/jest-dom"]
  }
}
```

## Passo 6: Atualizar package.json

Adicione os seguintes scripts ao seu `package.json`:

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch"
  }
}
```

## Passo 7: Criar um teste de exemplo

Crie uma pasta `__tests__` na raiz do projeto e adicione um arquivo `Home.test.tsx`:

```typescript
import { render, screen } from '@testing-library/react'
import Home from '../src/app/page'

describe('Home', () => {
  it('renders a heading', () => {
    render(<Home />)
    const heading = screen.getByRole('heading', { name: /welcome to next\.js!/i })
    expect(heading).toBeInTheDocument()
  })
})
```

## Passo 8: Executar os testes

Para executar os testes uma vez:

```bash
npm test
```

Para executar os testes em modo de observação:

```bash
npm run test:watch
```

## Estrutura do Projeto

```
meu-projeto/
├── __tests__/
│   └── Home.test.tsx
├── src/
│   ├── app/
│   │   └── page.tsx
│   ├── components/
│   └── pages/
├── jest.config.js
├── jest.setup.js
├── next.config.js
├── package.json
├── tsconfig.json
└── README.md
```

## Dicas Adicionais

1. Sempre coloque seus testes próximos aos componentes que eles testam.
2. Use `describe` para agrupar testes relacionados.
3. Use `it` ou `test` para descrever comportamentos específicos.
4. Utilize os utilitários do `@testing-library/react` para interagir com seus componentes nos testes.

## Recursos Úteis

- [Documentação do Next.js](https://nextjs.org/docs)
- [Documentação do Jest](https://jestjs.io/docs/getting-started)
- [Documentação do React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

Lembre-se de atualizar regularmente suas dependências e adaptar sua configuração conforme necessário à medida que seu projeto cresce.
