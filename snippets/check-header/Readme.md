# Check Header

## Description

You can fins a detailed description in Harrys repository called [ct](https://github.com/csswizardry/ct#readme).

## How to use it

<!-- START-HOW_TO[] -->




### Bookmark Snippet



<details>

<summary>Copy this code snippet into the bookmark to use it</summary>


```javascript

javascript:(() => {(function () {
    var ct = document.createElement('style');
    ct.innerText = `
    /*!==========================================================================
   #CT.CSS
   ========================================================================== */

/*!
 * ct.css – Let’s take a look inside your <head>…
 *
 * © Harry Roberts 2021 – twitter.com/csswizardry
 */





/**
 * It’s slightly easier to remember topics than it is colours. Set up some
 * custom properties for use later on.
 */

head {
  --ct-is-problematic: solid;
  --ct-is-affected: dashed;
  --ct-notify: #0bce6b;
  --ct-warn: #ffa400;
  --ct-error: #ff4e42;
}/**
 * Show the <head> and set up the items we might be interested in.
 */

head,
head script,
head script:not([src])[async],
head script:not([src])[defer],
head style, head [rel="stylesheet"],
head script ~ meta[http-equiv="content-security-policy"],
head > meta[charset]:not(:nth-child(-n+5)) {
  display: block;
}

head script,
head style, head [rel="stylesheet"],
head title,
head script ~ meta[http-equiv="content-security-policy"],
head > meta[charset]:not(:nth-child(-n+5)) {
  margin: 5px;
  padding: 5px;
  border-width: 5px;
  background-color: white;
  color: #333;
}

head ::before,
head script, head style {
  font: 16px/1.5 monospace, monospace;
  display: block;
}

head ::before {
  font-weight: bold;
}/**
 * External Script and Style
 */

head script[src],
head link[rel="stylesheet"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script[src]::before {
    content: "[Blocking Script – " attr(src) "]"
  }

  head link[rel="stylesheet"]::before {
    content: "[Blocking Stylesheet – " attr(href) "]"
  }/**
 * Inline Script and Style.
 */

head style:not(:empty),
head script:not(:empty) {
  max-height: 5em;
  overflow: auto;
  background-color: #ffd;
  white-space: pre;
  border-color: var(--ct-notify);
  border-style: var(--ct-is-problematic);
}

  head script:not(:empty)::before {
    content: "[Inline Script] ";
  }

  head style:not(:empty)::before {
    content: "[Inline Style] ";
  }/**
 * Blocked Title.
 *
 * These selectors are generally more complex because the Key Selector (\`title\`)
 * depends on the specific conditions of preceding JS--we can’t cast a wide net
 * and narrow it down later as we can when targeting elements directly.
 */

head script[src]:not([async]):not([defer]):not([type=module]) ~ title,
head script:not(:empty) ~ title {
  display: block;
  border-style: var(--ct-is-affected);
  border-color: var(--ct-error);
}

  head script[src]:not([async]):not([defer]):not([type=module]) ~ title::before,
  head script:not(:empty) ~ title::before {
    content: "[<title> blocked by JS] ";
  }/**
 * Blocked Scripts.
 *
 * These selectors are generally more complex because the Key Selector
 * (\`script\`) depends on the specific conditions of preceding CSS--we can’t cast
 * a wide net and narrow it down later as we can when targeting elements
 * directly.
 */

head [rel="stylesheet"]:not([media="print"]):not(.ct) ~ script,
head style:not(:empty) ~ script {
  border-style: var(--ct-is-affected);
  border-color: var(--ct-warn);
}

  head [rel="stylesheet"]:not([media="print"]):not(.ct) ~ script::before,
  head style:not(:empty) ~ script::before {
    content: "[JS blocked by CSS – " attr(src) "]";
  }/**
 * Using both \`async\` and \`defer\` is redundant (an anti-pattern, even). Let’s
 * flag that.
 */

head script[src][src][async][defer] {
  display: block;
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script[src][src][async][defer]::before {
    content: "[async and defer is redundant: prefer defer – " attr(src) "]";
  }/**
 * Async and defer simply do not work on inline scripts. It won’t do any harm,
 * but it’s useful to know about.
 */
head script:not([src])[async],
head script:not([src])[defer] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script:not([src])[async]::before {
    content: "The async attribute is redundant on inline scripts"
  }

  head script:not([src])[defer]::before {
    content: "The defer attribute is redundant on inline scripts"
  }/**
 * Third Party blocking resources.
 *
 * Expect false-positives here… it’s a crude proxy at best.
 *
 * Selector-chaining (e.g. \`[src][src]\`) is used to bump up specificity.
 */

head script[src][src][src^="//"],
head script[src][src][src^="http"],
head [rel="stylesheet"][href^="//"],
head [rel="stylesheet"][href^="http"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-error);
}

  head script[src][src][src^="//"]::before,
  head script[src][src][src^="http"]::before {
    content: "[Third Party Blocking Script – " attr(src) "]";
  }

  head [rel="stylesheet"][href^="//"]::before,
  head [rel="stylesheet"][href^="http"]::before {
    content: "[Third Party Blocking Stylesheet – " attr(href) "]";
  }/**
 * Mid-HEAD CSP disables the Preload Scanner
 */

head script ~ meta[http-equiv="content-security-policy"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-error);
}

  head script ~ meta[http-equiv="content-security-policy"]::before {
    content: "[Meta CSP defined after JS]"
  }/**
 * Charset should appear as early as possible
 */
head > meta[charset]:not(:nth-child(-n+5)) {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

head > meta[charset]:not(:nth-child(-n+5))::before {
  content: "[Charset should appear as early as possible]";
}/**
 * Hide all irrelevant or non-matching scripts and styles (including ct.css).
 *
 * We’re done!
 */

link[rel="stylesheet"][media="print"],
link[rel="stylesheet"].ct, style.ct,
script[async], script[defer], script[type=module] {
  display: none;
}
    `;
    ct.classList.add('ct');
    document.head.appendChild(ct);
}());
})()
``` 




</details>



## Console Tab Snippet

<details>

<summary>Copy this code snippet into the DevTools console Tab to use it</summary>


```javascript

(function () {
    var ct = document.createElement('style');
    ct.innerText = `
    /*!==========================================================================
   #CT.CSS
   ========================================================================== */

/*!
 * ct.css – Let’s take a look inside your <head>…
 *
 * © Harry Roberts 2021 – twitter.com/csswizardry
 */





/**
 * It’s slightly easier to remember topics than it is colours. Set up some
 * custom properties for use later on.
 */

head {
  --ct-is-problematic: solid;
  --ct-is-affected: dashed;
  --ct-notify: #0bce6b;
  --ct-warn: #ffa400;
  --ct-error: #ff4e42;
}/**
 * Show the <head> and set up the items we might be interested in.
 */

head,
head script,
head script:not([src])[async],
head script:not([src])[defer],
head style, head [rel="stylesheet"],
head script ~ meta[http-equiv="content-security-policy"],
head > meta[charset]:not(:nth-child(-n+5)) {
  display: block;
}

head script,
head style, head [rel="stylesheet"],
head title,
head script ~ meta[http-equiv="content-security-policy"],
head > meta[charset]:not(:nth-child(-n+5)) {
  margin: 5px;
  padding: 5px;
  border-width: 5px;
  background-color: white;
  color: #333;
}

head ::before,
head script, head style {
  font: 16px/1.5 monospace, monospace;
  display: block;
}

head ::before {
  font-weight: bold;
}/**
 * External Script and Style
 */

head script[src],
head link[rel="stylesheet"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script[src]::before {
    content: "[Blocking Script – " attr(src) "]"
  }

  head link[rel="stylesheet"]::before {
    content: "[Blocking Stylesheet – " attr(href) "]"
  }/**
 * Inline Script and Style.
 */

head style:not(:empty),
head script:not(:empty) {
  max-height: 5em;
  overflow: auto;
  background-color: #ffd;
  white-space: pre;
  border-color: var(--ct-notify);
  border-style: var(--ct-is-problematic);
}

  head script:not(:empty)::before {
    content: "[Inline Script] ";
  }

  head style:not(:empty)::before {
    content: "[Inline Style] ";
  }/**
 * Blocked Title.
 *
 * These selectors are generally more complex because the Key Selector (\`title\`)
 * depends on the specific conditions of preceding JS--we can’t cast a wide net
 * and narrow it down later as we can when targeting elements directly.
 */

head script[src]:not([async]):not([defer]):not([type=module]) ~ title,
head script:not(:empty) ~ title {
  display: block;
  border-style: var(--ct-is-affected);
  border-color: var(--ct-error);
}

  head script[src]:not([async]):not([defer]):not([type=module]) ~ title::before,
  head script:not(:empty) ~ title::before {
    content: "[<title> blocked by JS] ";
  }/**
 * Blocked Scripts.
 *
 * These selectors are generally more complex because the Key Selector
 * (\`script\`) depends on the specific conditions of preceding CSS--we can’t cast
 * a wide net and narrow it down later as we can when targeting elements
 * directly.
 */

head [rel="stylesheet"]:not([media="print"]):not(.ct) ~ script,
head style:not(:empty) ~ script {
  border-style: var(--ct-is-affected);
  border-color: var(--ct-warn);
}

  head [rel="stylesheet"]:not([media="print"]):not(.ct) ~ script::before,
  head style:not(:empty) ~ script::before {
    content: "[JS blocked by CSS – " attr(src) "]";
  }/**
 * Using both \`async\` and \`defer\` is redundant (an anti-pattern, even). Let’s
 * flag that.
 */

head script[src][src][async][defer] {
  display: block;
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script[src][src][async][defer]::before {
    content: "[async and defer is redundant: prefer defer – " attr(src) "]";
  }/**
 * Async and defer simply do not work on inline scripts. It won’t do any harm,
 * but it’s useful to know about.
 */
head script:not([src])[async],
head script:not([src])[defer] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

  head script:not([src])[async]::before {
    content: "The async attribute is redundant on inline scripts"
  }

  head script:not([src])[defer]::before {
    content: "The defer attribute is redundant on inline scripts"
  }/**
 * Third Party blocking resources.
 *
 * Expect false-positives here… it’s a crude proxy at best.
 *
 * Selector-chaining (e.g. \`[src][src]\`) is used to bump up specificity.
 */

head script[src][src][src^="//"],
head script[src][src][src^="http"],
head [rel="stylesheet"][href^="//"],
head [rel="stylesheet"][href^="http"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-error);
}

  head script[src][src][src^="//"]::before,
  head script[src][src][src^="http"]::before {
    content: "[Third Party Blocking Script – " attr(src) "]";
  }

  head [rel="stylesheet"][href^="//"]::before,
  head [rel="stylesheet"][href^="http"]::before {
    content: "[Third Party Blocking Stylesheet – " attr(href) "]";
  }/**
 * Mid-HEAD CSP disables the Preload Scanner
 */

head script ~ meta[http-equiv="content-security-policy"] {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-error);
}

  head script ~ meta[http-equiv="content-security-policy"]::before {
    content: "[Meta CSP defined after JS]"
  }/**
 * Charset should appear as early as possible
 */
head > meta[charset]:not(:nth-child(-n+5)) {
  border-style: var(--ct-is-problematic);
  border-color: var(--ct-warn);
}

head > meta[charset]:not(:nth-child(-n+5))::before {
  content: "[Charset should appear as early as possible]";
}/**
 * Hide all irrelevant or non-matching scripts and styles (including ct.css).
 *
 * We’re done!
 */

link[rel="stylesheet"][media="print"],
link[rel="stylesheet"].ct, style.ct,
script[async], script[defer], script[type=module] {
  display: none;
}
    `;
    ct.classList.add('ct');
    document.head.appendChild(ct);
}());

``` 




</details>




<!-- END-HOW_TO -->








































































































# Credits

Author: _Harry Roberts_  
Source: _[github.com/csswizardry/ct](https://github.com/csswizardry/ct)_  
