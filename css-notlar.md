# CSS Notları

## CSS Specificity (Öncelik Kuralları)

CSS'de hangi stilin uygulanacağını belirleyen **specificity** sistemi vardır. Kod sırası sadece eşit öncelikte kurallar için geçerlidir.

### Specificity Hesaplama

Her CSS seçicisinin bir öncelik değeri vardır:

| Seçici Türü | Değer | Örnek |
|------------|-------|-------|
| Inline Style | 1-0-0-0 | `<div style="color: red">` |
| ID | 0-1-0-0 | `#logo` |
| Class, Attribute, Pseudo-class | 0-0-1-0 | `.info`, `[type="text"]`, `:hover` |
| Element, Pseudo-element | 0-0-0-1 | `div`, `p`, `::before` |

### Örnek Karşılaştırmalar

```css
/* Specificity: 0-0-0-1 (1 element) */
span {
    color: red;
}

/* Specificity: 0-0-1-0 (1 class) */
.primary {
    color: blue;
}

/* Specificity: 0-0-1-1 (1 class + 1 element) */
.info span {
    color: red;
}

/* Specificity: 0-0-2-0 (2 class) */
.info .primary {
    color: blue;
}

/* Specificity: 0-1-0-0 (1 id) */
#para1 {
    color: green;
}

/* Specificity: 0-1-1-0 (1 id + 1 class) - EN YÜKSEK */
#para1.lead {
    color: purple;
}
```
**Basamak gibi düşün:**

0-1-0-0 > 0-0-99-99
         
### Pratik Örnek

```html
<p class="info">
    Lorem ipsum <span class="primary">dolor</span>
</p>
```

```css
.info span {
    color: red;    /* 0-0-1-1 */
}

.info .primary {
    color: blue;   /* 0-0-2-0 - KAZANAN! */
}
```

**Sonuç:** `span` elementi **mavi** olur çünkü `.info .primary` daha spesifiktir.

### Önemli Kurallar

1. **Daha yüksek specificity her zaman kazanır**
2. Eşit specificity'de **son yazılan kural** kazanır
3. `!important` tüm kuralları ezer (kullanımı önerilmez)
4. Araya boşluk konulduğunda "içindeki" anlamına gelir (direkt **çocuk olmak zorunda değil**).



## Bazı Emmet Kısayolları

Visual Studio Code'da HTML ve CSS yazmayı hızlandıran **Emmet** kısayolları kullanabilirsiniz.

### Element + Class

```html
div.box-1
```
**Enter'a basınca:**
```html
<div class="box-1"></div>
```

### Element + ID

```html
div#box-1
```
**Enter'a basınca:**
```html
<div id="box-1"></div>
```

### Element + Birden Fazla Class

```html
div.box-1.active.primary
```
**Enter'a basınca:**
```html
<div class="box-1 active primary"></div>
```

### Class + ID Birlikte

```html
div#main.container
```
**Enter'a basınca:**
```html
<div id="main" class="container"></div>
```

### Element Belirtmeden (varsayılan `div`)

```html
.box-1
```
**Enter'a basınca:**
```html
<div class="box-1"></div>
```

### Diğer Elementlerle

```html
button.btn-primary
span.highlight
p#intro.lead
```
**Enter'a basınca:**
```html
<button class="btn-primary"></button>
<span class="highlight"></span>
<p id="intro" class="lead"></p>
```

### Çoklu Element Oluşturma

```html
div.box-1*3
```
**Enter'a basınca:**
```html
<div class="box-1"></div>
<div class="box-1"></div>
<div class="box-1"></div>
```

**Not:** Emmet kısayolları hem HTML hem de CSS dosyalarında çalışır.
