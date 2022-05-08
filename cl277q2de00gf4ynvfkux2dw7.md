## Context API with TypeScript and Next.JS

### Why do we need context?
In a typical React application, data is passed top-down (parent to child) via props. but such usage can be cumbersome for certain types of props (e.g., locale preference, UI theme) that are required by many components within an application. Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree. [read more](https://reactjs.org/docs/context.html)

### What is contextAPI?
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

So, now that we know why we need context and what context is, let's dive into the coding part.

Before starting, set up a basic version of the next JS app with typescript

```npm
npx create-next-app context-api
npm install --save-dev typescript @types/react
```

Create a folder called context, here we will store all the different contexts. For now, create an AuthContext.tsx file

### Step 1:- Create context type
Inside AuthContext.tsx.
As we are using TypeScript we have to create types for our context
```typescript
type authContextType = {
    user: boolean;
    login: () => void;
    logout: () => void;
};
```
### Step 2:- Create context default values
```typescript
const authContextDefaultValues: authContextType = {
    user: null,
    login: () => {},
    logout: () => {},
};
```
### Step 3:- createContext & useContext
```typescript
import { createContext, useContext } from "react";

const AuthContext = createContext<authContextType>(authContextDefaultValues);

export function useAuth() {
    return useContext(AuthContext);
}
```
### Step 4:- Create a provider function
```typescript 
type Props = {
    children: ReactNode;
};

export function AuthProvider({ children }: Props) {
    const value = {

    }
    return (
        <AuthContext.Provider value={value}>
            {children}
        </AuthContext.Provider>
    );
}
```
We will wrap this AuthProvider function, where we want to use our context, and the value prop will have the values of authContextType. We will fill in the values in the next step.

### Step 5:- Fill up values
```typescript
export function AuthProvider({ children }: Props) {
    const [user, setUser] = useState<boolean>(null);

    const login = () => {
        setUser(true);
    };

    const logout = () => {
        setUser(false);
    };

    const value = {
        user,
        login,
        logout,
    };

    return (
    ...
```
Now our context is ready to use.

### Step 6:- Enable AuthProvider
First, we have to enable AuthProvider, to do so edit the default _app.js file like so
```typescript
import { AuthProvider } from "../context/AuthContext";
import "../styles/globals.css";

function MyApp({ Component, pageProps }) {
    return (
            <AuthProvider>
                <Component {...pageProps} />
            </AuthProvider>
    );
}

export default MyApp;
```
Step 7:- Using context
Now remove all the template nextJS generate and simply import the context
```typescript
import Head from "next/head";
import styles from "../styles/Home.module.css";
import { useAuth } from "../context/AuthContext";

export default function Home() {
    const { user, login, logout } = useAuth();

    return (
        <div className={styles.container}>
            <Head>
                <title>Context-api with TypeScript and nextJS</title>
                <link rel="icon" href="/favicon.ico" />
            </Head>
            <main className={styles.main}>
                <div>
                    <h1>Hello Context</h1>
                    <h2>User: {user ? "login" : "logout"}</h2>
                    <div>
                        <button onClick={login}>Login</button>
                        <button onClick={logout}>Logout</button>
                    </div>
                </div>
            </main>
        </div>
    );
}
```
Okay, many things happen here let me break it down, first, we import the context hook "useAuth" then inside our Home() we destructure all the values from "useAuth" then we use it as per our requirement.

[See the live demo](https://context-api-with-nextjs-and-ts.vercel.app/)
[Github repo](https://github.com/shareef99/context-api-with-nextjs-and-ts)
[My portfolio](https://portfolio.shareef.vercel.app/)
[Linkedin](https://www.linkedin.com/in/nadeem-shareef-7a8394182/)
[twitter](https://twitter.com/shareefBhai99)