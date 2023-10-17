# Prerequisites

Check the latest system requirements or minimum required versions to setup your Next.js app. This includes Node.js and yarn/npm.

System requirements (Next.js documentation 2023):

- Node.js 16.14 or later.
- macOS, Windows (including WSL), and Linux are supported.

## Project setup

There are two ways to start your Next.js app. Automatic and Manual installation. They recommend to use the Automatic installation which setups everything for you.

- To create a Next.js project, run:
  ```
  npx create-next-app@latest
  ```javascript
- This will prompt you with their recommended configuration but you are free to change it.
  ```
    What is your project named? my-app
    Would you like to use TypeScript? No / Yes
    Would you like to use ESLint? No / Yes
    Would you like to use Tailwind CSS? No / Yes
    Would you like to use `src/` directory? No / Yes
    Would you like to use App Router? (recommended) No / Yes
    Would you like to customize the default import alias (@/*)? No / Yes
    What import alias would you like configured? @/*
  ```javascript
- `App Router` is recommended since you are installing Next.js 13 or later.
- For import alias you can choose `No` to use Standard Import or `Yes` to use Import Alias.
- Standard Inmport (Without Aliases):
  ```
  import CustomComponent from './components/CustomComponent';
  ```javascript
- Import Aliases:
  ```
  import CustomComponent from '@/components/CustomComponent';
  ```javascript