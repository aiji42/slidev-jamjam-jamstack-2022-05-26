---
theme: unicorn
highlighter: shiki
lineNumbers: false
layout: center
---

<div class="text-center text-5xl pb-8">ð</div>

# Remixã®åã¿ãç´¹ä»ããã

## @aiji42_dev

---
layout: intro
introImage: 'https://storage.googleapis.com/zenn-user-upload/avatar/e738d28d01.jpeg'
---

# Who am I ?

## Uejima Aiji | Twitter: @aiji42_dev

<br>

- ð¢ æ ªå¼ä¼ç¤¾ã¨ã¤ãã¼ã ã©ã¤ããã¶ã¤ã³
- ð§ ãªã¼ãã¨ã³ã¸ãã¢
- ð¥ æè¿ã®æ´»å 
  - Cloudflareã§ISRãå®ç¾ããã
  - CSRãªãµã¤ããPrerenderã§SSRã½ãããã
  - PrismaããSupabase APIãå©ãããã«ã¦ã§ã¢ä½ã£ãã
  - ç¤¾åã§ãã­ã³ãã¨ã³ãçISSUCONéå¬ããã

---
layout: image-center
image: 'https://remix.run/remix-v1.jpg'
---

# ä»æ¥ã¯Remixãç´¹ä»ããã

ãããªãã¯ããã¦ããåå¹´éãåäººã§ãç¤¾åã§ãRemixãä½¿ãåããã®ã§

---

## ãã®çºè¡¨ããã²èãã¦æ¬²ããäºº

- Remixã£ã¦æè¿è¯ãèãããç®ã«ããããããªã¼ ð¤

- Next.jså¤§å¥½ãï¼æ­£ç´ã³ã¬ä¸æ¬ã§é£ã£ã¦ããããã­ ð
  - ãã®çºè¡¨ãèãã¨ããã¨ãRemixãä½¿ç¨ããªãã¦ãå®è£ã®ä»æ¹ã®å¹ãåºãããã¨ã§ããã

- æè¿Next.jsããªããæ°ããLayoutã«é¢ããRFå¬éãããã­
  - ããã§ããå®ã¯Remixããã®åé§ãã§ã

- Cloudflareã£ã¦ãªããæè¿å¢ããããã­ããªããè©¦ãã¦ã¿ããããª ð©
  - Cloudflareã¯Remixãèªãä¸ã§åãé¢ããªãè©±é¡ã§ã

---

## ãã®åã«ãæ­ã

ãã®çºè¡¨ã§ã¯Jamstackã«ãCMSã«ãè§¦ãã¾ãã ðâ

ããããRemixãè§£æ±ºãããã¨ãã¦ãããã¨ã¯ã  
ä»å¾ã®Reactããã­ã³ãçéã®æ¹åæ§ã«å°ãªãããå½±é¿ãä¸ãã¦ããã  
å¤ãã®äººã«è§¦ãã¦ã»ããç¥ã£ã¦ã»ããã¨ããæ°æã¡ã§ããã®çºè¡¨ã«è¨ãã§ãã¾ãã

---

# What is Remix ?

- React SSRãã¬ã¼ã ã¯ã¼ã¯
- React Routerã®éçºãã¼ã ãéçºãä¸»å°
- æ¨å¹´11ææ«ã«v1ããªãªã¼ã¹ãããã¿ã¤ãã³ã°ã§ãããªãã¯ã«
- Cloudflare Workersã§ç¨¼åãããããããDenoããµãã¼ããã¦ããã
- ð ã®ã¢ã¤ã³ã³ãããä½¿ããã

---

#### Remixã®ç¹å¾´ â 
<br>

# loader ã¨ action

---

<div class="flex space-x-4">
<div class="flex-1">

```tsx
// app/routes/posts/$slug.tsx
export const loader = async ({ params }) => {
  const post = await db.post.findUnique({ 
    where: params.slug
  })
  
  return { post }
}

export const action = async ({ request, params }) => {
  if (request.method === 'POST') {
    await db.post.create({ ... })
  }
  if (request.method === 'DELETE') {
    await db.post.delete({ ... })
  }
  if (request.method === 'PATCH') {
    await db.post.update({ ... })
  }
}

const Page: FC = () => {
  const { post } = useLoaderData()
  return ...
}
export default Page


```

