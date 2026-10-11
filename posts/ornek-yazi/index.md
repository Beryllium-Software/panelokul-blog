---
title: "Örnek yazı taslağı"
slug: ornek-yazi
meta_description: "Bu dosya içerik deposunun örnek taslağıdır. Yayına almak için status değerini published yapın."
target_keyword: "örnek blog yazısı"
category: urun-haberleri
tags:
  - Örnek
author: "PanelOkul Ekibi"
date: 2026-10-11T12:00:00+03:00
date_modified: 2026-10-11T12:00:00+03:00
canonical: https://panelokul.com/blog/ornek-yazi/
status: draft
faq:
  - q: "Bu yazı sitede görünür mü?"
    a: "Hayır. status draft olduğu sürece derleme bu klasörü yayına almaz."
coverAlt: "Örnek kapak görseli"
---

## Bu bir şablondur

Yayınlanacak yazının gövdesi bu çizginin altında, Markdown olarak durur. `status` değeri `published` olunca yazı bir sonraki site derlemesinde çıkar. İleriki bir saat için `scheduled` kullanın; `date` derleme anına gelince yazı yayına girer.

Kapağı aynı klasöre `cover.jpg` olarak koyun ve ön bilgiye `cover: cover.jpg` satırını ekleyin. Ölçü 1200x630 olsun.

## Yayından kaldırma

`status` değerini `draft` yapın. Yazı yalnızca bu depodaysa klasörü silmek de yeter.
