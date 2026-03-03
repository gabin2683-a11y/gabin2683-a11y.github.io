[steps (1).md](https://github.com/user-attachments/files/25708612/steps.1.md)
# GitHub Homepage with Crypto Price Table

## Step 1: Create a GitHub Account
1. Go to [github.com](https://github.com) and click **Sign up**
2. Enter your email, create a password, and choose a username
3. Verify your email address to activate the account

## Step 2: Create a GitHub Pages Homepage
1. Log in to GitHub and click **+** (top right) → **New repository**
2. Name the repository exactly: `[username].github.io` (e.g. `gabin2683-a11y.github.io`)
3. Set visibility to **Public** and check **Add a README file**
4. Click **Create repository**
5. In the repository, click **Add file** → **Create new file**
6. Name the file `index.html` and add basic HTML content
7. Click **Commit changes**
8. Go to **Settings** → **Pages** → set Source to **main branch** → Save
9. Your site will be live at `https://[username].github.io`

## Step 3: Add a Crypto Price Table Using CoinGecko

### Current Prices (fetched from CoinGecko on 2026-03-03)

| Coin       | Symbol | Price (USD)  |
|------------|--------|--------------|
| Bitcoin    | BTC    | $85,000      |
| Ethereum   | ETH    | $2,033.65    |

### How to fetch prices from CoinGecko API
The CoinGecko API endpoint used:
```
https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd
```

This returns JSON like:
```json
{
  "bitcoin": { "usd": 85000 },
  "ethereum": { "usd": 2033.65 }
}
```

## Step 4: Real-Time Auto-Updating Price Table

The `index.html` file uses JavaScript to:
1. Call the CoinGecko API every **30 seconds**
2. Parse the JSON response
3. Update the table cells with the latest prices
4. Show a **last updated** timestamp

The key JavaScript logic:
```javascript
async function fetchPrices() {
  const response = await fetch(
    'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd'
  );
  const data = await response.json();
  document.getElementById('btc-price').textContent = '$' + data.bitcoin.usd.toLocaleString();
  document.getElementById('eth-price').textContent = '$' + data.ethereum.usd.toLocaleString();
}

setInterval(fetchPrices, 30000); // update every 30 seconds
fetchPrices(); // run immediately on load
```

## Files in this Repository

| File         | Description                              |
|--------------|------------------------------------------|
| `index.html` | Homepage with real-time crypto price table |
| `steps.md`   | This documentation file                  |
| `steps.html` | HTML version of this documentation       |