</div>

<div class="flex-1">

# loaderã¨action

#### Next.js ã® getServerSideProps ã API Routes ã®ãããªãã®

<br>

ãã¼ã¸ã³ã³ããã³ãã¨åä¸ãã¡ã¤ã«ã«å®ç¾©å¯è½

<br>

##### loader
GETã¢ã¯ã»ã¹æã®ãã¼ã¿ãã§ãããå®ç¾©  
ãã¼ã¸(ã³ã³ããã³ã)ããã¯**useLoaderData**ã§åå¾ãã**useFetcher**ã§åãã§ããå¯è½

##### action
POSTãDELETEãªã©ã®ãã¥ã¼ãã¼ã·ã§ã³ãå®ç¾©ãã
**useSubmit**ã**useFormAction**ãformè¦ç´ ãããªã¯ã¨ã¹ããã

</div>
</div>

---

#### Remixã®ç¹å¾´ â¡
<br>

# File system routing ã¨ Nested Routing (Layout)

ã¬ã¤ã¢ã¦ãã«ã¼ã / å±éå¦ç

---


<div class="flex space-x-4">
<div class="flex-1">

```text
app/
âââ routes/
â   âââ blog/
â   â   âââ $postId.tsx
â   â   âââ categories.tsx
â   â   âââ index.tsx
â   âââ about.tsx
â   âââ blog.tsx
â   âââ index.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

ãã£ã¬ã¯ããªæ§æããã¡ã¤ã«åããã®ã¾ã¾URLã«ãªãã¨ããç¹ã¯ãNext.jsã®pagesã¨ããä¼¼ã¦ãã

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {7,9}
app/
âââ routes/
â   âââ blog/
â   â   âââ $postId.tsx
â   â   âââ categories.tsx
â   â   âââ index.tsx
â   âââ about.tsx
â   âââ blog.tsx
â   âââ index.tsx
âââ root.tsx
```

</div>

<div class="flex-1">


| URL    | Matched Route        |
|--------|----------------------|
| /      | app/routes/index.tsx |
| /about | app/routes/about.tsx |


</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {4-6}
app/
âââ routes/
â   âââ blog/
â   â   âââ $postId.tsx
â   â   âââ categories.tsx
â   â   âââ index.tsx
â   âââ about.tsx
â   âââ blog.tsx
â   âââ index.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

ãã£ã¬ã¯ããªã®å¥ãå­ã¯ãã®ã¾ã¾URLã«å¤æããã

$(ãã«ãã¼ã¯)ãã¤ããã¨ã  
ãã©ã¡ã¼ã¿ã¨ãã¦loader/actionã§æ±ãã


| URL              | Matched Route                  |
|------------------|--------------------------------|
| /blog            | app/routes/blog/index.tsx      |
| /blog/categories | app/routes/blog/categories.tsx |
| /blog/my-post    | app/routes/blog/$postId.tsx    |


</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {3,8,10}
app/
âââ routes/
â   âââ blog/
â   â   âââ $postId.tsx
â   â   âââ categories.tsx
â   â   âââ index.tsx
â   âââ about.tsx
â   âââ blog.tsx
â   âââ index.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

root.tsxããããã¬ã¤ã¤ã¬ã¤ã¢ã¦ã  
ãã£ã¬ã¯ããªã¨åä¸åãã¡ã¤ã«ãå­ã¬ã¤ã¢ã¦ã

| URL              | Matched Route                  | Layout               |
|------------------|--------------------------------|----------------------|
| /                | app/routes/index.tsx           | app/root.tsx         |
| /about           | app/routes/about.tsx           | app/root.tsx         |
| /blog            | app/routes/blog/index.tsx      | app/routes/blog.tsx  |
| /blog/categories | app/routes/blog/categories.tsx | app/routes/blog.tsx  |
| /blog/my-post    | app/routes/blog/$postId.tsx    | app/routes/blog.tsx  |


</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {3,7}
app/
âââ routes/
â   âââ __authed/
â   â   âââ dashboard.tsx
â   â   âââ $userId/
â   â   â   âââ profile.tsx
â   âââ __authed.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

