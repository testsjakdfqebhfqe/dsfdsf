---
title: example
deprecated: true
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<style>
  .mig-slot-preview, .mig-slot-preview * {
    box-sizing: border-box;
  }
  .mig-slot-preview {
    width: 100%;
    max-width: 410px;
    min-height: 568px;
    margin: 0 auto;
    background: #F0F0F0;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    border-radius: 12px;
  }
  .mig-slot-preview__container {
    width: 328px;
    min-height: 568px;
    background-image: url('https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExbXh1YXdieHlwOGxtdjNtbmZ4YWcxZGd1OGRreWFmczF2aTkyOGE2bCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3HpSslnzl7mKx0Yzhi/giphy.gif');
    background-size: cover;
    background-position: center;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    padding: 50px;
    text-align: center;
    position: relative;
  }
  .mig-slot-preview__header {
    font-family: Georgia, serif;
    font-size: 64px;
    font-weight: bold;
    color: #000000;
    margin: 0 0 20px;
    text-shadow: 2px 2px 4px rgba(255, 255, 255, 0.8);
  }
  .mig-slot-preview__button {
    color: #000000;
    border: 2px solid #000000;
    padding: 18px 40px;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
    border-radius: 8px;
    transition: all 0.3s;
    backdrop-filter: blur(5px);
    background: rgba(255, 255, 255, 0.8);
  }
  .mig-slot-preview__button:hover {
    background-color: #000000;
    color: #FFFFFF;
    transform: translateY(-2px);
  }
  .mig-slot-preview__button:active {
    transform: translateY(0);
  }
</style>

<div class="mig-slot-preview">
  <div class="mig-slot-preview__container">
    <h1 class="mig-slot-preview__header">50% off</h1>
    <button class="mig-slot-preview__button">Browse winterwear </button>
  </div>
</div>
