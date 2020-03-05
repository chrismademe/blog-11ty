---
author: Chris Galbraith
title: WooCommerce Auto Generated Coupons Throw an Error at Checkout
date: "2020-03-04T10:13:32.169Z"
description: How to fix auto generated coupon codes throwing an error when placing an order in WooCommerce 3.9+
tags:
    - post
    - code
    - php
    - wordpress
    - woocommerce
layout: post
---

```php
/**
 * Disable Stock hold for checkout
 *
 * This is to fix an issue where an applied coupon creates
 * an error when placing an order.
 *
 * @see https://wordpress.org/support/topic/auto-generated-coupon-code-not-working/
 */
add_filter('woocommerce_hold_stock_for_checkout',  '__return_false');
```