ããã«ã¢ã³ãã¼ã¹ã³ã¢ã§å§ããã¨  
URLåãããªãã¬ã¤ã¢ã¦ãã«ã¼ãã«ãªã  
(pathless layout routes)

</div>
</div>


<div class="flex space-x-4">
<div class="flex-1">

```text {4}
app/
âââ routes/
â   âââ blog.tsx
â   âââ blog.$slug.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

ãã£ã¬ã¯ããªæ§é ã®ä»£ããã«ãããã§ãè¡¨ç¾å¯è½

</div>
</div>

<div class="flex space-x-4">
<div class="flex-1">

```text {7}
app/
âââ routes/
â   âââ blog/
â   â   âââ $postId.tsx
â   â   âââ categories.tsx
â   â   âââ index.tsx
â   âââ $.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

Catch all route (*)

</div>
</div>

---

## ãã­ã¥ã¡ã³ãã§ç´¹ä»ããã¦ããä¾

<br>

<div class="flex space-x-4">
<div class="flex-1">

```text
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

</div>

<div class="flex-1">

![](/nested-route-0.png)

https://example.com/sales/invices/102000

ãããªæãã®ããã·ã¥ãã¼ã

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {8}
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

```tsx
export default function Root() {
  return (
    <Sidebar>
      <Outlet />
    </Sidebar>
  )
}
```

</div>

<div class="flex-1">

![](/nested-route-1.png)

root.tsxããããã¬ã¤ã¤ã¬ã¤ã¢ã¦ã

Outletã³ã³ããã³ãé¨åãã¬ã³ããªã³ã°æã«  
å­ã¬ã¤ã¢ã¦ãã»å­ãã¼ã¸ã«ãªã

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {3,7}
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

```tsx
export default function Sales() {
  return (
    <>
      <h1>Sles</h1>
      <Tabs />
      <Outlet />
    </>
  )
}
```

</div>

<div class="flex-1">

![](/nested-route-2.png)

ãã£ã¬ã¯ããªã¨åä¸åãã¡ã¤ã«ã§å­ã¬ã¤ã¢ã¦ããå®ç¾©

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {4,6}
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

```tsx
export const loader = async () => {
  const overview = await fetch(...).then((res) => res.json())
  // ...
  return { overviewData, inviceListData }
}
export default function InvoiceList() {
  const { overviewData, inviceListData } = useLoaderData()
  return (
    <>
      <Overview data={overviewData}>
      <InvoiceList items={inviceListData} >
        <Outlet />
      </InvoiceList>
    </>
  )
}
```

</div>

<div class="flex-1">

![](/nested-route-3.png)

layoutã«ãloaderãè¨­ç½®å¯è½

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {5}
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

```tsx
export const loader = async ({ params }) => {
  const data = await db.invoice.findOne({ where: { id: params.id } })
  return { data }
}

export default function Invoice() {
  const { data } = useLoaderData()
  return (
    <InvoiceItem data={data} />
  )
}

export function ErrorBoundary({ error }) {
  return (
    <ErrorMessage>{error.message}</ErrorMessage>
  )
}
```

</div>

<div class="flex-1">

![](/nested-route-4.png)

åãã¼ã¸ã»ã¬ã¤ã¢ã¦ãã«ãã¨ã«  
ErrorBoundaryãå®ç¾©å¯è½

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

```text {5}
app/
âââ routes/
â   âââ sales/
â   â   âââ invoices/
â   â   â    âââ $id.tsx
â   â   âââ invoices.tsx
â   âââ sales.tsx
âââ root.tsx
```

```tsx
export const loader = async ({ params }) => {
  const data = await db.invoice.findOne({ where: { id: params.id } })
  return { data }
}

export default function Invoice() {
  const { data } = useLoaderData()
  return (
    <InvoiceItem data={data} />
  )
}

