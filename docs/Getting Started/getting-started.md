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
    - type: basic
      slug: use-cases
      title: Use Cases
---
```html
<style>
  .mig-banner-preview, .mig-banner-preview * {
    box-sizing: border-box;
  }
  .mig-banner-preview {
    width: 100%;
    max-width: 760px;
    min-height: 360px;
    margin: 0 auto;
    background: #F0F0F0;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    border-radius: 12px;
  }
  .mig-banner-preview__container {
    width: 100%;
    min-height: 328px;
    background-image: url('https://images.pexels.com/photos/996329/pexels-photo-996329.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&fit=crop');
    background-size: cover;
    background-position: center;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    padding: 30px 20px;
    text-align: center;
    position: relative;
  }
  .mig-banner-preview__overlay {
    background: rgba(255, 255, 255, 0.9);
    padding: 24px 30px;
    border-radius: 12px;
    backdrop-filter: blur(10px);
  }
  .mig-banner-preview__header {
    color: #000000;
    font-family: Arial, sans-serif;
    font-size: 48px;
    font-weight: bold;
    margin: 0 0 20px;
    line-height: 1.2;
  }
  .mig-banner-preview__body {
    color: #000000;
    font-family: Arial, sans-serif;
    font-size: 18px;
    line-height: 1.5;
    margin: 0 0 30px;
    max-width: 300px;
  }
  .mig-banner-preview__button {
    background-color: transparent;
    color: #000000;
    border: 2px solid #000000;
    padding: 15px 35px;
    font-family: Arial, sans-serif;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    border-radius: 8px;
    transition: all 0.3s;
  }
  .mig-banner-preview__button:hover {
    background-color: #000000;
    color: #FFFFFF;
  }
  .mig-banner-preview__button:active {
    transform: scale(0.98);
  }
</style>
<div class="mig-banner-preview">
  <div class="mig-banner-preview__container">
    <div class="mig-banner-preview__overlay">
      <h1 class="mig-banner-preview__header">Sale 50% off</h1>
      <p class="mig-banner-preview__body">Only {user.LB} until this Friday, all clothes are discounted to celebrate the start of summer</p>
      <button class="mig-banner-preview__button">Browse sale</button>
    </div>
  </div>
</div>
```

<HTMLBlock>{`
<style>
  .mig-banner-preview, .mig-banner-preview * {
    box-sizing: border-box;
  }
  .mig-banner-preview {
    width: 100%;
    max-width: 760px;
    min-height: 360px;
    margin: 0 auto;
    background: #F0F0F0;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    border-radius: 12px;
  }
  .mig-banner-preview__container {
    width: 100%;
    min-height: 328px;
    background-image: url('https://images.pexels.com/photos/996329/pexels-photo-996329.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&fit=crop');
    background-size: cover;
    background-position: center;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    padding: 30px 20px;
    text-align: center;
    position: relative;
  }
  .mig-banner-preview__overlay {
    background: rgba(255, 255, 255, 0.9);
    padding: 24px 30px;
    border-radius: 12px;
    backdrop-filter: blur(10px);
  }
  .mig-banner-preview__header {
    color: #000000;
    font-family: Arial, sans-serif;
    font-size: 48px;
    font-weight: bold;
    margin: 0 0 20px;
    line-height: 1.2;
  }
  .mig-banner-preview__body {
    color: #000000;
    font-family: Arial, sans-serif;
    font-size: 18px;
    line-height: 1.5;
    margin: 0 0 30px;
    max-width: 300px;
  }
  .mig-banner-preview__button {
    background-color: transparent;
    color: #000000;
    border: 2px solid #000000;
    padding: 15px 35px;
    font-family: Arial, sans-serif;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    border-radius: 8px;
    transition: all 0.3s;
  }
  .mig-banner-preview__button:hover {
    background-color: #000000;
    color: #FFFFFF;
  }
  .mig-banner-preview__button:active {
    transform: scale(0.98);
  }
</style>
<div class="mig-banner-preview">
  <div class="mig-banner-preview__container">
    <div class="mig-banner-preview__overlay">
      <h1 class="mig-banner-preview__header">Sale 50% off</h1>
      <p class="mig-banner-preview__body">Only {user.LB} until this Friday, all clothes are discounted to celebrate the start of summer</p>
      <button class="mig-banner-preview__button">Browse sale</button>
    </div>
  </div>
</div>
`}</HTMLBlock>
