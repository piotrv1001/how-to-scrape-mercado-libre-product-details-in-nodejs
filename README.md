# How to Scrape Mercado Libre Product Details in Node.js

This example shows how to scrape Mercado Libre product pages from Node.js using the [Mercado Libre Product Details Scraper](https://apify.com/piotrv1001/mercado-libre-product-details-scraper) Actor on Apify. It uses the existing Actor rather than implementing marketplace requests or parsing locally.

## What this example does

- Calls `piotrv1001/mercado-libre-product-details-scraper`
- Passes product URLs from two regional sites
- Waits for the Actor run to finish
- Fetches the run's dataset
- Prints each localized product record

## Prerequisites

- [Node.js](https://nodejs.org) 18 or newer
- An [Apify account](https://console.apify.com/sign-up)
- An Apify API token from **Settings → Integrations**

## Installation

```bash
npm install
```

## Environment setup

```bash
cp .env.example .env
```

Add your token to `.env`:

```env
APIFY_TOKEN=your_apify_token_here
```

## Usage

```bash
npm start
```

## Code example

```js
import { ApifyClient } from 'apify-client';
import 'dotenv/config';

// Initialize the ApifyClient with your Apify API token
// Set APIFY_TOKEN in your .env file (copy .env.example to get started)
const client = new ApifyClient({
    token: process.env.APIFY_TOKEN,
});

// Prepare Actor input
const input = {
    productUrls: [
        'https://www.mercadolibre.com.ar/apple-iphone-15-128-gb-azul/p/MLA27172667',
        'https://www.mercadolivre.com.br/apple-iphone-15-128-gb-preto/p/MLB27172667',
    ],
    maxItems: 50,
};

// Run the Actor and wait for it to finish
const run = await client.actor('piotrv1001/mercado-libre-product-details-scraper').call(input);

// Fetch and print Actor results from the run's dataset (if any)
console.log('Results from dataset');
console.log(`💾 Check your data here: https://console.apify.com/storage/datasets/${run.defaultDatasetId}`);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach((item) => {
    console.dir(item);
});

// 📚 Want to learn more 📖? Go to → https://docs.apify.com/api/client/js/docs
```

## Example output

[`sample-output.json`](./sample-output.json) contains abbreviated Argentina and Brazil records from September 15, 2026. Key fields include site and currency, price and installments, stock and fulfilment, seller reputation, sibling variations, specifications, ratings, and top review samples.

## Use cases

- Compare localized offers across Mercado Libre country sites
- Track price, installment, stock, and seller changes
- Enrich catalogs with localized descriptions and specifications
- Monitor who holds the current product-page offer
- Follow sibling colour, size, or storage URLs

## Try the Actor on Apify

**[Open the Mercado Libre Product Details Scraper on Apify](https://apify.com/piotrv1001/mercado-libre-product-details-scraper)**

## Related resources

- [How to Scrape Mercado Libre Product Details Across Latin America](https://www.falconscrape.com/blog/how-to-scrape-mercado-libre-product-details)
- [Mercado Libre Listings Scraper](https://apify.com/piotrv1001/mercado-libre-listings-scraper)
- [Apify JavaScript client documentation](https://docs.apify.com/api/client/js/docs)

## License

MIT
