---
title: Introduction
excerpt: Find out what Control D is, and what it can do for you.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - slug: use-cases
      title: Use Cases
      type: basic
---
```html Banner HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Summer Sale</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: #F0F0F0;
            font-family: 'Arial', sans-serif;
        }
        .ad-container {
            width: 568px;
            height: 328px;
            background-image: url('https://images.pexels.com/photos/996329/pexels-photo-996329.jpeg?auto=compress&cs=tinysrgb&w=568&h=328&fit=crop');
            background-size: cover;
            background-position: center;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            align-items: center;
            padding: 50px 40px;
            text-align: center;
            position: relative;
        }
        .content-overlay {
            background: rgba(255, 255, 255, 0.9);
            padding: 40px 30px;
            border-radius: 12px;
            backdrop-filter: blur(10px);
        }
        .header {
            color: #000000ff;
            font-size: 48px;
            font-weight: bold;
            margin-bottom: 20px;
            line-height: 1.2;
        }
        .body-text {
            color: #000000ff;
            font-size: 18px;
            line-height: 1.5;
            margin-bottom: 30px;
            max-width: 300px;
        }
        .cta-button {
            background-color: transparent;
            color: #000000ff;
            border: 2px solid #000000ff;
            padding: 15px 35px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.3s;
        }
        .cta-button:hover {
            background-color: #000000ff;
            color: #FFFFFF;
        }
        .cta-button:active {
            transform: scale(0.98);
        }
    </style>
</head>
<body>
    <div class="ad-container">
        <div class="content-overlay">
            <h1 class="header">Sale 50% off</h1>
            <p class="body-text">Only until this Friday, all clothes are discounted to celebrate the start of summer</p>
            <button class="cta-button">Browse sale</button>
        </div>
    </div>
</body>
</html>
```
