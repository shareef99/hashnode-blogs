## Convert Excel to JSON in ReactJS in just 2 steps

**Hello Developers 🙌**

Today we will see how to convert Excel to JSON

We will use `xlsx` package.

No more talking let's jump into the coding part.

### Install `xlsx` package

```npm
npm i xlsx
```

### Create a basic structure for file upload

```html

<form>
    <label htmlFor="upload">Upload File</label>
    <input
        type="file"
        name="upload"
        id="upload"
        onChange={readUploadFile}
    />
</form>

```

### Convert Excel file to JSON

```js
const readUploadFile = (e) => {
    e.preventDefault();
    if (e.target.files) {
        const reader = new FileReader();
        reader.onload = (e) => {
            const data = e.target.result;
            const workbook = xlsx.read(data, { type: "array" });
            const sheetName = workbook.SheetNames[0];
            const worksheet = workbook.Sheets[sheetName];
            const json = xlsx.utils.sheet_to_json(worksheet);
            console.log(json);
        };
        reader.readAsArrayBuffer(e.target.files[0]);
    }
}

```

Kaboom!🔥 in just two simple steps, you can convert Excel to JSON

**HappyCoding**

Closing here 👋👋👋

> This is **Shareef**.
> My recent project [yourounotes](https://yourounotes.vercel.app/)
> My [Portfolio](https://portfolio.shareef.vercel.app/)
> Twitter [ShareefBhai99](https://twitter.com/shareefBhai99)
> [Linkedin](https://www.linkedin.com/in/nadeem-shareef-7a8394182/)
> My [other Blogs](https://dev.to/shareef)