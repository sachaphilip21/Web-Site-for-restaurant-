# TableDeal Toronto — quick guide

A landing page and directory of partner restaurants in Toronto. Customers pay for their reservation online (with a 10-15% discount), show up at the restaurant, and you pay out the restaurant's share afterward (Groupon-style model).

## 1. Site structure

Just one file: `index.html`. Everything is in it (HTML, styling, content). No server needed, nothing to install — you can even double-click it to preview it in your browser.

## 2. Adding / editing a restaurant

Open `index.html`, find the `const RESTAURANTS = [ ... ]` block near the end of the file. Each restaurant is a block like this:

```js
{
  name: "Nonna Trattoria",
  cuisine: "Italian",
  neighborhood: "King West",
  emoji: "🍝",
  color: "#b23b2e",
  deal: "15% off",
  fullPrice: 50,
  dealPrice: 42.50,
  link: "#"   // <- replace with your Stripe Payment Link (step 3)
}
```

Copy/paste a block, change the values, and a new card automatically appears on the site. To remove a restaurant, delete its block.

## 3. Setting up payments (Stripe Payment Links — no code needed)

Since you're setting up your Stripe account, here's what comes next once it's ready:

1. Log in at [dashboard.stripe.com](https://dashboard.stripe.com).
2. Make sure your account is activated to receive payments (Stripe will ask for your name, address, and a bank account for payouts — an "individual / sole proprietor" account is enough to get started, no incorporation needed).
3. In the menu, go to **Products → Payment Links**.
4. Click **+ Create payment link**.
5. Create one product per deal, e.g., name = "Nonna Trattoria — $50 credit (15% off)", price = $42.50 CAD.
6. Once created, Stripe gives you a URL (e.g. `https://buy.stripe.com/xxxxx`). Copy it.
7. Paste that URL into the `link:` field of the matching restaurant in `index.html`.

Repeat for each restaurant/deal. Since each link is unique per restaurant, you'll know exactly who paid for what just by checking your Stripe Dashboard (Payments section) — no real backend required.

## 4. Tracking the money and paying restaurant owners

Since payments flow through you, here's how to organize it:

- **Every week (or every month)**: go to your Stripe Dashboard, filter payments by link/product (i.e. by restaurant).
- Add up the total collected for that restaurant over the period.
- Calculate their share: `total collected − your commission = amount to pay out`.
- Pay out that amount via e-transfer or bank transfer.
- Keep a simple record (a Google Sheet is fine to start) with columns: Restaurant | Period | Total collected | Your commission | Amount paid out | Payment date.

This is the same principle Groupon used in its early days: you handle the money and the customer relationship, the restaurant just has to honor the reservations.

## 5. Publishing the site (GitHub Pages — free)

1. In GitHub Desktop, make sure `index.html` is committed and pushed to GitHub.
2. Go to the repository page on GitHub.com (the "View on GitHub" button in GitHub Desktop).
3. **Settings → Pages** tab.
4. Under "Branch", choose `main` and the `/ (root)` folder, then **Save**.
5. After a minute or two, GitHub gives you an address like `https://yourusername.github.io/Web-Site-for-restaurant`. That's your live site, ready to share on your calls.

## 6. Legal points to keep in mind (not legal advice)

Since customer money passes through you before reaching the restaurant owner, it's recommended to:
- Check with an accountant about when you need to register for GST/HST (mandatory once you pass $30,000 in revenue over 12 months in Canada).
- Have a simple written agreement with each restaurant owner (discount offered, commission %, payout frequency, no-show/cancellation policy).
- Set a clear refund policy in case a customer can't make their reservation.

This isn't legal or tax advice — it's worth checking with an accountant or lawyer before scaling up.
