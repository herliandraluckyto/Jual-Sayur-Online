[sayurOnline.html](https://github.com/user-attachments/files/31872944/sayurOnline.html)<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, viewport-fit=cover">
<title>SegarKu — Toko Sayur</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --green: #00E640;
    --green-deep: #0BA83F;
    --green-dark: #05341A;
    --ink: #10241A;
    --bg: #F4FAF5;
    --surface: #FFFFFF;
    --accent: #FF7A3D;
    --muted: #6B8577;
    --border: #E3EFE6;
    --radius-lg: 26px;
    --radius-md: 18px;
    --radius-sm: 12px;
    --shadow-soft: 0 10px 30px -12px rgba(5,52,26,.18);
    --shadow-card: 0 6px 18px -8px rgba(5,52,26,.14);
    --safe-bottom: env(safe-area-inset-bottom, 0px);
    color-scheme: light;
  }
  html.dark{
    --ink: #EAF5EC;
    --bg: #08150D;
    --surface: #0F2317;
    --border: #1B3A26;
    --muted: #7FA890;
    --shadow-soft: 0 10px 30px -12px rgba(0,0,0,.5);
    --shadow-card: 0 6px 18px -8px rgba(0,0,0,.45);
    color-scheme: dark;
  }
  *{box-sizing:border-box; margin:0; padding:0; -webkit-tap-highlight-color:transparent;}
  html,body{height:100%;}
  body{
    font-family:'Plus Jakarta Sans', system-ui, sans-serif;
    background:#DCEFE0;
    color:var(--ink);
    display:flex; justify-content:center;
    min-height:100vh;
    transition:background .3s ease, color .3s ease;
  }
  html.dark body{ background:#020806; }
  button{font-family:inherit; border:none; background:none; cursor:pointer; color:inherit;}
  input,select{font-family:inherit;}
  img{display:block;}
  a{color:inherit; text-decoration:none;}

  #app-shell{
    width:100%; max-width:460px;
    min-height:100vh;
    background:var(--bg);
    position:relative;
    overflow-x:hidden;
    box-shadow:var(--shadow-soft);
    display:flex; flex-direction:column;
  }

  /* ---------- Top App Header ---------- */
  .app-header{
    position:sticky; top:0; z-index:40;
    background:linear-gradient(180deg, var(--green) 0%, var(--green-deep) 100%);
    padding:18px 20px 22px;
    border-radius:0 0 28px 28px;
    color:#04240F;
    box-shadow:0 8px 24px -10px rgba(0,150,60,.45);
  }
  .header-top{ display:flex; align-items:center; justify-content:space-between; gap:12px; }
  .greeting{ display:flex; flex-direction:column; gap:2px; }
  .greeting .hi{ font-size:13px; font-weight:500; opacity:.85; }
  .greeting .name{ font-size:19px; font-weight:800; letter-spacing:-.2px; }
  .header-icons{ display:flex; gap:10px; }
  .icon-btn{
    width:42px; height:42px; border-radius:14px;
    background:rgba(255,255,255,.28);
    backdrop-filter:blur(6px);
    display:flex; align-items:center; justify-content:center;
    position:relative; flex-shrink:0;
    transition:transform .15s ease, background .15s ease;
  }
  .icon-btn:active{ transform:scale(.9); background:rgba(255,255,255,.42); }
  .icon-btn svg{ width:20px; height:20px; }
  .badge{
    position:absolute; top:-4px; right:-4px;
    background:var(--accent); color:#fff;
    font-size:10px; font-weight:800;
    min-width:18px; height:18px; border-radius:9px;
    display:flex; align-items:center; justify-content:center;
    padding:0 4px;
    border:2px solid var(--green);
  }
  .header-search{
    margin-top:16px; display:flex; align-items:center; gap:8px;
    background:rgba(255,255,255,.9);
    border-radius:16px; padding:12px 14px;
  }
  html.dark .header-search{ background:rgba(8,20,12,.85); }
  .header-search input{
    border:none; outline:none; background:transparent; flex:1;
    font-size:14px; color:var(--ink); font-weight:500;
  }
  .header-search svg{ width:18px; height:18px; color:var(--muted); flex-shrink:0; }

  .page-title-header{
    padding:20px 20px 16px;
  }
  .page-title-header h1{ font-size:22px; font-weight:800; letter-spacing:-.3px; }
  .page-title-header p{ font-size:13px; color:var(--muted); margin-top:2px; font-weight:500; }

  #view-container{
    flex:1; overflow-y:auto; -webkit-overflow-scrolling:touch;
    padding-bottom:calc(96px + var(--safe-bottom));
    position:relative;
  }
  .view{ display:none; animation:viewIn .32s cubic-bezier(.22,.61,.36,1); }
  .view.active{ display:block; }
  @keyframes viewIn{
    from{ opacity:0; transform:translateY(10px); }
    to{ opacity:1; transform:translateY(0); }
  }

  #pull-indicator{
    display:flex; align-items:center; justify-content:center;
    height:0; overflow:hidden; color:var(--green-deep); font-size:12px; font-weight:700;
    transition:height .18s ease;
    gap:6px;
  }
  .spinner{
    width:16px; height:16px; border-radius:50%;
    border:2px solid var(--border); border-top-color:var(--green-deep);
    animation:spin .7s linear infinite;
  }
  @keyframes spin{ to{ transform:rotate(360deg); } }

  .section{ padding:20px 20px 4px; }
  .section-head{ display:flex; align-items:baseline; justify-content:space-between; margin-bottom:14px; }
  .section-head h2{ font-size:17px; font-weight:800; letter-spacing:-.2px; }
  .section-head .link{ font-size:12.5px; font-weight:700; color:var(--green-deep); }

  /* ---------- Banner slider ---------- */
  .banner-wrap{ padding:18px 20px 4px; }
  .banner-track{ position:relative; border-radius:var(--radius-lg); overflow:hidden; box-shadow:var(--shadow-card); }
  .banner-slides{ display:flex; transition:transform .5s cubic-bezier(.65,0,.35,1); }
  .banner-slide{
    min-width:100%; padding:26px 22px; display:flex; flex-direction:column; gap:6px; justify-content:center;
    min-height:128px; position:relative; overflow:hidden;
  }
  .banner-slide::after{
    content:''; position:absolute; right:-30px; bottom:-40px; width:150px; height:150px; border-radius:50%;
    background:rgba(255,255,255,.14);
  }
  .banner-slide .tag{ font-size:11.5px; font-weight:700; color:rgba(255,255,255,.92); }
  .banner-slide h3{ font-size:19px; font-weight:800; color:#fff; max-width:76%; line-height:1.25; }
  .banner-slide p{ font-size:12.5px; color:rgba(255,255,255,.88); margin-top:2px; max-width:70%; }
  .banner-dots{ position:absolute; bottom:12px; left:22px; display:flex; gap:5px; z-index:2; }
  .banner-dots span{ width:6px; height:6px; border-radius:50%; background:rgba(255,255,255,.5); transition:width .25s ease, background .25s ease; }
  .banner-dots span.on{ width:16px; border-radius:4px; background:#fff; }

  .cat-row{ display:flex; gap:14px; overflow-x:auto; padding:4px 20px 6px; scrollbar-width:none; }
  .cat-row::-webkit-scrollbar{ display:none; }
  .cat-item{ display:flex; flex-direction:column; align-items:center; gap:7px; flex-shrink:0; width:64px; }
  .cat-circle{
    width:56px; height:56px; border-radius:18px; background:var(--surface);
    display:flex; align-items:center; justify-content:center; font-size:24px;
    box-shadow:var(--shadow-card); border:2px solid transparent;
    transition:transform .15s ease, border-color .15s ease;
  }
  .cat-item.active .cat-circle{ border-color:var(--green); background:#E8FBEC; }
  html.dark .cat-item.active .cat-circle{ background:#123420; }
  .cat-item:active .cat-circle{ transform:scale(.92); }
  .cat-item span{ font-size:11px; font-weight:700; color:var(--muted); text-align:center; }
  .cat-item.active span{ color:var(--green-dark); }
  html.dark .cat-item.active span{ color:var(--green); }

  .product-grid{ display:grid; grid-template-columns:1fr 1fr; gap:14px; padding:16px 20px 8px; }
  .product-card{
    background:var(--surface); border-radius:var(--radius-md); padding:12px;
    box-shadow:var(--shadow-card); position:relative;
    display:flex; flex-direction:column; gap:8px;
    transition:transform .15s ease;
  }
  .product-card:active{ transform:scale(.97); }
  .product-media{
    border-radius:var(--radius-sm); aspect-ratio:1/1; display:flex; align-items:center; justify-content:center;
    font-size:44px; position:relative; overflow:hidden;
  }
  .fav-btn{
    position:absolute; top:8px; right:8px; width:32px; height:32px; border-radius:11px;
    background:rgba(255,255,255,.92); display:flex; align-items:center; justify-content:center;
    box-shadow:0 4px 10px rgba(0,0,0,.12); transition:transform .18s ease;
  }
  .fav-btn svg{ width:16px; height:16px; stroke:var(--muted); fill:none; transition:fill .18s ease, stroke .18s ease; }
  .fav-btn.active svg{ fill:#FF4D6D; stroke:#FF4D6D; }
  .fav-btn:active{ transform:scale(.85); }
  .stock-tag{
    position:absolute; left:8px; top:8px; background:rgba(5,52,26,.55); color:#fff; font-size:10px; font-weight:700;
    padding:3px 8px; border-radius:8px; backdrop-filter:blur(3px);
  }
  .product-name{ font-size:14px; font-weight:700; letter-spacing:-.1px; }
  .product-desc{ font-size:11.5px; color:var(--muted); font-weight:500; line-height:1.35; min-height:15px; }
  .product-bottom{ display:flex; align-items:flex-end; justify-content:space-between; margin-top:2px; }
  .product-price{ font-size:14px; font-weight:800; color:var(--accent); }
  .product-price small{ font-size:10px; color:var(--muted); font-weight:600; display:block; }
  .add-btn{
    width:34px; height:34px; border-radius:11px; background:var(--green); color:var(--green-dark);
    display:flex; align-items:center; justify-content:center; flex-shrink:0; box-shadow:0 6px 14px -6px rgba(0,180,60,.6);
  }
  .add-btn svg{ width:17px; height:17px; }
  .add-btn.bounce{ animation:bounceAdd .32s ease; }
  @keyframes bounceAdd{ 0%{transform:scale(1);} 40%{transform:scale(.78);} 70%{transform:scale(1.12);} 100%{transform:scale(1);} }

  .skeleton{ background:linear-gradient(100deg, var(--border) 30%, #EFF7F1 45%, var(--border) 60%); background-size:200% 100%; animation:shimmer 1.3s ease-infinite; border-radius:var(--radius-sm); }
  html.dark .skeleton{ background:linear-gradient(100deg, #123420 30%, #1b4a2c 45%, #123420 60%); background-size:200% 100%; }
  @keyframes shimmer{ 0%{background-position:200% 0;} 100%{background-position:-200% 0;} }
  .sk-card{ background:var(--surface); border-radius:var(--radius-md); padding:12px; box-shadow:var(--shadow-card); }
  .sk-media{ aspect-ratio:1/1; border-radius:var(--radius-sm); margin-bottom:10px; }
  .sk-line{ height:10px; border-radius:6px; margin-bottom:6px; }

  /* ---------- Produk page filter bar ---------- */
  .filter-bar{ display:flex; gap:8px; padding:2px 20px 14px; overflow-x:auto; scrollbar-width:none; }
  .filter-bar::-webkit-scrollbar{ display:none; }
  .chip{
    flex-shrink:0; padding:9px 15px; border-radius:12px; font-size:12.5px; font-weight:700;
    background:var(--surface); color:var(--muted); box-shadow:var(--shadow-card); display:flex; align-items:center; gap:5px;
  }
  .chip.active{ background:var(--green); color:var(--green-dark); }
  .sort-select{
    margin-left:20px; margin-right:20px; margin-bottom:6px; padding:10px 12px; border-radius:12px; font-size:12.5px; font-weight:700;
    background:var(--surface); color:var(--ink); box-shadow:var(--shadow-card); border:none; width:calc(100% - 40px);
  }

  .empty-state{ display:flex; flex-direction:column; align-items:center; text-align:center; padding:70px 30px; gap:14px; }
  .empty-illustration{
    width:110px; height:110px; border-radius:32px; background:linear-gradient(160deg,#E8FBEC,#D3F5DC); display:flex; align-items:center; justify-content:center; font-size:46px;
  }
  html.dark .empty-illustration{ background:linear-gradient(160deg,#123420,#0d2818); }
  .empty-state h3{ font-size:15px; font-weight:800; }
  .empty-state p{ font-size:12.5px; color:var(--muted); max-width:220px; font-weight:500; }
  .empty-cta{ margin-top:6px; padding:12px 22px; border-radius:14px; background:var(--green); color:var(--green-dark); font-weight:800; font-size:13px; }

  .bottom-nav{
    position:sticky; bottom:0; z-index:50;
    display:flex; background:var(--surface); border-radius:26px 26px 0 0;
    box-shadow:0 -8px 24px -10px rgba(5,52,26,.18);
    padding:10px 8px calc(10px + var(--safe-bottom));
  }
  .nav-item{ flex:1; display:flex; flex-direction:column; align-items:center; gap:4px; padding:6px 0; border-radius:16px; transition:background .15s ease; }
  .nav-item svg{ width:22px; height:22px; stroke:var(--muted); fill:none; transition:stroke .15s ease, fill .15s ease; }
  .nav-item span{ font-size:10.5px; font-weight:700; color:var(--muted); }
  .nav-item.active{ background:#E8FBEC; }
  html.dark .nav-item.active{ background:#123420; }
  .nav-item.active svg{ stroke:var(--green-dark); }
  html.dark .nav-item.active svg{ stroke:var(--green); }
  .nav-item.active span{ color:var(--green-dark); }
  html.dark .nav-item.active span{ color:var(--green); }

  .profile-card{
    margin:18px 20px; padding:20px; border-radius:var(--radius-lg); background:linear-gradient(135deg,var(--green),var(--green-deep));
    display:flex; align-items:center; gap:14px; color:#04240F; box-shadow:var(--shadow-card);
  }
  .avatar{
    width:58px; height:58px; border-radius:18px; background:rgba(255,255,255,.35); display:flex; align-items:center; justify-content:center; font-size:26px; font-weight:800; flex-shrink:0;
  }
  .profile-info .pname{ font-size:16px; font-weight:800; }
  .profile-info .pphone{ font-size:12.5px; opacity:.85; font-weight:600; margin-top:2px; }
  .menu-list{ padding:6px 20px 20px; display:flex; flex-direction:column; gap:10px; }
  .menu-row{
    display:flex; align-items:center; gap:14px; background:var(--surface); padding:15px 16px; border-radius:16px; box-shadow:var(--shadow-card);
  }
  .menu-row .mi{ width:38px; height:38px; border-radius:12px; background:#E8FBEC; display:flex; align-items:center; justify-content:center; font-size:18px; flex-shrink:0; }
  html.dark .menu-row .mi{ background:#123420; }
  .menu-row span{ flex:1; font-size:13.5px; font-weight:700; }
  .menu-row .chev{ color:var(--muted); font-size:16px; }
  .toggle{ width:44px; height:26px; border-radius:13px; background:var(--border); position:relative; flex-shrink:0; transition:background .2s ease; }
  .toggle::after{ content:''; position:absolute; top:3px; left:3px; width:20px; height:20px; border-radius:50%; background:#fff; transition:transform .2s ease; box-shadow:0 2px 5px rgba(0,0,0,.2); }
  .toggle.on{ background:var(--green); }
  .toggle.on::after{ transform:translateX(18px); }

  .cart-item{ display:flex; gap:12px; background:var(--surface); border-radius:18px; padding:12px; margin:0 20px 12px; box-shadow:var(--shadow-card); align-items:center; }
  .cart-media{ width:58px; height:58px; border-radius:14px; display:flex; align-items:center; justify-content:center; font-size:28px; flex-shrink:0; }
  .cart-info{ flex:1; min-width:0; }
  .cart-info .cname{ font-size:13.5px; font-weight:700; }
  .cart-info .cprice{ font-size:12.5px; color:var(--accent); font-weight:800; margin-top:2px; }
  .qty-control{ display:flex; align-items:center; gap:8px; background:var(--bg); border-radius:11px; padding:4px; }
  .qty-control button{ width:26px; height:26px; border-radius:8px; background:var(--surface); font-weight:800; font-size:14px; box-shadow:var(--shadow-card); }
  .qty-control span{ font-size:13px; font-weight:800; min-width:16px; text-align:center; }

  .summary-card{ margin:6px 20px 16px; background:var(--surface); border-radius:20px; padding:18px; box-shadow:var(--shadow-card); }
  .summary-row{ display:flex; justify-content:space-between; font-size:13px; font-weight:600; color:var(--muted); padding:6px 0; }
  .summary-row.total{ color:var(--ink); font-weight:800; font-size:15.5px; border-top:1px dashed var(--border); margin-top:6px; padding-top:14px; }
  .summary-row.total .val{ color:var(--accent); }

  .checkout-block{ margin:0 20px 16px; background:var(--surface); border-radius:20px; padding:18px; box-shadow:var(--shadow-card); }
  .checkout-block h4{ font-size:13.5px; font-weight:800; margin-bottom:12px; display:flex; align-items:center; gap:8px; }
  .addr-text{ font-size:12.5px; color:var(--muted); font-weight:500; line-height:1.5; }
  .pay-option{ display:flex; align-items:center; gap:12px; padding:11px 0; border-bottom:1px solid var(--border); }
  .pay-option:last-child{ border-bottom:none; }
  .pay-option .po-icon{ width:34px; height:34px; border-radius:10px; background:var(--bg); display:flex; align-items:center; justify-content:center; font-size:15px; font-weight:800; flex-shrink:0; }
  .pay-option span{ flex:1; font-size:13px; font-weight:700; }
  .radio-dot{ width:19px; height:19px; border-radius:50%; border:2px solid var(--border); flex-shrink:0; position:relative; }
  .pay-option.sel .radio-dot{ border-color:var(--green); }
  .pay-option.sel .radio-dot::after{ content:''; position:absolute; inset:3px; border-radius:50%; background:var(--green); }

  .sticky-cta{ position:sticky; bottom:0; padding:14px 20px calc(14px + var(--safe-bottom)); background:linear-gradient(180deg, transparent, var(--bg) 30%); }
  .btn-primary{
    width:100%; padding:16px; border-radius:18px; background:var(--green); color:var(--green-dark); font-weight:800; font-size:14.5px;
    box-shadow:0 12px 24px -10px rgba(0,180,60,.55); display:flex; align-items:center; justify-content:center; gap:8px;
  }
  .btn-primary:active{ transform:scale(.98); }
  .btn-primary.small{ padding:11px; font-size:12.5px; border-radius:13px; box-shadow:none; }

  .track-card{ margin:16px 20px; background:var(--surface); border-radius:20px; padding:20px; box-shadow:var(--shadow-card); text-align:center; }
  .track-card .order-id{ font-size:12px; color:var(--muted); font-weight:700; }
  .track-card .order-title{ font-size:17px; font-weight:800; margin:4px 0 2px; }
  .timeline{ margin:20px; display:flex; flex-direction:column; }
  .tl-item{ display:flex; gap:14px; }
  .tl-marker{ display:flex; flex-direction:column; align-items:center; }
  .tl-dot{ width:26px; height:26px; border-radius:50%; background:var(--border); display:flex; align-items:center; justify-content:center; font-size:12px; color:var(--muted); flex-shrink:0; }
  .tl-dot.done{ background:var(--green); color:var(--green-dark); }
  .tl-dot.current{ background:var(--accent); color:#fff; box-shadow:0 0 0 6px rgba(255,122,61,.18); }
  .tl-line{ width:2px; flex:1; background:var(--border); min-height:32px; }
  .tl-line.done{ background:var(--green); }
  .tl-body{ padding-bottom:26px; padding-top:2px; }
  .tl-body .tt{ font-size:13.5px; font-weight:700; }
  .tl-body .ts{ font-size:11.5px; color:var(--muted); font-weight:500; margin-top:2px; }

  .overlay{
    position:absolute; inset:0; background:rgba(5,20,10,.5); z-index:100; opacity:0; pointer-events:none; transition:opacity .25s ease;
  }
  .overlay.show{ opacity:1; pointer-events:auto; }
  .sheet{
    position:absolute; left:0; right:0; bottom:0; background:var(--surface); border-radius:28px 28px 0 0;
    padding:10px 20px calc(20px + var(--safe-bottom)); transform:translateY(100%); transition:transform .32s cubic-bezier(.32,.72,0,1);
    max-height:88%; overflow-y:auto;
  }
  .overlay.show .sheet{ transform:translateY(0); }
  .sheet-handle{ width:38px; height:5px; border-radius:3px; background:var(--border); margin:6px auto 14px; }
  .sheet-close{ position:absolute; top:16px; right:20px; width:34px; height:34px; border-radius:11px; background:var(--bg); display:flex; align-items:center; justify-content:center; font-size:16px; font-weight:700; z-index:2; }
  .pd-media{ width:100%; aspect-ratio:1.3/1; border-radius:20px; display:flex; align-items:center; justify-content:center; font-size:80px; margin-bottom:16px; }
  .pd-name{ font-size:19px; font-weight:800; }
  .pd-desc{ font-size:13px; color:var(--muted); font-weight:500; margin:8px 0 14px; line-height:1.6; }
  .pd-row{ display:flex; align-items:center; justify-content:space-between; margin-bottom:16px; }
  .pd-price{ font-size:20px; font-weight:800; color:var(--accent); }
  .pd-price small{ display:block; font-size:11px; color:var(--muted); font-weight:600; }
  .pd-stock{ font-size:12px; font-weight:700; color:var(--green-deep); background:#E8FBEC; padding:6px 12px; border-radius:10px; }
  html.dark .pd-stock{ background:#123420; }

  .promo-overlay{ position:absolute; inset:0; background:rgba(5,20,10,.6); z-index:110; display:flex; align-items:center; justify-content:center; opacity:0; pointer-events:none; transition:opacity .25s ease; padding:30px; }
  .promo-overlay.show{ opacity:1; pointer-events:auto; }
  .promo-box{ width:100%; background:var(--surface); border-radius:26px; padding:26px 22px; text-align:center; position:relative; transform:scale(.85); transition:transform .3s cubic-bezier(.32,.72,0,1); }
  .promo-overlay.show .promo-box{ transform:scale(1); }
  .promo-box .pb-icon{ font-size:52px; margin-bottom:10px; }
  .promo-box h3{ font-size:18px; font-weight:800; margin-bottom:6px; }
  .promo-box p{ font-size:13px; color:var(--muted); font-weight:500; margin-bottom:18px; line-height:1.5; }
  .promo-close{ position:absolute; top:14px; right:14px; width:30px; height:30px; border-radius:10px; background:var(--bg); font-weight:700; }

  #toast-wrap{ position:absolute; top:14px; left:0; right:0; z-index:200; display:flex; flex-direction:column; align-items:center; gap:8px; pointer-events:none; }
  .toast{
    background:var(--green-dark); color:#fff; font-size:12.5px; font-weight:700; padding:12px 18px; border-radius:14px; box-shadow:0 10px 24px rgba(0,0,0,.25);
    display:flex; align-items:center; gap:8px; opacity:0; transform:translateY(-14px); transition:all .3s cubic-bezier(.32,.72,0,1);
  }
  .toast.show{ opacity:1; transform:translateY(0); }

  ::-webkit-scrollbar{ width:0; height:0; }
</style>
</head>
<body>
<div id="app-shell">

  <div id="toast-wrap"></div>

  <div class="app-header" id="app-header"></div>

  <div id="pull-indicator"><div class="spinner"></div><span>Menyegarkan...</span></div>

  <div id="view-container">

    <!-- HOME -->
    <section class="view" data-view="home">
      <div class="banner-wrap">
        <div class="banner-track">
          <div class="banner-slides" id="banner-slides"></div>
          <div class="banner-dots" id="banner-dots"></div>
        </div>
      </div>
      <div class="section">
        <div class="section-head"><h2>Kategori</h2></div>
      </div>
      <div class="cat-row" id="home-cats"></div>
      <div class="section" style="margin-top:6px;">
        <div class="section-head">
          <h2>Produk Populer</h2>
          <a class="link" data-goto="produk">Lihat Semua</a>
        </div>
      </div>
      <div class="product-grid" id="home-products"></div>
    </section>

    <!-- PRODUK -->
    <section class="view" data-view="produk">
      <div class="filter-bar" id="produk-filters"></div>
      <select class="sort-select" id="sort-select">
        <option value="default">Urutkan: Rekomendasi</option>
        <option value="price-asc">Harga Terendah</option>
        <option value="price-desc">Harga Tertinggi</option>
        <option value="name-asc">Nama A-Z</option>
      </select>
      <div class="product-grid" id="produk-grid"></div>
    </section>

    <!-- FAVORITE -->
    <section class="view" data-view="favorite">
      <div class="section" style="padding-top:20px;"><div class="section-head"><h2>Produk Favorit</h2></div></div>
      <div class="product-grid" id="favorite-grid"></div>
    </section>

    <!-- AKUN -->
    <section class="view" data-view="akun">
      <div class="profile-card">
        <div class="avatar">R</div>
        <div class="profile-info">
          <div class="pname">Rudy Hartono</div>
          <div class="pphone">+62 812-3456-7890</div>
        </div>
      </div>
      <div class="menu-list">
        <div class="menu-row" data-action="toast" data-msg="Riwayat pesanan dibuka"><div class="mi">📦</div><span>Riwayat Pesanan</span><div class="chev">›</div></div>
        <div class="menu-row" data-action="toast" data-msg="Alamat pengiriman dibuka"><div class="mi">📍</div><span>Alamat Pengiriman</span><div class="chev">›</div></div>
        <div class="menu-row" data-goto="favorite"><div class="mi">❤️</div><span>Produk Favorit</span><div class="chev">›</div></div>
        <div class="menu-row" data-action="toast" data-msg="Belum ada voucher tersedia"><div class="mi">🎁</div><span>Voucher Saya</span><div class="chev">›</div></div>
        <div class="menu-row" data-action="toast" data-msg="Terima kasih atas penilaiannya!"><div class="mi">⭐</div><span>Beri Penilaian</span><div class="chev">›</div></div>
        <div class="menu-row" id="darkmode-row"><div class="mi">🌙</div><span>Mode Gelap</span><div class="toggle" id="dark-toggle"></div></div>
        <div class="menu-row" data-action="toast" data-msg="Sampai jumpa lagi, Rudy!"><div class="mi">🚪</div><span>Logout</span><div class="chev">›</div></div>
      </div>
    </section>

    <!-- CART -->
    <section class="view" data-view="cart">
      <div class="section" style="padding-top:20px;"><div class="section-head"><h2>Keranjang Saya</h2></div></div>
      <div id="cart-items"></div>
      <div class="summary-card" id="cart-summary" style="display:none;">
        <div class="summary-row"><span>Subtotal</span><span id="cart-subtotal">Rp0</span></div>
        <div class="summary-row"><span>Ongkos Kirim</span><span id="cart-ongkir">Rp5.000</span></div>
        <div class="summary-row total"><span>Total</span><span class="val" id="cart-total">Rp0</span></div>
      </div>
      <div class="sticky-cta" id="cart-cta" style="display:none;">
        <button class="btn-primary" data-goto="checkout">Lanjut Checkout</button>
      </div>
    </section>

    <!-- CHECKOUT -->
    <section class="view" data-view="checkout">
      <div class="section" style="padding-top:20px;"><div class="section-head"><h2>Checkout</h2></div></div>
      <div class="checkout-block">
        <h4>📍 Alamat Pengiriman</h4>
        <p class="addr-text">Rudy Hartono — Jl. Kenanga No. 12, RT 04/RW 07, Depok, Jawa Barat 16424. <b>+62 812-3456-7890</b></p>
      </div>
      <div class="checkout-block">
        <h4>💳 Metode Pembayaran</h4>
        <div id="pay-options"></div>
      </div>
      <div class="summary-card">
        <div class="summary-row"><span>Subtotal</span><span id="co-subtotal">Rp0</span></div>
        <div class="summary-row"><span>Ongkos Kirim</span><span id="co-ongkir">Rp5.000</span></div>
        <div class="summary-row"><span>Diskon</span><span id="co-diskon">-Rp2.000</span></div>
        <div class="summary-row total"><span>Total</span><span class="val" id="co-total">Rp0</span></div>
      </div>
      <div class="sticky-cta">
        <button class="btn-primary" id="btn-buat-pesanan">Buat Pesanan</button>
      </div>
    </section>

    <!-- TRACKING -->
    <section class="view" data-view="tracking">
      <div class="track-card">
        <div class="order-id">📦 Pesanan #SYR-0001</div>
        <div class="order-title">Sedang Diproses</div>
      </div>
      <div class="timeline" id="timeline"></div>
      <div class="sticky-cta">
        <button class="btn-primary" data-goto="home">Kembali ke Beranda</button>
      </div>
    </section>

  </div>

  <nav class="bottom-nav" id="bottom-nav"></nav>

  <div class="overlay" id="pd-overlay">
    <div class="sheet" id="pd-sheet">
      <div class="sheet-handle"></div>
      <button class="sheet-close" id="pd-close">✕</button>
      <div id="pd-content"></div>
    </div>
  </div>

  <div class="promo-overlay" id="promo-overlay">
    <div class="promo-box">
      <button class="promo-close" id="promo-close">✕</button>
      <div class="pb-icon">🎉</div>
      <h3>Gratis Ongkir Hari Ini!</h3>
      <p>Belanja sayur segar minimal Rp30.000 dan nikmati gratis biaya antar ke rumahmu. Berlaku hari ini saja.</p>
      <button class="btn-primary small" id="promo-cta">Belanja Sekarang</button>
    </div>
  </div>

</div>

<script>
(function(){
  "use strict";

  const CATEGORIES = [
    { id:'sayuran', label:'Sayuran', icon:'🥬' },
    { id:'umbi', label:'Umbi-Umbian', icon:'🥕' },
    { id:'buah', label:'Buah', icon:'🍅' },
    { id:'bumbu', label:'Bumbu', icon:'🌶' },
    { id:'telur', label:'Telur', icon:'🥚' },
  ];

  const PRODUCTS = [
    { id:'bayam', name:'Bayam', cat:'sayuran', price:5000, unit:'ikat', desc:'Bayam hijau segar, dipetik pagi hari, kaya zat besi.', stock:32, icon:'🥬', tint:'#DFF7E4' },
    { id:'kangkung', name:'Kangkung', cat:'sayuran', price:4000, unit:'ikat', desc:'Kangkung renyah cocok untuk tumis maupun lalapan.', stock:28, icon:'🌿', tint:'#E1F8E6' },
    { id:'sawi', name:'Sawi Hijau', cat:'sayuran', price:4500, unit:'ikat', desc:'Sawi hijau segar dengan batang renyah dan manis.', stock:21, icon:'🥬', tint:'#DCF6E2' },
    { id:'selada', name:'Selada', cat:'sayuran', price:6000, unit:'ikat', desc:'Selada segar, daun lebar, pas untuk salad dan burger.', stock:18, icon:'🥗', tint:'#E4F8E9' },
    { id:'wortel', name:'Wortel', cat:'umbi', price:8000, unit:'kg', desc:'Wortel manis warna oranye cerah, kaya vitamin A.', stock:40, icon:'🥕', tint:'#FFE9D6' },
    { id:'kentang', name:'Kentang', cat:'umbi', price:10000, unit:'kg', desc:'Kentang lokal, tekstur pulen, cocok segala olahan.', stock:35, icon:'🥔', tint:'#F3E9D8' },
    { id:'lobak', name:'Lobak', cat:'umbi', price:7000, unit:'kg', desc:'Lobak putih segar, renyah dan sedikit manis.', stock:22, icon:'🫚', tint:'#F1F3E6' },
    { id:'brokoli', name:'Brokoli', cat:'sayuran', price:12000, unit:'pcs', desc:'Brokoli hijau padat, kaya serat dan vitamin C.', stock:15, icon:'🥦', tint:'#DDF5E1' },
    { id:'kembangkol', name:'Kembang Kol', cat:'sayuran', price:11000, unit:'pcs', desc:'Kembang kol putih bersih, tekstur lembut saat dimasak.', stock:14, icon:'🥦', tint:'#F2F6E2' },
    { id:'tomat', name:'Tomat', cat:'buah', price:9000, unit:'kg', desc:'Tomat merah segar, asam manis seimbang.', stock:38, icon:'🍅', tint:'#FDE3E0' },
    { id:'cabai', name:'Cabai Merah', cat:'bumbu', price:15000, unit:'ons', desc:'Cabai merah segar pedas, wajib ada di dapur.', stock:26, icon:'🌶', tint:'#FCE0DD' },
    { id:'bawang', name:'Bawang Merah', cat:'bumbu', price:18000, unit:'ons', desc:'Bawang merah lokal, aroma tajam dan segar.', stock:30, icon:'🧅', tint:'#FBE7EE' },
  ];

  const BANNERS = [
    { tag:'GRATIS ANTAR', title:'Belanja Sayur, Diantar Sampai Depan Rumah', sub:'Min. belanja Rp30.000', bg:'linear-gradient(135deg,#00C853,#009e40)' },
  ];

  const state = {
    view:'home',
    cart:JSON.parse(localStorage.getItem('sk_cart')||'{}'),
    fav:JSON.parse(localStorage.getItem('sk_fav')||'[]'),
    dark:localStorage.getItem('sk_dark')==='1',
    produkCat:'all',
    produkSearch:'',
    produkSort:'default',
    bannerIdx:0,
  };

  function saveCart(){ localStorage.setItem('sk_cart', JSON.stringify(state.cart)); }
  function saveFav(){ localStorage.setItem('sk_fav', JSON.stringify(state.fav)); }
  function cartCount(){ return Object.values(state.cart).reduce((a,b)=>a+b,0); }
  function fmt(n){ return 'Rp'+n.toLocaleString('id-ID'); }
  function findProduct(id){ return PRODUCTS.find(p=>p.id===id); }

  function toast(msg, icon){
    const wrap = document.getElementById('toast-wrap');
    const el = document.createElement('div');
    el.className='toast';
    el.innerHTML = `<span>${icon||'✅'}</span><span>${msg}</span>`;
    wrap.appendChild(el);
    requestAnimationFrame(()=> el.classList.add('show'));
    setTimeout(()=>{ el.classList.remove('show'); setTimeout(()=>el.remove(),300); }, 2200);
  }
  function renderHeader(){
    const header = document.getElementById('app-header');
    if(state.view === 'home'){
      header.innerHTML = `
        <div class="header-top">
          <div class="greeting"><span class="hi">Selamat Datang,</span><span class="name">Rudy! 👋</span></div>
          <div class="header-icons">
            <button class="icon-btn" data-action="notif" aria-label="Notifikasi">
              <svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round"><path d="M18 8a6 6 0 10-12 0c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 01-3.46 0"/></svg>
              <span class="badge" id="notif-badge">2</span>
            </button>
            <button class="icon-btn" data-goto="cart" aria-label="Keranjang">
              <svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 002 1.61h9.72a2 2 0 002-1.61L23 6H6"/></svg>
              <span class="badge" id="cart-badge" style="display:none;">0</span>
            </button>
          </div>
        </div>
        <div class="header-search">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/></svg>
          <input placeholder="Cari sayuran segar..." id="home-search-input" />
        </div>`;
    } else if(state.view === 'produk'){
      header.innerHTML = `
        <div class="header-top">
          <div class="greeting"><span class="hi">Katalog</span><span class="name">Semua Produk</span></div>
          <div class="header-icons">
            <button class="icon-btn" data-goto="cart" aria-label="Keranjang">
              <svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 002 1.61h9.72a2 2 0 002-1.61L23 6H6"/></svg>
              <span class="badge" id="cart-badge2" style="display:none;">0</span>
            </button>
          </div>
        </div>
        <div class="header-search">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/></svg>
          <input placeholder="Cari produk..." id="produk-search-input" value="${state.produkSearch}"/>
        </div>`;
    } else if(state.view === 'favorite'){
      header.innerHTML = `<div class="header-top"><div class="greeting"><span class="hi">Koleksi</span><span class="name">Favorit Saya</span></div><div class="header-icons"><button class="icon-btn" data-goto="home" aria-label="Beranda"><svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12l9-9 9 9"/><path d="M5 10v10h14V10"/></svg></button></div></div>`;
    } else if(state.view === 'akun'){
      header.innerHTML = `<div class="header-top"><div class="greeting"><span class="hi">Halo,</span><span class="name">Akun Saya</span></div><div class="header-icons"><button class="icon-btn" data-goto="home" aria-label="Beranda"><svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12l9-9 9 9"/><path d="M5 10v10h14V10"/></svg></button></div></div>`;
    } else if(state.view === 'cart'){
      header.innerHTML = `<div class="header-top"><div class="greeting"><span class="hi">Belanjaan</span><span class="name">Keranjang Saya</span></div><div class="header-icons"><button class="icon-btn" data-goto="home" aria-label="Kembali"><svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 18l-6-6 6-6"/></svg></button></div></div>`;
    } else if(state.view === 'checkout'){
      header.innerHTML = `<div class="header-top"><div class="greeting"><span class="hi">Selangkah lagi</span><span class="name">Checkout</span></div><div class="header-icons"><button class="icon-btn" data-goto="cart" aria-label="Kembali"><svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 18l-6-6 6-6"/></svg></button></div></div>`;
    } else if(state.view === 'tracking'){
      header.innerHTML = `<div class="header-top"><div class="greeting"><span class="hi">Terima kasih!</span><span class="name">Lacak Pesanan</span></div><div class="header-icons"><button class="icon-btn" data-goto="home" aria-label="Beranda"><svg viewBox="0 0 24 24" fill="none" stroke="#04240F" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12l9-9 9 9"/><path d="M5 10v10h14V10"/></svg></button></div></div>`;
    }
    updateCartBadges();
    if(state.view==='home'){
      const inp = document.getElementById('home-search-input');
      inp.addEventListener('input', e=>{ state.produkSearch = e.target.value; if(e.target.value.trim()){ goto('produk'); } });
    }
    if(state.view==='produk'){
      const inp = document.getElementById('produk-search-input');
      inp.addEventListener('input', e=>{ state.produkSearch = e.target.value; renderProduk(); });
      inp.focus();
    }
  }

  function updateCartBadges(){
    const c = cartCount();
    ['cart-badge','cart-badge2'].forEach(id=>{
      const b = document.getElementById(id);
      if(!b) return;
      if(c>0){ b.style.display='flex'; b.textContent = c>99?'99+':c; } else { b.style.display='none'; }
    });
  }

  function productCard(p){
    const isFav = state.fav.includes(p.id);
    return `
    <div class="product-card" data-open-product="${p.id}">
      <div class="product-media" style="background:${p.tint};">
        <span class="stock-tag">Stok ${p.stock}</span>
        <button class="fav-btn ${isFav?'active':''}" data-fav="${p.id}" aria-label="Favorit">
          <svg viewBox="0 0 24 24" stroke-width="2"><path d="M12 21s-7.5-4.6-10-9.3C.5 8 2 4 6 4c2.2 0 3.7 1.2 6 3.6C14.3 5.2 15.8 4 18 4c4 0 5.5 4 4 7.7C19.5 16.4 12 21 12 21z"/></svg>
        </button>
        <span>${p.icon}</span>
      </div>
      <div class="product-name">${p.name}</div>
      <div class="product-desc">${p.desc.slice(0,34)}${p.desc.length>34?'…':''}</div>
      <div class="product-bottom">
        <div class="product-price">${fmt(p.price)}<small>/ ${p.unit}</small></div>
        <button class="add-btn" data-add="${p.id}" aria-label="Tambah ke keranjang">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg>
        </button>
      </div>
    </div>`;
  }

  function skeletonCard(){
    return `<div class="sk-card"><div class="skeleton sk-media"></div><div class="skeleton sk-line" style="width:70%;"></div><div class="skeleton sk-line" style="width:45%;"></div></div>`;
  }

  function renderBanner(){
    const track = document.getElementById('banner-slides');
    const dots = document.getElementById('banner-dots');
    track.innerHTML = BANNERS.map(b=>`
      <div class="banner-slide" style="background:${b.bg};">
        <span class="tag">${b.tag}</span>
        <h3>${b.title}</h3>
        <p>${b.sub}</p>
      </div>`).join('');
    dots.innerHTML = BANNERS.length>1 ? BANNERS.map((_,i)=>`<span class="${i===state.bannerIdx?'on':''}"></span>`).join('') : '';
    track.style.transform = `translateX(-${state.bannerIdx*100}%)`;
  }
  function nextBanner(){
    if(BANNERS.length<=1) return;
    state.bannerIdx = (state.bannerIdx+1) % BANNERS.length;
    renderBanner();
  }

  function renderHomeCats(){
    const wrap = document.getElementById('home-cats');
    wrap.innerHTML = CATEGORIES.map(c=>`
      <div class="cat-item" data-cat-goto="${c.id}">
        <div class="cat-circle">${c.icon}</div>
        <span>${c.label}</span>
      </div>`).join('');
  }

  function renderHomeProducts(loading){
    const grid = document.getElementById('home-products');
    if(loading){ grid.innerHTML = Array(4).fill(skeletonCard()).join(''); return; }
    const popular = PRODUCTS.slice(0,4);
    grid.innerHTML = popular.map(productCard).join('');
  }

  function renderProdukFilters(){
    const wrap = document.getElementById('produk-filters');
    const all = [{id:'all', label:'Semua', icon:'🛒'}, ...CATEGORIES];
    wrap.innerHTML = all.map(c=>`<div class="chip ${state.produkCat===c.id?'active':''}" data-cat-filter="${c.id}">${c.icon} ${c.label}</div>`).join('');
    document.getElementById('sort-select').value = state.produkSort;
  }

  function renderProduk(loading){
    const grid = document.getElementById('produk-grid');
    if(loading){ grid.innerHTML = Array(6).fill(skeletonCard()).join(''); return; }
    let list = PRODUCTS.filter(p=> state.produkCat==='all' || p.cat===state.produkCat);
    if(state.produkSearch.trim()){
      const q = state.produkSearch.trim().toLowerCase();
      list = list.filter(p=> p.name.toLowerCase().includes(q));
    }
    if(state.produkSort==='price-asc') list = [...list].sort((a,b)=>a.price-b.price);
    if(state.produkSort==='price-desc') list = [...list].sort((a,b)=>b.price-a.price);
    if(state.produkSort==='name-asc') list = [...list].sort((a,b)=>a.name.localeCompare(b.name));

    if(list.length===0){
      grid.innerHTML = '';
      grid.parentElement.insertAdjacentHTML('beforeend','');
      document.getElementById('produk-empty')?.remove();
      const empty = document.createElement('div');
      empty.id='produk-empty';
      empty.className='empty-state';
      empty.innerHTML = `<div class="empty-illustration">🔍</div><h3>Produk tidak ditemukan</h3><p>Coba ubah kata kunci atau pilih kategori lain.</p>`;
      grid.after(empty);
      return;
    } else {
      document.getElementById('produk-empty')?.remove();
    }
    grid.innerHTML = list.map(productCard).join('');
  }

  function renderFavorite(){
    const grid = document.getElementById('favorite-grid');
    const list = PRODUCTS.filter(p=>state.fav.includes(p.id));
    if(list.length===0){
      grid.innerHTML='';
      document.getElementById('fav-empty')?.remove();
      const empty=document.createElement('div');
      empty.id='fav-empty'; empty.className='empty-state';
      empty.innerHTML = `<div class="empty-illustration">❤️</div><h3>Belum ada produk favorit</h3><p>Ketuk ikon hati pada produk untuk menyimpannya di sini.</p><button class="empty-cta" data-goto="produk">Jelajahi Produk</button>`;
      grid.after(empty);
      return;
    } else {
      document.getElementById('fav-empty')?.remove();
    }
    grid.innerHTML = list.map(productCard).join('');
  }

  function renderCart(){
    const wrap = document.getElementById('cart-items');
    const ids = Object.keys(state.cart).filter(id=>state.cart[id]>0);
    if(ids.length===0){
      wrap.innerHTML = `<div class="empty-state"><div class="empty-illustration">🛒</div><h3>Keranjang masih kosong</h3><p>Yuk mulai belanja sayur segar untuk hari ini.</p><button class="empty-cta" data-goto="produk">Mulai Belanja</button></div>`;
      document.getElementById('cart-summary').style.display='none';
      document.getElementById('cart-cta').style.display='none';
      return;
    }
    wrap.innerHTML = ids.map(id=>{
      const p = findProduct(id); const qty = state.cart[id];
      return `<div class="cart-item">
        <div class="cart-media" style="background:${p.tint};">${p.icon}</div>
        <div class="cart-info">
          <div class="cname">${p.name}</div>
          <div class="cprice">${fmt(p.price*qty)} <span style="color:var(--muted);font-weight:600;">(${fmt(p.price)}/${p.unit})</span></div>
        </div>
        <div class="qty-control">
          <button data-qty="${id}" data-delta="-1">−</button>
          <span>${qty}</span>
          <button data-qty="${id}" data-delta="1">+</button>
        </div>
      </div>`;
    }).join('');
    const subtotal = ids.reduce((s,id)=> s + findProduct(id).price*state.cart[id], 0);
    const ongkir = subtotal>0 ? 5000 : 0;
    document.getElementById('cart-subtotal').textContent = fmt(subtotal);
    document.getElementById('cart-ongkir').textContent = fmt(ongkir);
    document.getElementById('cart-total').textContent = fmt(subtotal+ongkir);
    document.getElementById('cart-summary').style.display='block';
    document.getElementById('cart-cta').style.display='block';
  }

  const PAY_METHODS = [
    {id:'qris', label:'QRIS', icon:'QR'},
    {id:'dana', label:'DANA', icon:'D'},
    {id:'ovo', label:'OVO', icon:'O'},
    {id:'gopay', label:'GoPay', icon:'G'},
    {id:'transfer', label:'Transfer Bank', icon:'🏦'},
    {id:'cod', label:'Bayar di Tempat (COD)', icon:'💵'},
  ];
  let selectedPay = 'qris';

  function renderCheckout(){
    const wrap = document.getElementById('pay-options');
    wrap.innerHTML = PAY_METHODS.map(m=>`
      <div class="pay-option ${selectedPay===m.id?'sel':''}" data-pay="${m.id}">
        <div class="po-icon">${m.icon}</div>
        <span>${m.label}</span>
        <div class="radio-dot"></div>
      </div>`).join('');
    const ids = Object.keys(state.cart).filter(id=>state.cart[id]>0);
    const subtotal = ids.reduce((s,id)=> s + findProduct(id).price*state.cart[id], 0);
    const ongkir = subtotal>0?5000:0;
    const diskon = subtotal>=30000 ? ongkir : 2000;
    const total = Math.max(subtotal+ongkir-diskon,0);
    document.getElementById('co-subtotal').textContent = fmt(subtotal);
    document.getElementById('co-ongkir').textContent = fmt(ongkir);
    document.getElementById('co-diskon').textContent = '-'+fmt(diskon);
    document.getElementById('co-total').textContent = fmt(total);
  }

  const TL_STEPS = [
    { t:'Pesanan Dibuat', s:'Pesanan kamu telah diterima', icon:'✓' },
    { t:'Pembayaran Dikonfirmasi', s:'Pembayaran berhasil diverifikasi', icon:'✓' },
    { t:'Sedang Diproses', s:'Sayur sedang disiapkan oleh mitra kami', icon:'●' },
    { t:'Sedang Diantar', s:'Kurir sedang menuju lokasimu', icon:'○' },
    { t:'Selesai', s:'Pesanan telah sampai, selamat menikmati!', icon:'○' },
  ];
  function renderTracking(activeStep){
    const wrap = document.getElementById('timeline');
    wrap.innerHTML = TL_STEPS.map((step,i)=>{
      const done = i < activeStep;
      const current = i === activeStep;
      return `<div class="tl-item">
        <div class="tl-marker">
          <div class="tl-dot ${done?'done':''} ${current?'current':''}">${done?'✓':(current?'●':'')}</div>
          ${i<TL_STEPS.length-1?`<div class="tl-line ${done?'done':''}"></div>`:''}
        </div>
        <div class="tl-body"><div class="tt">${step.t}</div><div class="ts">${step.s}</div></div>
      </div>`;
    }).join('');
  }

  const NAV_ITEMS = [
    { id:'home', label:'Home', icon:'<path d="M3 12l9-9 9 9"/><path d="M5 10v10h14V10"/>' },
    { id:'produk', label:'Product', icon:'<rect x="3" y="7" width="18" height="14" rx="2"/><path d="M8 7V5a4 4 0 018 0v2"/>' },
    { id:'favorite', label:'Favorite', icon:'<path d="M12 21s-7.5-4.6-10-9.3C.5 8 2 4 6 4c2.2 0 3.7 1.2 6 3.6C14.3 5.2 15.8 4 18 4c4 0 5.5 4 4 7.7C19.5 16.4 12 21 12 21z"/>' },
    { id:'akun', label:'Akun', icon:'<circle cx="12" cy="8" r="4"/><path d="M4 21c0-4 4-6 8-6s8 2 8 6"/>' },
  ];
  function renderBottomNav(){
    const nav = document.getElementById('bottom-nav');
    const mainViews = ['home','produk','favorite','akun'];
    nav.innerHTML = NAV_ITEMS.map(n=>`
      <button class="nav-item ${state.view===n.id?'active':''}" data-goto="${n.id}">
        <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">${n.icon}</svg>
        <span>${n.label}</span>
      </button>`).join('');
    nav.style.display = mainViews.includes(state.view) ? 'flex' : 'none';
  }

  function openProductModal(id){
    const p = findProduct(id);
    const isFav = state.fav.includes(p.id);
    document.getElementById('pd-content').innerHTML = `
      <div class="pd-media" style="background:${p.tint};">${p.icon}</div>
      <div class="pd-name">${p.name}</div>
      <div class="pd-desc">${p.desc}</div>
      <div class="pd-row">
        <div class="pd-price">${fmt(p.price)}<small>per ${p.unit}</small></div>
        <div class="pd-stock">Stok: ${p.stock}</div>
      </div>
      <div style="display:flex; gap:10px;">
        <button class="btn-primary" style="background:var(--surface); box-shadow:var(--shadow-card); color:${isFav?'#FF4D6D':'var(--ink)'}; flex:0 0 56px;" id="pd-fav-btn" data-fav="${p.id}">${isFav?'♥':'♡'}</button>
        <button class="btn-primary" id="pd-add-btn" data-add="${p.id}" style="flex:1;">Tambah ke Keranjang</button>
      </div>`;
    document.getElementById('pd-overlay').classList.add('show');
  }
  function closeProductModal(){ document.getElementById('pd-overlay').classList.remove('show'); }


  function showPromo(){ document.getElementById('promo-overlay').classList.add('show'); }
  function hidePromo(){ document.getElementById('promo-overlay').classList.remove('show'); }


  function goto(view){
    state.view = view;
    document.querySelectorAll('.view').forEach(v=> v.classList.toggle('active', v.dataset.view===view));
    document.getElementById('view-container').scrollTop = 0;
    renderHeader();
    renderBottomNav();
    if(view==='home'){ renderHomeProducts(true); setTimeout(()=>renderHomeProducts(false), 500); }
    if(view==='produk'){ renderProdukFilters(); renderProduk(true); setTimeout(()=>renderProduk(false), 500); }
    if(view==='favorite') renderFavorite();
    if(view==='cart') renderCart();
    if(view==='checkout') renderCheckout();
    if(view==='tracking'){ startTrackingAnimation(); }
    closeProductModal();
  }

  function startTrackingAnimation(){
    let step = 2;
    renderTracking(step);
    clearInterval(window._trackTimer);
    window._trackTimer = setInterval(()=>{
      if(step >= TL_STEPS.length-1){ clearInterval(window._trackTimer); return; }
      step++;
      renderTracking(step);
    }, 3500);
  }

  function applyDark(){
    document.documentElement.classList.toggle('dark', state.dark);
    const toggle = document.getElementById('dark-toggle');
    if(toggle) toggle.classList.toggle('on', state.dark);
  }

  function addToCart(id, btnEl){
    state.cart[id] = (state.cart[id]||0)+1;
    saveCart();
    updateCartBadges();
    if(state.view==='cart') renderCart();
    const p = findProduct(id);
    toast(`${p.name} ditambahkan ke keranjang`, '🛒');
    if(btnEl){ btnEl.classList.remove('bounce'); void btnEl.offsetWidth; btnEl.classList.add('bounce'); }
  }
  function toggleFav(id){
    const idx = state.fav.indexOf(id);
    if(idx>-1){ state.fav.splice(idx,1); toast('Dihapus dari favorit','💔'); }
    else { state.fav.push(id); toast('Ditambahkan ke favorit','❤️'); }
    saveFav();
    document.querySelectorAll(`[data-fav="${id}"]`).forEach(b=> b.classList.toggle('active', state.fav.includes(id)));
    if(state.view==='favorite') renderFavorite();
    if(document.getElementById('pd-overlay').classList.contains('show')){
      const favBtn = document.getElementById('pd-fav-btn');
      if(favBtn){ const isFav = state.fav.includes(id); favBtn.textContent = isFav?'♥':'♡'; favBtn.style.color = isFav?'#FF4D6D':'var(--ink)'; }
    }
  }

  document.addEventListener('click', function(e){
    const gotoEl = e.target.closest('[data-goto]');
    if(gotoEl){ goto(gotoEl.dataset.goto); return; }

    const catGoto = e.target.closest('[data-cat-goto]');
    if(catGoto){ state.produkCat = catGoto.dataset.catGoto; goto('produk'); return; }

    const catFilter = e.target.closest('[data-cat-filter]');
    if(catFilter){ state.produkCat = catFilter.dataset.catFilter; renderProdukFilters(); renderProduk(); return; }

    const addBtn = e.target.closest('[data-add]');
    if(addBtn){ e.stopPropagation(); addToCart(addBtn.dataset.add, addBtn); return; }

    const favBtn = e.target.closest('[data-fav]');
    if(favBtn){ e.stopPropagation(); toggleFav(favBtn.dataset.fav); return; }

    const openProd = e.target.closest('[data-open-product]');
    if(openProd){ openProductModal(openProd.dataset.openProduct); return; }

    const payOpt = e.target.closest('[data-pay]');
    if(payOpt){ selectedPay = payOpt.dataset.pay; renderCheckout(); return; }

    const qtyBtn = e.target.closest('[data-qty]');
    if(qtyBtn){
      const id = qtyBtn.dataset.qty, delta = parseInt(qtyBtn.dataset.delta,10);
      state.cart[id] = Math.max((state.cart[id]||0)+delta, 0);
      if(state.cart[id]===0) delete state.cart[id];
      saveCart(); updateCartBadges(); renderCart();
      return;
    }

    const actionEl = e.target.closest('[data-action]');
    if(actionEl){
      const act = actionEl.dataset.action;
      if(act==='notif') toast('Tidak ada notifikasi baru','🔔');
      if(act==='toast') toast(actionEl.dataset.msg || 'Oke','✅');
      return;
    }

    if(e.target.id==='pd-close' || e.target.id==='pd-overlay'){ closeProductModal(); return; }
    if(e.target.id==='promo-close' || e.target.id==='promo-overlay'){ hidePromo(); return; }
    if(e.target.id==='promo-cta'){ hidePromo(); goto('produk'); return; }

    if(e.target.id==='dark-toggle'){
      state.dark = !state.dark;
      localStorage.setItem('sk_dark', state.dark?'1':'0');
      applyDark();
      return;
    }

    if(e.target.id==='btn-buat-pesanan'){
      const ids = Object.keys(state.cart).filter(id=>state.cart[id]>0);
      if(ids.length===0){ toast('Keranjang masih kosong','⚠️'); return; }
      toast('Pesanan berhasil dibuat!','🎉');
      state.cart = {}; saveCart(); updateCartBadges();
      goto('tracking');
      return;
    }
  });
                                                                  
  document.getElementById('sort-select').addEventListener('change', function(e){
    state.produkSort = e.target.value;
    renderProduk();
  });

  (function(){
    const container = document.getElementById('view-container');
    const indicator = document.getElementById('pull-indicator');
    let startY = 0, pulling = false;
    container.addEventListener('touchstart', e=>{
      if(container.scrollTop<=0 && state.view==='home'){ startY = e.touches[0].clientY; pulling = true; }
    }, {passive:true});
    container.addEventListener('touchmove', e=>{
      if(!pulling) return;                
      const diff = e.touches[0].clientY - startY;
      if(diff>10 && diff<120){ indicator.style.height = Math.min(diff,50)+'px'; }
    }, {passive:true});                          
    container.addEventListener('touchend', e=>{
      if(!pulling) return;                             
      pulling = false;
      if(parseInt(indicator.style.height||'0',10) > 35){
        indicator.style.height='44px';
        renderHomeProducts(true);
        setTimeout(()=>{ renderHomeProducts(false); indicator.style.height='0'; toast('Beranda diperbarui','🔄'); }, 700);
      } else {
        indicator.style.height='0';
      }
    });
  })();
 
  function init(){
    applyDark();
    renderBanner();
    renderHomeCats();
    renderHeader();
    renderBottomNav();
    renderHomeProducts(true);
    setTimeout(()=>renderHomeProducts(false), 600);
    document.querySelectorAll('.view').forEach(v=> v.classList.toggle('active', v.dataset.view==='home'));
    setInterval(nextBanner, 3000);
    document.getElementById('pd-close').addEventListener('click', closeProductModal);
    document.getElementById('promo-close').addEventListener('click', hidePromo);
    setTimeout(showPromo, 1800);
  }
  init();
})();
</script>
</body>
</html>
