---
parent: React
nav_order: 2
---

# Next.js

Next.js is framework for react which itself is a UI framework. It comes with all the features needed for production: hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. [Reference](https://nextjs.org/learn/basics/create-nextjs-app)

Create a new next.js app using

```bash
$ npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"
$ cd nextjs-blog
$ npm run dev
```

## Pages and navigation

To create a new page, you create a file in the `pages` directory. The path of the file is the route.

```js
// pages/posts/first-post.js
export default function FirstPost() {
  return <h1>First Post</h1>;
}
```

This shows up in `/posts/first-post/`. To link the page to a different page, you use `Link` component to wrap the traditional `a`. Here's how you use it

```js
// pages/posts/first-post.js
import Link from "next/link";

export default function FirstPost() {
  return (
    <>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </>
  );
}
```

Link allows us to do client-side navigation. This means page transition happens using javascript which is faster than default navigation done by the browser. Next.js does code splitting by page so that only js for current page is loaded first. On production, it also pre-fetches `Link`s in the current page. This makes page transition near-instant.

## Assets and Metadata

Assets are put in `public` directory. For example if you put a file at `public/images/profile.jpg`, it'll be available at `/images/profile.jpg`. You can use following html to use this pic:

```html
<img src="/images/profile.jpg" alt="Your Name" />
```

But this is not recommended. Instead use `Image` component to use automatic image optimizations. Use it the following way

```js
import Image from "next/image";

const YourComponent = () => (
  <Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
  />
);
```

For metadata of a page, use `Head` component instead of traditional `head`:

```js
<Head>
  <title>Create Next App</title>
  <link rel="icon" href="/favicon.ico" />
</Head>
```

## CSS

You should use css modules to add styling to your components. Here's how you do it: create css in your component directory ending with `.module.css`

```css
/* components/layout.module.css */
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
```

And in your component

```js
// components/layout.js
import styles from "./layout.module.css";

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>;
}
```

This automatically generates css class names so that you don't have to worry about css collisions. Also only minimal amount of css required for each page is loaded.

While css modules are more useful for component-level styles, you can also have global css. Global css file can be put anywhere, but they have to be imported only in `pages/_app.js`. Create following following files

```css
/* styles/global.css */
html,
body {
  padding: 0;
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu,
    Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  line-height: 1.6;
  font-size: 18px;
}

img {
  max-width: 100%;
  display: block;
}
```

```js
// pages/_app.js
import "../styles/global.css";

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />;
}
```

## Pre-rendering and data fetching

By default, next.js pre-renders every page i.e. HTML for every page is generated in advance instead of having client generate everything using js (like in standard react app). This helps in better performance and SEO. 


Next.js can do two forms of pre-rendering: static generation or service-side rendering. You can also choose type of rendering per page.

### Static generation

Static generation can work event if the data for the html has to be fetched from database or file system. You can do this by exporting an async function `getStaticProps` as follows.

```js
import Head from "next/head";
import Layout, { siteTitle } from "../components/layout";
import { getSortedPostsData } from "../lib/posts";

export async function getStaticProps() {
  const allPostsData = getSortedPostsData();
  return {
    props: {
      allPostsData,
    },
  };
}

export default function Home({ allPostsData }) {
  return (
    <Layout home>
      <Head>
        <title>{siteTitle}</title>
      </Head>
      <section className={utilStyles.headingMd}>
        <p>[Your Self Introduction]</p>
      </section>
      <section className={`${utilStyles.headingMd} ${utilStyles.padding1px}`}>
        <h2 className={utilStyles.headingLg}>Blog</h2>
        <ul className={utilStyles.list}>
          {allPostsData.map(({ id, date, title }) => (
            <li className={utilStyles.listItem} key={id}>
              {title}
              <br />
              {id}
              <br />
              {date}
            </li>
          ))}
        </ul>
      </section>
    </Layout>
  );
}
```

### Server-side rendering

Static generation will not work if you can't pre-render page ahead of user's request. So, we'll use server-side rendering to fetch the data at the request time. Just like static generation, we need to export async function `getServerSideProps`.


```js
export async function getServerSideProps(context) {
  return {
    props: {
      // props for your component
    }
  }
}
```

## Dynamic routes

We've learnt to add specific pages but what if we want to add dynamic routes which depend on data say `/posts/<id>`. To do this we create a file `pages/posts/[id].js` and implement `getStaticPaths` and `getStaticProps`.


```js
// pages/posts/[id].js
import Layout from '../../components/layout'
import { getAllPostIds, getPostData } from '../../lib/posts'

export async function getStaticPaths() {
  const paths = getAllPostIds()
  return {
    paths,
    fallback: false
  }
}

export async function getStaticProps({ params }) {
  const postData = getPostData(params.id)
  return {
    props: {
      postData
    }
  }
}

export default function Post({ postData }) {
  return (
    <Layout>
      {postData.title}
      <br />
      {postData.id}
      <br />
      {postData.date}
    </Layout>
  )
}
```