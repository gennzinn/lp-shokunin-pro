---
updated: 2026-07-08
aliases: [HTMLテンプレート]
---

# 完成形HTMLテンプレート

これは実案件で検証済みの土台である。**この構造・クラス名を維持したまま**、
【 】を案件の内容に、`:root`の色をテーマ(03)の色に置き換えて使う。
セクションの増減は自由だが、02_tech_spec.md の絶対条件を壊さないこと。

```html
<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<!-- 計測タグ:ユーザー指定がある場合のみここに入れる -->
<meta name="description" content="【地域名+サービス+ベネフィット。80〜120字】">
<meta name="format-detection" content="telephone=no">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' rx='22' fill='%23【メイン色hex(#抜き)】'/%3E%3Ctext x='50' y='68' font-size='48' font-family='sans-serif' font-weight='bold' fill='%23fff' text-anchor='middle'%3E【頭文字1〜2字】%3C/text%3E%3C/svg%3E">
<title>【サービス名 | 会社名】</title>
<meta property="og:site_name" content="【会社名】">
<meta property="og:title" content="【サービス名 | 会社名】">
<meta property="og:url" content="【公開URL】">
<meta property="og:description" content="【description同文でよい】">
<meta property="og:type" content="website">
<!-- og:image は実在URLがある場合のみ追加 -->

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=【テーマのフォント指定】&display=swap" rel="stylesheet">

<script>
// JS有効時のみアニメーション用の非表示スタイルを適用(JS無効でも全文表示される)
document.documentElement.classList.add('js');
</script>

<style>
/* ========== reset ========== */
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
img,svg{max-width:100%;vertical-align:middle;}
ul,ol{list-style:none;}
a{color:inherit;text-decoration:none;}
html{scroll-behavior:smooth;scroll-padding-top:80px;}

/* ========== テーマ変数(03_design_themesの色に差し替える) ========== */
:root{
  --c-main:【メイン色】;
  --c-accent:【アクセント色】;
  --c-ink:【文字色】;
  --c-ink-soft:【補助文字色】;
  --c-bg:【ベース背景】;
  --c-bg-alt:【交互セクション背景】;
  --c-line:【罫線色(背景より少し濃く)】;
  --grad:linear-gradient(120deg,var(--c-main) 0%,var(--c-accent) 100%);
  --radius:16px;
  --shadow:0 12px 40px rgba(0,0,0,.10);
  --font-body:'【本文フォント】',sans-serif;
  --font-head:'【見出しフォント】',sans-serif;
  --font-en:'【英字フォント】',sans-serif;
}
body{font-family:var(--font-body);color:var(--c-ink);background:var(--c-bg);font-size:16px;line-height:1.9;-webkit-text-size-adjust:100%;}
.inner{max-width:1080px;margin:0 auto;padding:0 24px;}
section{padding:96px 0;}
@media(max-width:768px){section{padding:64px 0;}}

/* セクション見出し(英語ラベル+日本語の2段) */
.sec-head{text-align:center;margin-bottom:56px;}
.sec-head .en{font-family:var(--font-en);font-weight:700;font-size:13px;letter-spacing:.35em;color:var(--c-accent);text-transform:uppercase;}
.sec-head .ja{display:block;font-family:var(--font-head);font-size:34px;font-weight:900;line-height:1.4;margin-top:8px;}
.sec-head .lead{margin-top:16px;color:var(--c-ink-soft);font-size:15px;}
@media(max-width:768px){.sec-head .ja{font-size:26px;}}

/* ボタン */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;font-weight:700;border-radius:999px;transition:.3s;cursor:pointer;}
.btn-primary{background:var(--grad);color:#fff;padding:18px 44px;font-size:17px;box-shadow:0 10px 30px rgba(0,0,0,.25);}
.btn-primary:hover{transform:translateY(-3px);}
.btn-line{border:2px solid var(--c-main);color:var(--c-main);padding:15px 40px;font-size:15px;background:transparent;}
.btn-line:hover{background:var(--c-main);color:#fff;}
.btn .arrow{transition:.3s;}
.btn:hover .arrow{transform:translateX(4px);}

/* 固定ヘッダー */
header{position:fixed;inset:0 0 auto 0;z-index:100;padding:14px 0;background:transparent;transition:.3s;}
header.scrolled{background:rgba(255,255,255,.9);backdrop-filter:blur(10px);box-shadow:0 4px 20px rgba(0,0,0,.08);}
.header-in{display:flex;align-items:center;justify-content:space-between;max-width:1160px;margin:0 auto;padding:0 24px;}
.logo{line-height:1.3;font-weight:900;}
.logo .co{font-family:var(--font-head);font-size:18px;color:var(--c-main);}
.logo .en{display:block;font-family:var(--font-en);font-size:10px;letter-spacing:.3em;color:var(--c-accent);}
.gnav{display:flex;align-items:center;gap:26px;}
.gnav a{font-size:14px;font-weight:500;}
.gnav .btn-cta{background:var(--grad);color:#fff;padding:10px 24px;border-radius:999px;font-weight:700;transition:.3s;}
.gnav .btn-cta:hover{transform:translateY(-2px);}
@media(max-width:860px){.gnav a:not(.btn-cta){display:none;}}

/* ヒーロー */
#hero{position:relative;overflow:hidden;padding:180px 0 110px;background:【テーマに合わせた背景。グラデーション+装飾】;}
.hero-in{display:flex;align-items:center;gap:48px;}
.hero-txt{flex:1 1 56%;}
.hero-eyebrow{display:inline-block;font-size:13px;font-weight:700;letter-spacing:.1em;color:var(--c-accent);margin-bottom:22px;}
#hero h1{font-family:var(--font-head);font-size:48px;font-weight:900;line-height:1.45;}
#hero h1 .accent{color:var(--c-main);}
.hero-lead{margin-top:24px;font-size:16px;color:var(--c-ink-soft);max-width:560px;}
.hero-btns{margin-top:36px;display:flex;gap:16px;flex-wrap:wrap;}
.hero-chips{margin-top:38px;display:flex;gap:12px;flex-wrap:wrap;}
.hero-chips li{font-size:13px;font-weight:700;padding:8px 18px;border-radius:999px;background:rgba(255,255,255,.7);border:1px solid var(--c-line);color:var(--c-main);}
.hero-art{flex:1 1 40%;display:flex;justify-content:center;}
@media(max-width:900px){
  #hero{padding:140px 0 80px;}
  .hero-in{flex-direction:column;}
  #hero h1{font-size:32px;}
  .hero-art{width:75%;max-width:340px;}
}

/* 悩み提起 */
#problem{background:var(--c-bg-alt);}
.problem-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:18px;max-width:860px;margin:0 auto;}
.problem-grid li{background:#fff;border-radius:var(--radius);padding:22px 26px;display:flex;gap:14px;box-shadow:var(--shadow);font-weight:500;line-height:1.7;}
.problem-grid .chk{flex:0 0 auto;width:28px;height:28px;border-radius:50%;background:var(--grad);display:grid;place-items:center;margin-top:2px;color:#fff;font-weight:900;font-size:14px;}
.problem-close{text-align:center;margin-top:48px;font-size:22px;font-weight:900;line-height:1.7;}
.problem-close .marker{background:linear-gradient(transparent 62%,color-mix(in srgb,var(--c-accent) 35%,transparent) 62%);}
@media(max-width:768px){.problem-grid{grid-template-columns:1fr;}.problem-close{font-size:18px;}}

/* サービス(01〜の連番) */
.svc-list{display:flex;flex-direction:column;gap:28px;}
.svc{display:flex;gap:32px;align-items:flex-start;background:#fff;border:1px solid var(--c-line);border-radius:var(--radius);padding:36px 40px;box-shadow:var(--shadow);transition:.3s;}
.svc:hover{transform:translateY(-4px);}
.svc-num{font-family:var(--font-en);font-weight:800;font-size:44px;line-height:1;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;flex:0 0 auto;min-width:72px;}
.svc h3{font-family:var(--font-head);font-size:21px;font-weight:900;margin-bottom:4px;}
.svc .en-sub{font-family:var(--font-en);font-size:12px;letter-spacing:.25em;color:var(--c-accent);text-transform:uppercase;display:block;margin-bottom:12px;}
.svc p{color:var(--c-ink-soft);font-size:15px;}
.svc-tags{margin-top:16px;display:flex;flex-wrap:wrap;gap:8px;}
.svc-tags li{font-size:12.5px;padding:5px 14px;border-radius:999px;background:var(--c-bg-alt);border:1px solid var(--c-line);color:var(--c-main);font-weight:700;}
@media(max-width:768px){.svc{flex-direction:column;gap:12px;padding:28px 24px;}.svc-num{font-size:36px;}}

/* 選ばれる理由 */
#reason{background:var(--c-bg-alt);}
.reason-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;}
.reason{background:#fff;border-radius:var(--radius);padding:40px 30px;text-align:center;box-shadow:var(--shadow);border-top:3px solid var(--c-accent);}
.reason .r-num{font-family:var(--font-en);font-weight:800;font-size:14px;letter-spacing:.2em;color:var(--c-accent);display:block;margin-bottom:14px;}
.reason h3{font-family:var(--font-head);font-size:19px;font-weight:900;line-height:1.6;margin-bottom:14px;color:var(--c-main);}
.reason p{font-size:14px;color:var(--c-ink-soft);text-align:left;}
@media(max-width:860px){.reason-grid{grid-template-columns:1fr;max-width:520px;margin:0 auto;}}

/* 料金 */
.price-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;align-items:stretch;}
.price-card{background:#fff;border-radius:var(--radius);padding:40px 30px;text-align:center;box-shadow:var(--shadow);display:flex;flex-direction:column;position:relative;border:2px solid transparent;}
.price-card.featured{border-color:var(--c-main);}
.price-badge{position:absolute;top:-16px;left:50%;transform:translateX(-50%);background:var(--grad);color:#fff;font-size:12.5px;font-weight:700;padding:5px 20px;border-radius:999px;white-space:nowrap;}
.price-card h3{font-family:var(--font-head);font-size:19px;font-weight:900;margin-bottom:6px;}
.price-card .p-sub{font-size:12.5px;color:var(--c-ink-soft);margin-bottom:20px;}
.price-val{font-weight:900;margin-bottom:20px;}
.price-val .num{font-family:var(--font-en);font-size:40px;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;}
.price-val .unit{font-size:14px;color:var(--c-ink-soft);font-weight:700;}
.price-card ul{text-align:left;font-size:14px;flex:1;}
.price-card ul li{padding:9px 0 9px 26px;border-bottom:1px dashed var(--c-line);position:relative;}
.price-card ul li::before{content:"✓";position:absolute;left:2px;color:var(--c-accent);font-weight:900;}
.price-note{text-align:center;margin-top:32px;font-size:13px;color:var(--c-ink-soft);}
@media(max-width:860px){.price-grid{grid-template-columns:1fr;max-width:480px;margin:0 auto;gap:32px;}}

/* 流れ */
.flow-list{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;}
.flow-item{background:#fff;border:1px solid var(--c-line);border-radius:var(--radius);padding:32px 22px;position:relative;box-shadow:var(--shadow);}
.flow-item::after{content:"";position:absolute;top:50%;right:-14px;border-top:8px solid transparent;border-bottom:8px solid transparent;border-left:10px solid var(--c-accent);}
.flow-item:last-child::after{display:none;}
.flow-step{font-family:var(--font-en);font-weight:800;font-size:13px;letter-spacing:.15em;color:var(--c-accent);display:block;margin-bottom:10px;}
.flow-item h3{font-family:var(--font-head);font-size:16.5px;font-weight:900;line-height:1.5;margin-bottom:10px;}
.flow-item p{font-size:13.5px;color:var(--c-ink-soft);}
@media(max-width:900px){
  .flow-list{grid-template-columns:1fr;max-width:520px;margin:0 auto;}
  .flow-item::after{top:auto;right:auto;bottom:-14px;left:50%;transform:translateX(-50%);border-left:8px solid transparent;border-right:8px solid transparent;border-top:10px solid var(--c-accent);border-bottom:none;}
}

/* FAQ */
#faq{background:var(--c-bg-alt);}
.faq-list{max-width:800px;margin:0 auto;display:flex;flex-direction:column;gap:14px;}
.faq-list details{background:#fff;border-radius:14px;box-shadow:var(--shadow);overflow:hidden;}
.faq-list summary{list-style:none;cursor:pointer;padding:22px 56px 22px 26px;font-weight:700;position:relative;font-size:15.5px;line-height:1.6;}
.faq-list summary::-webkit-details-marker{display:none;}
.faq-list summary::before{content:"Q.";color:var(--c-main);font-family:var(--font-en);font-weight:800;margin-right:12px;}
.faq-list summary::after{content:"+";position:absolute;right:24px;top:50%;transform:translateY(-50%);font-size:24px;color:var(--c-main);transition:.3s;}
.faq-list details[open] summary::after{transform:translateY(-50%) rotate(45deg);}
.faq-a{padding:0 26px 24px;font-size:14.5px;color:var(--c-ink-soft);}
.faq-a::before{content:"A.";color:var(--c-accent);font-family:var(--font-en);font-weight:800;margin-right:12px;}

/* 最終CTA */
#cta{background:【メイン色ベースの濃い背景+光のグラデーション】;color:#fff;text-align:center;}
#cta h2{font-family:var(--font-head);font-size:34px;font-weight:900;line-height:1.5;}
#cta p{margin-top:18px;color:rgba(255,255,255,.85);}
#cta .btn-primary{margin-top:36px;font-size:18px;padding:20px 56px;background:#fff;color:var(--c-main);}
#cta .cta-note{margin-top:16px;font-size:13px;color:rgba(255,255,255,.6);}
@media(max-width:768px){#cta h2{font-size:24px;}}

/* フッター */
footer{background:【文字色系の濃色】;color:rgba(255,255,255,.75);padding:56px 0 32px;font-size:13.5px;}
.foot-in{display:flex;justify-content:space-between;gap:32px;flex-wrap:wrap;}
.foot-co .name{color:#fff;font-size:17px;font-weight:900;margin-bottom:10px;font-family:var(--font-head);}
.copy{text-align:center;margin-top:40px;font-size:12px;color:rgba(255,255,255,.45);}

/* スクロールアニメーション(JS無効でも表示される実装) */
.js .reveal{opacity:0;transform:translateY(28px);transition:opacity .8s ease,transform .8s ease;}
.js .reveal.on{opacity:1;transform:none;}
@media(prefers-reduced-motion:reduce){
  html{scroll-behavior:auto;}
  .js .reveal{opacity:1;transform:none;transition:none;}
}
</style>
</head>
<body>

<header id="header">
  <div class="header-in">
    <a href="#" class="logo"><span class="co">【会社名】</span><span class="en">【英字サブ】</span></a>
    <nav class="gnav">
      <a href="#service">サービス</a>
      <a href="#price">料金</a>
      <a href="#flow">流れ</a>
      <a class="btn-cta" href="【CTAのURL】">【CTA文言(短)】</a>
    </nav>
  </div>
</header>

<main>

<!-- ========== ヒーロー ========== -->
<section id="hero">
  <div class="inner hero-in">
    <div class="hero-txt">
      <span class="hero-eyebrow">【地域・ターゲットを示す一言】</span>
      <h1>【キャッチコピー。<span class="accent">強調部分</span>にaccent】</h1>
      <p class="hero-lead">【誰の何をどう解決するか+安心材料。2〜3行】</p>
      <div class="hero-btns">
        <a class="btn btn-primary" href="【CTAのURL】">【CTA文言】<span class="arrow">→</span></a>
        <a class="btn btn-line" href="#service">サービス内容を見る</a>
      </div>
      <ul class="hero-chips">
        <li>✔ 【安心材料1】</li><li>✔ 【安心材料2】</li><li>✔ 【安心材料3】</li>
      </ul>
    </div>
    <div class="hero-art">
      <!-- 業種に合わせたインラインSVGイラスト(創作可。写真URL支給時は<img>+onerror) -->
    </div>
  </div>
</section>

<!-- ========== 悩み提起 ========== -->
<section id="problem">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">Problem</span><span class="ja">こんなお悩みありませんか?</span></div>
    <ul class="problem-grid">
      <li class="reveal"><span class="chk">✓</span>【悩み1(一人称の心の声)】</li>
      <li class="reveal"><span class="chk">✓</span>【悩み2】</li>
      <li class="reveal"><span class="chk">✓</span>【悩み3】</li>
      <li class="reveal"><span class="chk">✓</span>【悩み4】</li>
    </ul>
    <p class="problem-close reveal">【共感+解決宣言。<span class="marker">強調</span>にmarker】</p>
  </div>
</section>

<!-- ========== サービス ========== -->
<section id="service">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">Service</span><span class="ja">サービス内容</span></div>
    <div class="svc-list">
      <div class="svc reveal">
        <span class="svc-num">01</span>
        <div>
          <h3>【サービス名1】</h3><span class="en-sub">【英語サブラベル】</span>
          <p>【機能でなく変化を書く。2〜3行】</p>
          <ul class="svc-tags"><li>【タグ】</li><li>【タグ】</li><li>【タグ】</li></ul>
        </div>
      </div>
      <!-- 02〜05 同構造で繰り返し(3〜5個) -->
    </div>
  </div>
</section>

<!-- ========== 選ばれる理由 ========== -->
<section id="reason">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">Reason</span><span class="ja">選ばれる理由</span></div>
    <div class="reason-grid">
      <div class="reason reveal"><span class="r-num">REASON 01</span><h3>【理由1見出し】</h3><p>【本文】</p></div>
      <div class="reason reveal"><span class="r-num">REASON 02</span><h3>【理由2見出し】</h3><p>【本文】</p></div>
      <div class="reason reveal"><span class="r-num">REASON 03</span><h3>【理由3見出し】</h3><p>【本文】</p></div>
    </div>
  </div>
</section>

<!-- ========== 料金 ========== -->
<section id="price">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">Price</span><span class="ja">料金プラン</span></div>
    <div class="price-grid">
      <div class="price-card reveal">
        <h3>【プラン1】</h3><p class="p-sub">【誰向けか】</p>
        <div class="price-val"><span class="num">【金額】</span><span class="unit">【単位】</span></div>
        <ul><li>【含まれるもの】</li><li>【含まれるもの】</li></ul>
      </div>
      <div class="price-card featured reveal">
        <span class="price-badge">おすすめ</span>
        <h3>【プラン2(主力)】</h3><p class="p-sub">【誰向けか】</p>
        <div class="price-val"><span class="num">【金額】</span><span class="unit">【単位】</span></div>
        <ul><li>【含まれるもの】</li><li>【含まれるもの】</li><li>【含まれるもの】</li></ul>
      </div>
      <div class="price-card reveal">
        <h3>【プラン3】</h3><p class="p-sub">【誰向けか】</p>
        <div class="price-val"><span class="num">【金額】</span><span class="unit">【単位】</span></div>
        <ul><li>【含まれるもの】</li><li>【含まれるもの】</li></ul>
      </div>
    </div>
    <p class="price-note reveal">※【税込/税別】。【追加費用や見積りの注記】</p>
  </div>
</section>

<!-- ========== 流れ ========== -->
<section id="flow">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">Flow</span><span class="ja">ご利用の流れ</span></div>
    <ol class="flow-list">
      <li class="flow-item reveal"><span class="flow-step">STEP.01</span><h3>【手順1】</h3><p>【説明】</p></li>
      <li class="flow-item reveal"><span class="flow-step">STEP.02</span><h3>【手順2】</h3><p>【説明】</p></li>
      <li class="flow-item reveal"><span class="flow-step">STEP.03</span><h3>【手順3】</h3><p>【説明】</p></li>
      <li class="flow-item reveal"><span class="flow-step">STEP.04</span><h3>【手順4】</h3><p>【説明】</p></li>
    </ol>
  </div>
</section>

<!-- ========== FAQ ========== -->
<section id="faq">
  <div class="inner">
    <div class="sec-head reveal"><span class="en">FAQ</span><span class="ja">よくあるご質問</span></div>
    <div class="faq-list reveal">
      <details><summary>【質問1(申込み直前の不安順)】</summary><p class="faq-a">【回答】</p></details>
      <details><summary>【質問2】</summary><p class="faq-a">【回答】</p></details>
      <details><summary>【質問3】</summary><p class="faq-a">【回答】</p></details>
    </div>
  </div>
</section>

<!-- ========== 最終CTA ========== -->
<section id="cta">
  <div class="inner">
    <h2 class="reveal">【行動を促す見出し】</h2>
    <p class="reveal">【行動しない理由を潰す一文】</p>
    <a class="btn btn-primary reveal" href="【CTAのURL】">【CTA文言】<span class="arrow">→</span></a>
    <p class="cta-note">【安心の一言(相談無料・しつこい営業なし等、事実のみ)】</p>
  </div>
</section>

</main>

<footer>
  <div class="inner">
    <div class="foot-in">
      <div class="foot-co">
        <p class="name">【会社名】</p>
        <p>【住所】<br>【営業時間】</p>
      </div>
    </div>
    <p class="copy">Copyright © 【会社名】 All Rights Reserved.</p>
  </div>
</footer>

<script>
// ヘッダーのスクロール時の背景切替
var header = document.getElementById('header');
function onScroll(){
  if(window.scrollY > 40){ header.classList.add('scrolled'); }
  else{ header.classList.remove('scrolled'); }
}
window.addEventListener('scroll', onScroll);
onScroll();

// スクロールで要素をふわっと表示(未対応ブラウザは即表示)
if('IntersectionObserver' in window){
  var io = new IntersectionObserver(function(entries){
    entries.forEach(function(e){
      if(e.isIntersecting){ e.target.classList.add('on'); io.unobserve(e.target); }
    });
  }, {threshold: .15});
  document.querySelectorAll('.reveal').forEach(function(el){ io.observe(el); });
}else{
  document.querySelectorAll('.reveal').forEach(function(el){ el.classList.add('on'); });
}
</script>
</body>
</html>
```

## 補足

- `color-mix()` はマーカー装飾のみに使用(非対応ブラウザでも文字は読める=装飾の劣化で済む)
- ダークテーマ(A・G)ではヘッダーの `.scrolled` 背景を `rgba(10,10,20,.85)` 系に、
  カード背景を `rgba(255,255,255,.05)`+境界線に変更する
- ヒーローのSVGイラストは業種モチーフ(ネットワーク/葉/皿/家など)を単純図形+グラデで描く
