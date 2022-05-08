## Rendering markdown made easy with react-markdown
in ReactJS and NextJS web APPs

# Hello Developers 👋

If you are using ReactJS or NextJS(React Framework) to make your blog then rendering **MARKDOWN** is so much easy with **React-Markdown**

> React-Markdown comes with build-in **TypeScript** support 🤩.
> Let's stop talking and start coding.

## Basic setup

* I am using **NextJS** with **TypeScript** for this blog.
* I have a folder/directory with the name *post* containing all the posts and inside the *post* folder/directory I have two posts.
* You can find the code on my GitHub (Link will be shared at the end).

```tsx
// pages/index.tsx
import { FC, Fragment } from "react";
import Link from "next/link";

interface Props {}

const Home: FC<Props> = () => (
    <Fragment>
        <h1>Hello Next.js 👋</h1>
        <div className="posts-container">
            <Link href="/posts/first-post">First post</Link>
            <Link href="/posts/second-post">Second post</Link>
        </div>
    </Fragment>
);

export default Home;
```
* I am keeping things simple to focus more on **React-Markdown**

> These two posts are taken from **[Maximilian](https://twitter.com/maxedapps)** course on **NextJS**

* Then we have a file to show individual posts and render our **MARKDOWN**

```tsx
// /pages/posts/[slug].tsx

import { FC, Fragment } from "react";
import { GetStaticProps, GetStaticPropsContext, GetStaticPaths } from "next";
import { PostType } from "../../interfaces";
import { getPostData, getPostsFiles } from "../../lib/post-utils";
import PostContent from "../../components/PostContent";

interface Props {
    post: PostType;
}

const BlogPost: FC<Props> = ({ post }: Props) => {
    return (
        <Fragment>
            // /components/PostContent.tsx
            <PostContent post={post} />
        </Fragment>
    );
};

export const getStaticProps: GetStaticProps = async (context: GetStaticPropsContext) => {
    const { slug } = context.params;
    const postData = getPostData(slug);
    return {
        props: {
            post: postData,
        },
        // regenerate after every 600s(10mins)
        revalidate: 600,
    };
};

export const getStaticPaths: GetStaticPaths = async () => {
    const postFilenames = getPostsFiles();
    const slugs = postFilenames.map((fileName) =>
        fileName.replace(/\.md$/, "")
    );
    return {
        paths: slugs.map((slug) => ({ params: { slug: slug } })),
        fallback: false,
    };
};

export default BlogPost;

```
> Here I set up the basic /posts/[slug] page, I will not go into details, let's Work on the **PostContent** component

## Let's work with React-Markdown.

* Install *React-Markdwon*
```npm
     npm i react-markdown
```
> Now the easiest way to render **MARKDOWN**

```tsx

import React from "react";
import { PostType } from "../interfaces";
import ReactMarkdown from "react-markdown";

interface Props {
    post: PostType;
}

const PostContent = ({ post }: Props) => {
    return (
        <article className="content">
            <ReactMarkdown>{post.content}</ReactMarkdown>
        </article>
    );
};

export default PostContent;

```

> Wooowww! with just one line we render **MARKDOWN**
> But if we go to the first blog it doesn't show an image because we get only the name of the file, we have to generate the path for the image and we can also customize how an image should display.

## Let's optimize & customize the image.

* ReactMarkdown has **components** prop which help us to map tag name to React Component
* **components** take an object which contains the mapping of HTML tags.

> Here, we are checking if a **P** tag has an image element if yes, then we are rendering our own image with our custom styles and if it is not an image then we are just returning the content of it.

```tsx

...
const PostContent = ({ post }: Props) => {
    return (
        <article className="content">
            <ReactMarkdown
                components={{
                    p: ({ node, children }) => {
                        if (node.children[0].tagName === "img") {
                            const image: any = node.children[0];
                            return (
                                <div className="image">
                                    <Image
                                        src={`/images/${image.properties.src}`}
                                        alt={image.properties.alt}
                                        width="600"
                                        height="300"
                                    />
                                </div>
                            );
                        }
                        // Return default child if it's not an image
                        return <p>{children}</p>;
                    },
                }}
            >
                {post.content}
            </ReactMarkdown>
        </article>
    );
};

```

## Let's add syntax highlighting for *CODE* blocks

* Firstly install syntax-highlighter
```
npm i react-syntax-highlighter @types/react-syntax-highlighter
```
* react-syntax-highlighter makes it very easy to style our **CODE** blocks.
* Here I am using 'materialDark' but you have many options and many themes to apply for your site.

```tsx

import { Prism as SyntaxHighlighter } from "react-syntax-highlighter";
import { materialDark } from "react-syntax-highlighter/dist/cjs/styles/prism";

const PostContent = ({ post }: Props) => {
    return (
        <article className="content">
            <ReactMarkdown
                components={{
                    p: ({ node, children }) => {
                        ...
                    },
                    code({ className, children }) {
                        // Removing "language-" because React-Markdown already added "language-"
                        const language = className.replace("language-", "");
                        return (
                            <SyntaxHighlighter
                                style={materialDark}
                                language={language}
                                children={children[0]}
                            />
                        );
                    },
                }}
            >
                {post.content}
            </ReactMarkdown>
        </article>
    );
};

```

Closing here 👋👋👋
> This is **Shareef**.
> My [Portfolio](https://portfolio.shareef.vercel.app/)
> Twitter [ShareefBhai99](https://twitter.com/shareefBhai99)
> [GitHub repo of this blog](https://github.com/shareef99/blogs/tree/master/markdown)
> [Linkedin](https://www.linkedin.com/in/nadeem-shareef-7a8394182/)
> My [other Blogs](https://dev.to/shareef)



> Cover photo by [Dustin Curtis] (https://github.com/dcurtis/markdown-mark/tree/master/svg)