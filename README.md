# PriceWise

Track Amazon product prices and get notified when they drop.

## What it does

Paste an Amazon product link, and PriceWise will scrape the current price and keep tracking it over time. You can sign up with your email to get alerts when:

- The price hits an all-time low
- A product comes back in stock
- The discount crosses 40%

## Tech Stack

- **Next.js 16** with App Router
- **MongoDB** + Mongoose for storing products and price history
- **Cheerio** for scraping Amazon product pages
- **Nodemailer** for email notifications
- **Tailwind CSS** for styling
- **Headless UI** for the modal component
- **BrightData** proxy for reliable scraping

## Getting Started

1. Clone the repo

```bash
git clone https://github.com/SaurabPoudel/ecommerce-scrape.git
cd ecommerce-scrape
```

2. Install dependencies

```bash
npm install
```

3. Create a `.env` file in the root with these variables:

```
MONGODB_URI=your_mongodb_connection_string
BRIGHT_DATA_USERNAME=your_brightdata_username
BRIGHT_DATA_PASSWORD=your_brightdata_password
EMAIL_PASSWORD=your_email_app_password
```

4. Run the dev server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) and you should be good to go.

## Project Structure

```
├── app/
│   ├── api/cron/        # Cron job to re-scrape all products
│   ├── products/[id]/   # Product detail page
│   ├── layout.tsx
│   └── page.tsx         # Home page with search + trending
├── components/          # Navbar, Searchbar, Modal, Cards
├── lib/
│   ├── actions/         # Server actions (scrape, fetch, email)
│   ├── models/          # Mongoose product schema
│   ├── scraper/         # Amazon scraping logic
│   ├── nodemailer/      # Email templates + sending
│   ├── mongoose.ts      # DB connection
│   └── utils.ts         # Price helpers, extractors
└── types/               # TypeScript interfaces
```

## How the cron works

Hit `GET /api/cron` (e.g. via Vercel Cron or any scheduler) and it will:

1. Fetch all tracked products from the DB
2. Re-scrape each one for the latest price
3. Update price history, lowest/highest/average
4. Send email alerts if any thresholds are met

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server (Turbopack) |
| `npm run dev:webpack` | Start dev server (Webpack) |
| `npm run build` | Production build |
| `npm run start` | Start production server |