This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

![alt nextjs-logo](./1200px-Nextjs-logo.svg.png)

# Nextjs

This project is a nextjs app ,Nextjs is a **React** frontend development web framework created by Vercel that enables functionality such as server-side rendering and static site generation

# What is SERVER-SIDE RENDERING (SSR)

Unlike a traditional react app where the entire application is loaded and rendered on the client, Nextjs allows the first page load to be rendered by the server,which is great for SEO and performance.
ps: keep in mind the fewer the dependencies used the lighter the app and the higher performance your app will be .

![alt Server-Side-Rendering-Flowchart](./Server-Side-Rendering-Flowchart.jpg)

# Benefits of the NEXTjs

- Easy page routing (like in the html you just create the page you will go with the name **like** store.js => url/store)

- API Routes

- Out of the box TypeScript and Sass (you can use ts and sass in your app)

- Static site generation

- Easy Deployment (vercel.com just import you github repo)

# File and Folder Structure

- **Public** : Where a static site is generated there you can put images there ,but keep in mind that everything you put there is accessable from your browser.

- **Styles** : There is a globals.css which is for the whole app to apply like font-family ,and other stuff can be added to apply on your whole app.

- **Pages** : You will have index.js file and here you will benefit from nextjs, since when you create in this folder a file with a name it will dynamically add it to your route (no need to add routes and other stuff) /store => store.js file .

- **\_app.js**: Wrapps around all of your page components , where it is a function which takes in a component which is your page component with page props and return it , but we can add for this a layout like a navbar,footer, and other stuff.

To create a custom Document ,where document is commonly used to augment your application's html and body tags (this is rendered on the server so no need to add onclick ...),create the file './pages/\_document.js' and extend the Document class like :

```bash
class MyDocument extends Document
```

[Nextjs documentation part](https://nextjs.org/docs/advanced-features/custom-document)

# Data Fetching

fetch data and pass it as a props to our component , there are three separate methods that we can use :

1. get static props : which will allow us to fetch data at build time .
2. get server side props : which will fetch the data on every request (little slower).
3. get static paths props : which to dynamically generate paths based on the data fetching.

##### getstaticprops method example:

```bash
export const getStaticProps = async () =>{
    const res = await fetch(`https......(url)`);
    const results = await res.json();

    return {
        props:{
            results
        }
    }
}
```

### Nested Routes

_example: /post/1_

For the **Link** tag in nextjs you might use nested links :
example:

```bash
<Link href="/post/[id]" as={`/post/${post.id}`}>{title}</Link>
```

for nested route you create a folder in the **pages** folder with the route name (post) ,and inside this folder
you create another folder with the param like [id] ([make sure to adapt to the href you are pointing to ]) ,and inside this folder you create a index.js file and create your page.
ps: you can use the useRouter hook from next/router to access the url route

```bash
const post = () =>{
    const router = useRouter();
    const {id} = router.query
    return <div>this is a post {id}</div>
}
```

At this level we can getprops from server for this page lets use the getServerSideProps which happens on the request time (note that context can be passed to methods to get page route params and details)

```bash
export const getServerSideProps = async (context) =>{
    const res = await fetch(`https....../posts/${context.params.id}`);
    const result = await res.json();
    return {
        props:{
            result
        }
    }
}
```

And another solution for dynamic route you can call the getStaticPaths to get the props

```bash
export const getStaticPaths = async ()=>{
    const res = await fetch(`https...../posts`);
    const results = await res.json();
    const ids = posts.map(post=>post.id);
    const paths = ids.map(id=>({params:{id:id.toString()}}))

    return {
        paths,
        fallback:false //this if you go to a path which is not found it will return a 404 page
    }
}
```

##### https://nextjs-project-rho-eight.vercel.app/

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
