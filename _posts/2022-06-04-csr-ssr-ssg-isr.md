---
title: CSR, SSR, SSG and ISR
author: Sanh Doan
date: 2022-06-04 11:00:00 +0700
categories: [Frontend]
tags: [Frontend, NextJS]
---

## SSR - Server side rendering

- The HTML is generated on each request (run-time)

## SSG - Static side generate

- The HTML is generated at build-time and is reused for each request.
- Use CDN for serving static file faster <br />

<img src="/assets/img/pages/ssg.png" style="max-width:600px" width="100%">

## CSR - Client side rendering

- Server returns JS file, and HTML is rendered from browser
- Usually: SSG without Data + Fetch data on Client-side

## ISR: Incremental Static Regeneration

- Use case:
  - There are 1 million products, but we can not generate 1 million static files (long build time)
  - We generate 1,000 static files for 1,000 common products
  - For the rest, when user access a page, it will use SSR for the first time, then also generate static file so that the next request can use SSG

## More notes

- Use case:
  - SSG + CSR: private web (dashboard, admin tools,...)
  - SSG/ISR: public web (e-commerce, blog,...)
- In NextJS, you can choose which pre-rendering form to use for each page

|  #  |   Name    |                                 Description                                 |
| :-: | :-------: | :-------------------------------------------------------------------------: |
|  1  |  Static   |        Automatically rendered as static HTML (uses no initial props)        |
|  2  |    SSG    |     automatically generated as static HTML + JSON (uses getStaticProps)     |
|  3  |    ISR    |     incremental static regeneration (uses revalidate in getStaticProps)     |
|  4  | SSG + CSR |      pre-rendered HTML + data fetching on client side using useEffect       |
|  5  |    SSR    | server-side renders at runtime (uses getInitialProps or getServerSideProps) |
