# panelokul-blog

Bu klasör, `Beryllium-Software/panelokul-blog` deposunun köküne kopyalanmak üzere hazırlanmış iskelettir. Site deposuna (`kres-platform-web`) pull request açmadan blog yazısı yayınlamak için yazılar burada durur.

Depo **herkese açık** olmalıdır. Site derlemesi jeton kullanmaz; `main` dalını şu adresten alır:

`https://codeload.github.com/Beryllium-Software/panelokul-blog/tar.gz/refs/heads/main`

Dal adı `main` olmalıdır. Depo yoksa veya erişilemezse site, kendi içindeki `src/sections/blog/posts.json` yedeğiyle yayınlanmaya devam eder.

## Kopyalama

Bu klasörün **içini** yeni deponun köküne koyun. Sonuç şöyle görünür:

```text
README.md
schema/post.schema.json
posts/<slug>/index.md
posts/<slug>/cover.jpg
```

`posts/` altındaki beş yazı sitede duran yedeğin aynısıdır. `posts/ornek-yazi/` bir taslaktır; `status: draft` olduğu için kopyalansa da yayına girmez.

Yazıyı bot ile eklemek, güncellemek ve yayından kaldırmak için site deposundaki `docs/blog-yayin-api.md` dosyasına bakın.

## Dosya

Her yazı tek klasördür:

```text
posts/<slug>/index.md
posts/<slug>/cover.jpg
```

`index.md` YAML ön bilgi ile başlar. Gövde, kapanış `---` satırından sonraki Markdown'dır. Ön bilginin şeması `schema/post.schema.json` dosyasındadır.

```yaml
---
title: "Yazı başlığı"
slug: yazi-basligi
meta_description: "Arama sonucu metni. En fazla 155 karakter."
target_keyword: "hedef kelime"
category: okul-yonetimi
tags:
  - Yoklama
author: "PanelOkul Ekibi"
date: 2026-10-11T12:00:00+03:00
date_modified: 2026-10-11T12:00:00+03:00
canonical: https://panelokul.com/blog/yazi-basligi/
status: published
faq:
  - q: "Soru cümlesi?"
    a: "Kısa cevap."
cover: cover.jpg
coverAlt: "Kapağın kısa tarifi"
---

## İlk başlık

Gövde Markdown olarak burada durur.
```

`slug`, klasör adıyla aynı olmalıdır. Küçük harf, rakam ve tire kullanılır.

## Alanlar

| Alan | Kural |
| --- | --- |
| `title` | Zorunlu. En fazla 60 karakter. |
| `slug` | Zorunlu. Klasör adıyla aynı. |
| `meta_description` | Zorunlu. En fazla 155 karakter. Dış yazıda cümlenin belirli bir çağrı metniyle bitmesi gerekmez. |
| `target_keyword` | Zorunlu. En fazla 120 karakter. Sayfada gösterilmez. |
| `category` | `okul-yonetimi`, `veli-iletisimi`, `finans-aidat`, `kvkk-guvenlik`, `urun-haberleri` |
| `tags` | Metin listesi. Boş dizi olabilir. |
| `author` | Boşsa `PanelOkul Ekibi`. |
| `date` | `YYYY-MM-DDTHH:mm:ss+03:00`. Europe/Istanbul duvar saati. |
| `date_modified` | Aynı biçim. |
| `canonical` | İsteğe bağlı. Boşsa `https://panelokul.com/blog/<slug>/`. `https://` ile başlar ve `/` ile biter. |
| `status` | `draft`, `published` veya `scheduled`. |
| `faq` | İsteğe bağlı `{q, a}` listesi. Varsa yazının sonunda görünür ve `FAQPage` şemasına girer. |
| `cover` | İsteğe bağlı. Aynı klasördeki göreli dosya (`cover.jpg`). jpg, jpeg, png veya webp. Önerilen ölçü 1200x630. |
| `coverAlt` | İsteğe bağlı kapak alt metni. Boşsa başlık kullanılır. |

Değerleri tek satırda yazın. İçinde `:` olan metinleri tırnak içine alın.

Yazı içindeki iletişim bağlantısı `/contact-us/` olmalıdır. Sitede `/iletisim/` sayfası yoktur.

## Hangi yazı yayına girer

Derleme saati esas alınır. Tarayıcının saati yazıyı erkenden açmaz.

- `published`: derlemeye girer.
- `scheduled` ve `date` derleme anına eşit ya da ondan önce: derlemeye girer.
- `scheduled` ve `date` gelecekte: girmez.
- `draft`: girmez.

Aynı `slug` hem bu depoda hem sitedeki `posts.json` yedeğinde varsa bu depodaki yazı kazanır. Geçerli bir `draft` veya henüz vakti gelmemiş `scheduled` kayıt, yedekteki aynı slug'ı da gizler.

Bozuk bir yazı (uzun başlık, yanlış kategori, eksik kapak dosyası, kapanmamış ön bilgi) yalnızca kendisi atlanır. Uyarı yazılır, sitenin geri kalanı derlenir.

## Yayından kaldırma

- Tercih edilen yol: `status: draft` yapıp dosyayı güncellemek. Yedekteki aynı slug da gizlenir.
- Yazı yalnızca bu depodaysa `posts/<slug>/index.md` dosyasını silmek yeter. Kapak varsa onu da silin.
- Klasörü silip `status: draft` bırakmamak, slug hâlâ `posts.json` yedeğindeyse yazıyı geri getirir. Yedekteki beş yazı için `draft` kullanın.

## Kapak

Derleme kapağı `dist/blog/covers/<slug>.<uzantı>` yoluna kopyalar. Sitedeki adresi `/blog/covers/<slug>.<uzantı>` olur.
