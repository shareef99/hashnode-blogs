## How to hide password value in inspect using React and Formik

**Hello Developers 🤩🤩**

Have you ever logged in to Facebook?
Have you ever inspected the Facebook login page?
If not go to [Facebook](https://www.facebook.com/) and try inspecting it, you will find the value of the password filed is not showing.

We will replicate that behavior using React and Formik.

### Creating Project

```npm
npx create-react-app my-app
```

After project setup, install formik.

```npm
npm install formik --save
```

### Basic setup
Setup a basic template for email and password input with submit button.

```jsx
import { useFormik } from "formik";

function App() {
    return (
        <form>
            <input name="email" type="email" placeholder="email" />
            <input 
                name="password"
                type="password"
                placeholder="password"
            />
            <button type="submit">Submit</button>
        </form>
    );
}

export default App;
```

### Implementing Formik

```jsx
import { useFormik } from "formik";

function App() {
    const handleSubmit = (values) => {
        console.log(values);
    };

    const formik = useFormik({
        initialValues: {
            email: "",
            password: "",
        },
    });

    return (
        <form
            onSubmit={(e) => {
                e.preventDefault();
                handleSubmit(formik.values);
            }}
        >
            <input
                name="email"
                type="email"
                placeholder="email"
                {...formik.getFieldProps("email")}
            />
            <input
                name="password"
                type="password"
                placeholder="password"
                onChange={formik.handleChange}
                onBlur={formik.handleBlur}
            />
            <button type="submit">Submit</button>
        </form>
    );
}

export default App;
```

Now check the value in Inspect.
**Kaboom 🔥🔥🔥**
No value in Inspect.

[Live Preview](https://39ph6.csb.app)

Closing here 👋👋👋
> [Github Code Repo](https://github.com/shareef99/blogs/tree/master/hide-password-value)
> This is **Shareef**.
> My recent project [yourounotes](https://yourounotes.vercel.app/)
> My [Portfolio](https://portfolio.shareef.vercel.app/)
> Twitter [ShareefBhai99](https://twitter.com/shareefBhai99)
> [Linkedin](https://www.linkedin.com/in/nadeem-shareef-7a8394182/)
> My [other Blogs](https://dev.to/shareef)