export function ErrorBoundary({ error }) {
  return (
    <ErrorMessage>{error.message}</ErrorMessage>
  )
}
```

</div>

<div class="flex-1">

![](/nested-route-error.png)

ã¨ã©ã¼ã®ä¼æ¬ãçãããã¨ãã§ãã    
ãã©ã¼ã«ããã¯ãæå°éã«ãªã

</div>
</div>

---

## Nested Routes ãããã¨ä½ãå¬ããã

- ã¬ã¤ã¢ã¦ãã®ã°ã«ã¼ãã³ã°ã¨éå±¤çãªé©å¿

- ä¸¦åãã¼ã¿ãã§ãã
  - åloaderã¯ä¸¦åã«å¦çããããããé«éåã«ã¤ãªãã
  - <img src="/fetch.png" class="h-80" />

---

- ã­ã¸ãã¯ã®å±éå 
  - ç¹å®ã«ã¼ãéä¸ã¯ã­ã°ã¤ã³å¿é ã«ãããªã©ã®ãå±éå¦çãéå±¤çã«ãããããã
  - pathless routesã¨çµã¿åããã¦ç¹å®ã®ãã£ã¬ã¯ããªä¸ã¯æé»çã«èªè¨¼å¿é ã«ãããªã©
 
- å·®åã­ã¼ãã»åãã§ãã
  - ããã²ã¼ã·ã§ã³æã«ãã«ãã¼ã¸ã­ã¼ãã§ã¯ãªããå¿è¦ãªã¬ã¤ã¢ã¦ãã«ã¼ãåã®ã­ã¼ããè¡ããã
  - ä»»æã«ãã¼ã¸åãæ´æ°ããåãã§ããå¦çãå®è£ãããã

---

## ã¡ããã©åæ¥Next.jsã«ãåç­ãªæ©è½ã®RFCãå¬éããã

![](/nextjs-rfc.png)
https://nextjs.org/blog/layouts-rfc

- ç¾ãã­ãã¼ã¶ã«ã§ã¯ããããRemixã¨åç­ã®æ©è½ãã«ãã¼ããäºå®
  - pathlessãErrorBoundaryã«é¢ãã¦ãããã­ã¥ã¡ã³ãã«ã¯ãªããããã¼ã2ã§è¨åãããã¨ã®ãã¨
    - ããªãRemixã®ãã¦ãã¦ãæææ±ºå®ã«å½±é¿ãä¸ãã¦ããå°è±¡
  - ããã©ã«ãã§Server Componentã«ãªã (Remixã§ãåæ§ã«è­°è«ããã¦ããè¿ãå°æ¥ããã©ã«ãã«ãªãã¯ã)

---
layout: cover-logos
logos: [
'https://cdn.worldvectorlogo.com/logos/cloudflare-1.svg',
'https://cdn.worldvectorlogo.com/logos/express-109.svg',
'https://cdn.worldvectorlogo.com/logos/deno-1.svg',
'https://cdn.worldvectorlogo.com/logos/nodejs.svg',
'https://cdn.worldvectorlogo.com/logos/cloudflare-pages-single.svg',
'https://cdn.worldvectorlogo.com/logos/netlify.svg',
'https://cdn.worldvectorlogo.com/logos/vercel.svg',
'https://seeklogo.com/images/F/fly-io-logo-BD23E4EA17-seeklogo.com.png'
]
---

#### Remixã®ç¹å¾´ â¢
<br>

# ãã«ãã©ã³ã¿ã¤ã 

<style>
li {
 font-size: medium;
}
</style>

- Node / web worker / Deno
- Vercel / Netlify / Cloudflare Workersã»Pages, etc
- ãã¡ããã»ã«ããã¹ãå¯è½

---

## Remixã®ä¸çªã®å¼·ã¿ã¯ Cloudflare Workers ä¸ã§åãã¨ããç¹

ã ã¨åäººçã«ã¯æãã

**ã¨ãã¸ã­ã±ã¼ã·ã§ã³ã§ã¬ã³ããªã³ã°ã§ããã¨ããã®ã¯ä»å¾ã®Reactçéã«ããã¦éè¦ãªæå³ããã¤**

---

## Reactãåããå - Server component / Streaming render

<style>
li {
  font-size: medium;
}
</style>

- ã³ã³ããã³ãã®ã¬ã³ããªã³ã°ãServerãµã¤ãã§è¡ãããã«ãªã
  - å¾æ¥ã®SSRã¨ã¯ãã¨ãªããã³ã³ããã³ãã®ç²åº¦ã§è§£æ±ºããããã«ã¹ããªã¼ã ã§è¿å´ãã
  - <small>src: https://mxstbr.com/thoughts/streaming-ssr/</small> <img src="https://mxstbr.com/static/images/renderToString.png" class="h-60 bg-white" />
  - åã³ã³ããã³ãã§ãã¼ã¿ãã§ããã®å¦çãæã¡ãéåæçã»èªå¾çã«è§£æ±ºãã

- åææ¥ç¶æ°ã¯ççºçã«å¢å ããããã¦ã©ã¦ã³ãããªããã«ããã¬ã¤ãã³ã·ãç¡è¦ã§ããªããªããã¨ãäºæ³ã§ãã

---

## ãããªæªæ¥ãè¦æ®ããã¨

- ã¨ãã¸ãã¡ã³ã¯ã·ã§ã³(ã­ã±ã¼ã·ã§ã³)ããªãªã¸ã³ã¨ãã¦æ©è½ãã
- ã¹ã±ã¼ã«ãã¾ãæè­ããªãã¦è¯ã
- 1ãªã¯ã¨ã¹ããããã®ã³ã¹ããå®ä¾¡

ã¨ããç¹ã¯å¤§ããªã¢ããã³ãã¼ã¸ã«ãªã

## ã ããCloudflare Workersä¸ã§åãã¨ããã®ã¯å¤§ããªæå³ãæã¤

<br>

#### Next.jsãæ¨å¹´ã®ã¨ãã¸ãã¡ã³ã¯ã·ã§ã³(middleware)ã®çºè¡¨ãç®åãã«ãã¨ãã¸ã¬ã³ããªã³ã°ãæ¨¡ç´¢ãã¦ãã  
[RFC: Switchable Next.js Runtime #34179](https://github.com/vercel/next.js/discussions/34179)

---

<div class="flex space-x-4">
<div class="flex-1">
<br>

#### Remixã®ç¹å¾´ â£
<br>

# Formã¨ãã«ãã¼

<br>

åè¿°ã®actionã¨éä¿¡ãè¡ãããã®ãFormã³ã³ããã³ããå¤æ°ã®ãã«ãã¼ãåãã¦ãã

ç¹ã« **useTransition** ã¯ãã©ã¼ã ã®submitã®ç¶æ  
(idle / submitting / loading)ãç®¡çããã  
submitä¸­ã®ãã¼ã¿ãåãæ±ããã¨ãå¯è½ãªã®ã§ãæ¥½è¦³çUIã®å®è£ãå®¹æ

</div>
<div class="flex-1">
<video controls autoplay>
  <source src="https://remix.run/jokes-tutorial/img/optimistic-ui.mp4" type="video/mp4">
</video>
</div>
</div>

---

<div class="flex space-x-4">

<div class="flex-1">

```tsx
import { ValidatedForm } from "remix-validated-form";
import { withZod } from "@remix-validated-form/with-zod";

