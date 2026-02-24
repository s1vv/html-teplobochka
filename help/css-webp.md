Отлично. Делать нужно сразу правильно, но без фанатизма.

Разберём по шагам.

---

# 1️⃣ Lazy loading

Просто добавляешь атрибут:

```html
<img
  src="images/img1.webp"
  alt="Описание фото 1"
  loading="lazy"
  decoding="async"
/>
```

### Почему ещё `decoding="async"`?

- браузер не блокирует отрисовку
- быстрее рендер
- бесплатная оптимизация

Для статической страницы — must-have.

---

# 2️⃣ Переход на WebP (правильно)

Если ты просто заменишь `.jpg` → `.webp`, это уже хорошо.
Но **правильнее** — использовать `<picture>` с fallback.

Почему?

- старые браузеры (редко, но бывают) не поддерживают WebP
- SEO и валидность лучше

Вот как надо:

```html
<figure class="gallery__item">
  <picture>
    <source srcset="images/img1.webp" type="image/webp" />
    <img
      src="images/img1.jpg"
      alt="Описание фото 1"
      loading="lazy"
      decoding="async"
    />
  </picture>
  <figcaption>Описание 1</figcaption>
</figure>
```

Если тебе вообще не важна поддержка старых браузеров — можно оставить только WebP.

---

# 3️⃣ Как конвертировать в webp (правильно)

В Linux Mint самый простой способ:

### Через cwebp

```bash
sudo apt install webp
cwebp img1.jpg -q 80 -o img1.webp
```

`-q 80` — нормальный баланс качества и веса.

---

### Если фото много

```bash
for f in *.jpg; do
  cwebp "$f" -q 80 -o "${f%.jpg}.webp"
done
```

---

# 4️⃣ Я бы ещё добавил aspect-ratio

Чтобы layout не "прыгал" при загрузке:

Добавь в CSS:

```css
.gallery__item img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  display: block;
}
```

Теперь:

- сетка стабильная
- CLS отсутствует
- выглядит аккуратно

---

# Итоговая рекомендация

Минимально правильно:

- WebP
- loading="lazy"
- decoding="async"
- aspect-ratio
- отдельный CSS

Без JS. Без библиотек. Без лишнего.

---

Если хочешь — могу показать, как сделать ещё более профессионально:
с `srcset` для разных размеров (чтобы мобильным не грузить 2000px картинку).
