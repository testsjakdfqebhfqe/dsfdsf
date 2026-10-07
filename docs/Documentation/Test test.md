---
title: Welcome to Taurus
deprecated: false
hidden: false
icon: 👍
metadata:
  robots: index
---
Welcome to the Taurus Platform Integration documentation. You will find all required information to understand and use our products  structured along the four main blocks below.

1. Documentation Overview
2. User Guides
3. API reference
4. SDK

Note that User Guides access is password protected and only available to clients.

Enjoy and have fun!

***

<br />

<HTMLBlock>{`
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Docs Grid – Taurus Style</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #ffffff;
      --bg-soft: #f6f6f8;
      --card-bg: #ffffff;
      --border: #e4e4ea;
      --text: #1b1b23;
      --text-muted: #7a7a8a;
      --accent-pink: #e192ed;
      --accent-pink-soft: #fbe9ff;
      --shadow-soft: 0 14px 30px rgba(15, 15, 30, 0.08);
      --radius-card: 24px;
    }

    * {
      box-sizing: border-box;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text", "Inter", sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .wrapper {
      width: 80%;
      max-width: 980px;
      padding: 2.5rem 1.5rem;
      margin: 0 auto;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 1.75rem;
    }

    .card {
      background: var(--card-bg);
      border-radius: var(--radius-card);
      overflow: hidden;
      border: 1px solid var(--border);
      box-shadow: var(--shadow-soft);
      cursor: pointer;
      transition:
        transform 160ms ease-out,
        box-shadow 160ms ease-out,
        border-color 160ms ease-out,
        background 160ms ease-out;
    }

    .card:hover {
      transform: translateY(-4px);
      box-shadow: 0 18px 40px rgba(15, 15, 30, 0.12);
      border-color: rgba(225, 146, 237, 0.7);
      background: linear-gradient(135deg, #ffffff, var(--accent-pink-soft));
    }

    .card a {
      color: inherit;
      text-decoration: none;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 0.5rem;
    }

    /* Image area for cards (fixed aspect ratio, responsive width) */
    .card-image {
      width: 80%;
      aspect-ratio: 16 / 9;
      background-color: #f7f5fc;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .card-image-inner-overview,
    .card-image-inner,
    .card-image-inner-api,
    .card-image-inner-sdk {
      width: 80%;
      height: 80%;
      border-radius: 18px;
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
    }

    .card-image-inner-overview {
      background-image: url("https://files.readme.io/6410cea97b056ce2aa0a92b99d96e553c37ae9f7911b1dec1db948eab6733519-2026_Taurus.jpg");
    }

    .card-image-inner {
      background-image: url("https://www.taurushq.com/img/hero-home.webp");
    }

    .card-image-inner-api {
      background-image: url("https://files.readme.io/e44e6a515e0f528c1389ecdcb0979ceadaa9815cd58b2af8a0a1397ecbb24792-generated-image.png");
    }

    .card-image-inner-sdk {
      background-image: url("https://files.readme.io/cc5e43be3eeca7058da33999d94c75e04ebb4dc316999c198cb664404005b972-2026_SDK.png");
    }

    .card-body {
      padding: 1rem 1.4rem 1.1rem;
    }

    .card-title {
      font-size: 0.98rem;
      font-weight: 500;
    }

    .card-sub {
      margin-top: 0.1rem;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .card-arrow {
      flex-shrink: 0;
      width: 28px;
      height: 28px;
      border-radius: 999px;
      border: 1px solid rgba(225, 146, 237, 0.6);
      background: linear-gradient(135deg, var(--accent-pink-soft), #ffffff);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.9rem;
      color: var(--accent-pink);
    }

    /* RESPONSIVE ADJUSTMENTS */

    /* Stack cards in one column on tablets/phones used to be 780 */
    @media (max-width: 750px) {
      body {
        align-items: flex-start;
      }

      .wrapper {
        padding: 1.5rem 1rem 2rem;
      }

      .grid {
        grid-template-columns: minmax(0, 1fr);
      }

      .card a {
        align-items: flex-start;
      }
    }

    /* Tighter layout on very small phones used to be 480 */
    @media (max-width: 480x) {
      .wrapper {
        padding: 1.25rem 0.75rem 1.75rem;
      }

      .card-body {
        padding: 0.9rem 1rem 1rem;
      }

      .card-title {
        font-size: 0.9rem;
      }

      .card-sub {
        font-size: 0.78rem;
      }
    }
  </style>
</head>
<body>
  <main class="wrapper">
    <section class="grid">
      <!-- Taurus Overview -->
      <article class="card">
        <div class="card-image">
          <div class="card-image-inner-overview"></div>
        </div>
        <div class="card-body">
          <a href="https://docs.taurushq.com/protect-capital/docs/taurus-platform-capabilities">
            <div>
              <div class="card-title">Documentation Overview</div>
              <div class="card-sub">Security principles, architecture, and wallet overview</div>
            </div>
            <div class="card-arrow">›</div>
          </a>
        </div>
      </article>

      <!-- User Guide -->
      <article class="card">
        <div class="card-image">
          <div class="card-image-inner"></div>
        </div>
        <div class="card-body">
          <a href="https://docs.taurushq.com/user-guides/docs/introduction">
            <div>
              <div class="card-title">User Guides</div>
              <div class="card-sub">Master Taurus products through our detailed user guide</div>
            </div>
            <div class="card-arrow">›</div>
          </a>
        </div>
      </article>

      <!-- API Reference -->
      <article class="card">
        <div class="card-image">
          <div class="card-image-inner-api"></div>
        </div>
        <div class="card-body">
          <a href="https://docs.taurushq.com/protect-capital/reference/api">
            <div>
              <div class="card-title">API Reference</div>
              <div class="card-sub">API endpoints and detailed API examples</div>
            </div>
            <div class="card-arrow">›</div>
          </a>
        </div>
      </article>

      <!-- SDK -->
      <article class="card">
        <div class="card-image">
          <div class="card-image-inner-sdk"></div>
        </div>
        <div class="card-body">
          <a href="https://docs.taurushq.com/protect-capital/page/sdk-reference">
            <div>
              <div class="card-title">SDK</div>
              <div class="card-sub">Java, Go, Python SDKs and much more</div>
            </div>
            <div class="card-arrow">›</div>
          </a>
        </div>
      </article>
    </section>
  </main>
</body>
</html>
`}</HTMLBlock>

<br />

Should you require any assistance or have questions about this documentation, do not hesitate to [submit a support request. ](https://customer.support.taurushq.com/servicedesk/customer/portals).