export const validator = withZod(
  // your zod role
);

export const action = async ({ request }) => {
  const result = await validator.validate(await request.formData());
  if (result.error) return validationError(result.error);

  const { firstName, lastName, email } = result.data;
  // Do something with the data
};

export default function MyPage() {
  return (
    <ValidatedForm validator={validator} method="post">
      <FormInput name="firstName" label="First Name" />
      <FormInput name="lastName" label="Last Name" />
      <FormInput name="email" label="Email" />
      <SubmitButton />
    </ValidatedForm>
  );
}
```

</div>
<div class="flex-1">

## remix-validated-form
https://www.remix-validated-form.io/

<br>

remix-validated-formã¨zodãä½¿ç¨ããã¨actionã¨ã³ã³ããã³ããä¸ä½åã§ãã

ã¯ã©ã¤ã¢ã³ãã¨ãµã¼ãã¨ã§ããªãã¼ã·ã§ã³ãå±éåã§ããã ãã§ãªã  
ã¨ã©ã¼ã¡ãã»ã¼ã¸ã®è¿å´ã»ã¬ã³ããªã³ã°ãä¾å¤å¦çã®å®è£ããéæ¾ããã

å¥ã®ãã¼ã¿ã½ã¼ã¹ã¨éä¿¡ãã¦å¥éããªãã¼ã·ã§ã³ãããªã©ããµã¼ããµã¤ããªã³ãªã¼ãªããªãã¼ã·ã§ã³ãããããã«è¿½å å¯è½

</div>
</div>

---

#### Remixã®ç¹å¾´ â¤

<br>

# Cookieãã«ãã¼

CookieãSessionãåãæ±ãããã®ãã«ãã¼ãæ¨æºè£å  

ã·ãªã¢ã©ã¤ãº&æ¤è¨¼ã®æ©è½ãããã©ã«ãã§å®è£ããã¦ãã

loader/actionã¨çµã¿åããããã¨ã§ã  
ããã¾ã§ãã­ã³ãã«å®è£ãã¦ããã¹ãã¼ãç®¡çãèªè¨¼ãªã©ããµã¼ããµã¤ãã¸ç§»è­²ã§ãã

ã­ã¸ãã¯ããã­ã³ãã«é²åºããªãããã  
ç§å¿æ§ã®é«ãæå ±ã®æ¼æ´©é²æ­¢ãããã³ãã«ãµã¤ãºã®è»½æ¸ã«ã¤ãªãã

---

<div class="flex space-x-4">
<div class="flex-1">

```tsx
export const loader = async ({ request }) =>
  supabaseStrategy.checkSession(request, {
    successRedirect: '/private'
  });

