## Prerequisites

Check the latest system requirements or minimum required versions to setup your Next.js app. This includes Node.js and yarn/npm.

System requirements (Next.js documentation 2023):

- Node.js 16.14 or later.
- macOS, Windows (including WSL), and Linux are supported.

## Project setup

There are two ways to start your Next.js app. Automatic and Manual installation. They recommend to use the Automatic installation which setups everything for you.

### Automatic Installation
- To create a Next.js project, run:
  ```
    npx create-next-app@latest
  ```
- This will prompt you with their recommended configuration but you are free to change it.
  ```
    What is your project named? my-app
    Would you like to use TypeScript? Yes
    Would you like to use ESLint? No
    Would you like to use Tailwind CSS? No
    Would you like to use `src/` directory? No
    Would you like to use App Router? (recommended) Yes
    Would you like to customize the default import alias (@/*)? No
    What import alias would you like configured? @/* // This will only show if you choose Yes above
  ```
- For optional `src/` directory, you have the choice of whether you want to create an `src` folder to separate your code from configuration files.
  - Choosing `No`
    ```
      root/
      ├── node_modules/
      ├── app/
      │   ├── page.js
      │   ├── layout.js
      ├── styles/
      │   ├── main.module.css
      ├── public/
      │   ├── images/
      │   ├── favicon.ico
      ├── package.json
    ```
  - Choosing `Yes`. It will put the app, styles and public folder inside `src`
    ```
      root/
      ├── node_modules/
      ├── src/
      │   ├── app/
      │   │   ├── page.js
      │   │   ├── layout.js
      │   ├── styles/
      │   │   ├── main.module.css
      │   ├── public/
      │   │   ├── images/
      │   │   ├── favicon.ico
      ├── package.json
    ```
- `App Router` is recommended since you are installing Next.js 13 or later.
- For import alias you can choose `No` to use Standard Import or `Yes` to use Import Alias.
  - Standard Import (Without Aliases):
    ```javascript
    import CustomComponent from './components/CustomComponent';
    ```
  - Import Aliases:
    ```javascript
    import CustomComponent from '@/components/CustomComponent';
    ```
  - Then run `npm/yarn run dev` and visit `localhost:3000`

### Manual Installation
- Create an empty folder anywhere in your local machine, and run:
  ```
    mkdir my-app // this will be your app name
    cd my-app // this will change your directory to your app
  ```
- Install the required packages
  ```
    npm install next@latest react@latest react-dom@latest
  ```
- After installation, it will create the `node_modules` folder, `package.json` and `package.lock.json`
- You can see this inside your `package.json`
  ```
    {
      "dependencies": {
        "next": "^14.0.3",
        "react": "^18.2.0",
        "react-dom": "^18.2.0"
      }
    }
  ```
- Put the required scripts on your `package.json`
  ```
    {
      "dependencies": {
        "next": "^14.0.3",
        "react": "^18.2.0",
        "react-dom": "^18.2.0"
      },
      "scripts": {
        "dev": "next dev", // start Next.js in development mode.
        "build": "next build", // build the application for production usage.
        "start": "next start", // start a Next.js production server.
        "lint": "next lint" // set up Next.js' built-in ESLint configuration.
      }
    }
  ```
- To test your app locally, you need to manually create the `app` directory by manually creating a folder `app` in root directory.
- Under `app` folder create a `layout.tsx` and `page.tsx` file and put the following inside:
  ```
    // for layout.tsx
    export default function RootLayout({
      children,
    }: {
      children: React.ReactNode
    }) {
      return (
        <html lang="en">
          <body>{children}</body>
        </html>
      )
    }
  ```
  ```
    // for page.tsx
    export default function Page() {
      return <h1>Hello, Mashup Garage!</h1>
    }
  ```
- Then run `npm/yarn run dev` and visit `localhost:3000`
- Problems you might encounter after running `npm/yarn run dev`, this is because the latest nextjs requires `Nodejs 18`
  ```
    ReferenceError: Request is not defined
  ```
- You can fix this by setting up your local nodejs version to `"node": ">=18.17.0" ` example:
  ```
    asdf local nodejs 18.17.0
  ```