export const action = async ({ request }) =>
  authenticator.authenticate('sb', request, {
    successRedirect: '/private',
    failureRedirect: '/login'
  });

export default function LoginPage() {
  return (
    <Form method="post">
      <input type="email" name="email" />
      <input type="password" name="password" />
      <button>Sign In</button>
    </Form>
  );
}
```

</div>
<div class="flex-1">

## remix-auth  
https://github.com/sergiodxa/remix-auth  
(ãµã³ãã«ã³ã¼ãã¯[remix-auth-supabase](https://github.com/mitchelvanbever/remix-auth-supabase))

èªè¨¼æ¹æ³ã»èªå¯ã«ã¼ã«ã»ãã©ã¼ã«ããã¯ã«ã¼ã«ãªã©ãç°¡åã«è¨­å®ã»å¶å¾¡ã§ãã

ã¯ã©ã¤ã¢ã³ãå´ã«ã¯ä¸åã­ã¸ãã¯ãé²åºããªã

</div>
</div>

---

<div class="flex space-x-4">
<div class="flex-1">

# å®ç¨ã«èããããã®ï¼

</div>

<div class="flex-1">

<div class="text-5xl">ð¤</div>


</div>
</div>

<br>


---

<div class="flex space-x-4">
<div class="flex-1">

## <Tweet id="1529131553481453569"/>

</div>

<div class="flex-1">

<img src="https://camo.qiitausercontent.com/bf17791a3291dfe19a39cb25a72449b8e70cea48/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e61702d6e6f727468656173742d312e616d617a6f6e6177732e636f6d2f302f37303336332f35323734633438342d666563342d316137352d313164632d3361313365646637626335632e706e67" class="h-50" />


<img src="/leaderboard.png" class="h-70" />

<small>ä»ã«åäººéçºãµã¼ãã¹ã®éç¨å®ç¸¾ãç¤¾åã§ã®å®ãµã¼ãã¹éçºã¸ã®å°å¥å®ç¸¾ã</small>

</div>
</div>

---

# å®éã«å¾ãããæ©æµ

- ã¹ãã¼ãç®¡çã©ã¤ãã©ãªãä¸è¦
  - åè¿°ã®éã
- èªè¨¼ã­ã¸ãã¯ã»ãã¼ã¿ãã§ããã­ã¸ãã¯ãã¹ã¦ããµã¼ããµã¤ãå®çµ
  - ã¯ã©ã¤ã¢ã³ãã®å®è£ã¯ãã¼ã¿ã®æç»ã®ã¿ã«éä¸­ã§ãã
- æå ±æ´æ°ãããç´°ãããªã¢ã«ã¿ã¤ã ã«ããã¤é«éã«
  - åè¿°ã®ä¾ã§ã¯Supabaseã®subscribeã¨çµã¿åããã¦ãDBã«å¤æ´ãå ãã£ããã¹ã¿ãããåãã§ããã
  - ãã¹ããããé¨åçãªã¬ã¤ã¢ã¦ãã®ã¿åãã§ãã(ãã«ãã¼ã¸ã­ã¼ãããªã)
  - å®éã®ãã¼ã¿ãã§ããã¯loaderå´ã§è¡ãã®ã§ãã­ã¸ãã¯ã¯ä¸åé²åºããªã

---

- ã¨ãã¸ã¬ã³ããªã³ã°(Cloudflare Workers)ã«ããæ©æµ
  - ã¼ã­ã³ã¼ã«ãã¹ã¿ã¼ã
    - KVä½¿ããªãã¦ãã200-300msã§å¿ç­ã§ãã(TTFB)
      - åä¸æ§æã® Next.js on Vercel ã®SSRã§300-500ms
    - KVä½¿ãã°SSRã§60-80ms
    - ãã¡ãããã¼ã¿ã½ã¼ã¹ã«å¼ã£å¼µãããã
  - ã¹ã±ã¼ã«ãæ°ã«ããªãã¦è¯ã

---

# è¦ãã¿

- Nested Routeã¯æ³åä»¥ä¸ã«é£æåº¦ãé«ã
  - URLè¨­è¨ã¨ãã£ã¬ã¯ããªè¨­è¨ãã»ããã§è¡ããªããã°ãªããªã
  - è¯ããæªããã­ã¸ãã¯ãåæ£ããè³åã¡ã¢ãªãå§è¿«ãã
  - å®éãã¹ãã¯2éå±¤ãããã«ã¨ã©ãã¦ããã®ããã
    - æåã®ãµã³ãã«ã«ä¸ãããããªæ§æã¯æ­£ç´ç¡ç

---

Workersã«éã£ãè©±ã«ãªããããã
  
- UIã©ã¤ãã©ãªå¥ããã¨1MBã«ãã³ãã«ãµã¤ãºãæããã®ã¯çµæ§ãã¤ã
  - SSRãªã®ã§å¨ã¦ãã³ãã«ããªãã¨ãããªã(ãã£ã³ã¯ãã§ããªã)
  - Service Bindingsãé§ä½¿ãã¦åé¿ãã
- ã¾ã ã¾ã Workeréå¯¾å¿ãªã©ã¤ãã©ãªãå¤ã
  - esbuildã§polyfillããããinjectããããªã©è·äººè¸ãæ±ãããã
  - ããããããããRemixã®ã³ã³ãã¤ã©(esbuild)ã®è¨­å®ã®æ¡å¼µãä¸å¯è½
    - next.config.jsããwebpackã®è¨­å®ããããã¿ãããªæãã®ãã¨ã¯ã§ããªã 
    - æ¡å¼µèªä½ãã³ãã¥ããã£ã®ããªã·ã¼çã«NG (ããã¸ã¡ã³ãã³ã¹ãã¨ãªã¹ã¯ã®åé¡)
      - ä½åº¦ãDiscussionãPRã¯èµ·ç¥¨ããã¦ããããã¨ãã¨ããªã¸ã§ã¯ã
  - æçµçã«èªåã§Remixã®esbuild ãæ¡å¼µå¯è½ã«ãããã©ã°ã¤ã³ãæ¸ãã
    - https://github.com/aiji42/remix-esbuild-override

---

# ç¸æ§ã®è¯ããµã¼ãã¹ããµã¤ã

æ¬¡ã®ãããªã±ã¼ã¹ãªãNext.jsã§å®è£ãããããRemixã§å®è£ããã»ããéçºã³ã¹ãã¯å°ãããªã(ã¨åäººçã«ã¯æã)

---

- React Router ã§æ§ç¯ãããSPAãµã¤ããSSRã«ç§»è¡ããããSEOå¯¾ç­ããã
  - React Routeã®ææ³ããã¼ã¹ã«æ§ç¯ããã¦ãããããå¤§ããæ§é ãå¤ããã«ç§»è¡ã§ãã

- è¤æ°ãã¼ã¸ã«æ¸¡ãã¨ã³ããªã¼ãã©ã¼ã ãç°¡åã«å®è£ããã
  - åè¿°ã®éããremix-validated-formã¨zodã§ç°¡åã«ä½ãã
  - ã¹ãã¼ãã©ã¤ãã©ãªãä¸è¦
  - MVCãªWebãã¬ã¼ã ã¯ã¼ã¯(Rails)ä½¿ã£ã¦ãäººã¯æ¯è¼çã¨ã£ã¤ãããã(ã¨åäººçã«ã¯æã)

- ç®¡çç»é¢ãããã·ã¥ãã¼ãããã«ã¹ã¯ã©ããããã
  - React Adminã®å°å¥ãè©¦ã¿ããããã¼ã¿ã¹ã­ã¼ã ã»ãã¸ãã¹ã­ã¸ãã¯ã«é©ããã¢ããã¿ã¼ããªãã£ããªã©
  - Nested Routes ã¨ remix-validated-form, remix-auth ãé§ä½¿ãã
  - loader/actionãåãã©ã¼ã ããã¼ã¿ãã£ã¼ãã¨1å¯¾1ã§éç½®ããUIã¨ãã¼ã¿ã­ã¸ãã¯ãããããã§åç¸®
    - ãã¹ã¿ããªãã£ã®åä¸ã«ãã¤ãªãã

---

# ã¾ã¨ã

<br>

ãªãã¨è¨ã£ã¦ã  

- Cloudflare Workerã§åã

- Nested routesã®åé§ã
  - ã¬ã¤ã¢ã¦ãã¨ãã¼ã¿ãã§ããã­ã¸ãã¯ã®åæ£ç®¡ç
  - Next.jsã«å½±é¿ãåã¼ãç¨ã®åè¦æ§

<br>

ãã®2ã¤ãåãã¦ãã¦ãããã¾ã§å®æåº¦ã®é«ããã¬ã¼ã ã¯ã¼ã¯ã¯ä»ã«ã¯ããã¾ããã  
ã¡ã¤ã³ã§ä½¿ããã¬ã¼ã ã¯ã¼ã¯ã¨ã¾ã¯ãããªãã¦ããä¸åº¦è©¦ãä¾¡å¤ã¯ããã¨æãã¾ãã

Next.jsã®æ°ããLayoutæ¦ç¥ãGAãããã¾ã§ã®ç´ æ¯ãã¨ãã¦ããè¯ããµã³ãããã¯ã¹ã«ãªãã¨æãã¾ãã

---

# One more thing

## Next.jsã«Remixã®ã¨ãã»ã³ã¹ãåãå¥ãã

---

<div class="flex space-x-4">
<div class="flex-1">

```tsx
import { handle, json, Form, useFormSubmit } from 'next-runtime';

export const getServerSideProps = handle({
  async get() {
    return json({ name: 'smeijer' });
  },
  async post({ req: { body } }) {
    await db.comments.insert(body);

    return json({ message: 'thanks for your comment!' });
  },
});

export default function MyPage({ name, message }) {
  const { isSubmitting } = useFormSubmit();

  if (message) return <p>{message}</p>;
  return (
    <Form method="post">
      <input name="name" defaultValue={name} />
      <input name="message" />
      <button type="submit" disabled={pending}>
        {isSubmitting ? 'submitting' : 'submit'}
      </button>
    </Form>
  );
}
```

</div>

<div class="flex-1">

## next-runtime
https://next-runtime.meijer.ws/getting-started/1-introduction

<img src="https://github.com/smeijer/next-runtime/raw/main/docs/public/banner.png" class="h-20" />

<br>

getServerSidePropsãæ¡å¼µãããªã¯ã¨ã¹ãã¡ã½ãããã¨ã«å®è£ãæ¸ãåãããã¨ãã§ãã  
ãã©ã¼ã ã®ã¢ã¯ã·ã§ã³ãapi routesã«ãããèªãã¹ã«åããã°ãæ¬ä¼¼çãªloader/actionã«ãªã

æ¥½è¦³çUIã®ããã®ãã«ãã¼ãCookieãåãæ±ããã«ãã¼ãªã©ãç¨æããã¦ãããããªãRemixã«ä¼¼ã¦ãã

<small>ã¨ããããRemixãã¤ã³ã¹ãã¤ã¢ããã¦å®è£ããã¨ä½èããã­ã¥ã¡ã³ãã§æè¨ãã¦ãã</small>


</div>
</div>

---

ãã¡ãã®è¨äºã§ãç´¹ä»ãã¦ãã¾ã

<img src="/og-base_z4sxah.png" class="h-70 bg-white" />

https://zenn.dev/aiji42/articles/23a88a7b111694