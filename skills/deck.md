---
name: fitstars-deck
description: Собрать презентацию FitStars в фирменном стиле по брифу, документу или расшифровке звонка. Используй, когда просят презентацию, слайды, деку, презу, «собери презентацию», «сделай слайды», презентацию для встречи, борда, амбассадоров, стратсессии, отчёта или защиты проекта. Не для лендингов, баннеров и креативов.
---

# Презентация FitStars

Собери деку уровня отдела дизайна: фиксированный шаблон, утверждённая палитра,
библиотека иконок и маскота, обязательная приёмка.

**Ты не изобретаешь оформление.** Все числа и правила ниже. Чего здесь нет — не придумывай:
пропусти или спроси. Холст 1920×1080, только пиксели, один HTML-файл.

---

## 1 · Бриф. Не пропускать

Восемь из десяти плохих дек — из недосказанного запроса, а не из слабой сборки.

**Режим** по тому, что принесли:

| Режим | Вход | Что делаешь |
|---|---|---|
| **A · Structured** | готовые слайды или структура | приводишь в вид, дугу автора не ломаешь |
| **B · Document** | документ, текст | режешь на слайды и визуализируешь внутри истории |
| **C · Transcript** | расшифровка созвона | чистишь → опорные тезисы → **фиксируешь историю** → только потом вёрстка |

Для C фиксация обязательна до вёрстки, иначе правки по смыслу придут после и всё переделается.

**Собери и покажи на подтверждение:** режим · аудитория · регистр языка · тезис одним
предложением · что зритель должен понять или сделать · число слайдов · нужен ли mobile review ·
обязательные элементы (цифры, логотипы, дисклеймеры).

Недостающее добери **2–4 вопросами, не больше**. Человека нет на связи — возьми самое разумное
прочтение, напиши сверху какое, продолжай.

**Роли слайдов** (смысловые, не визуальные): `cover` контекст и обещание · `shift` ломает
ожидание · `meaning` перевод в интерес зрителя · `proof` данные и сравнение · `case` живое
доказательство · `mechanism` как работает · `ask` что сделать вместе · `thesis` финал-унос.

## 2 · Язык

Выбери **один** регистр, не смешивай.

- **Consumer** — продукт, соцсети, рассылки. Дружелюбно, просто, можно смайлы и лёгкий юмор.
- **Ambassadors** — комьюнити, школа. Теплее, «мы вместе», энергия. Без внутренних шуток команды.
- **Board** — топ-менеджмент, стратсессия. Простой, живой, профессиональный.
  **Запрещено:** внутренний сленг, грубые обороты («льём», «просели», «убили») кроме прямой
  цитаты, англицизмы-глаголы («дотюнить», «челленджить»), мемы и смайлы в заголовках.

**Висячие предлоги — запрещено во всех регистрах.** Короткие служебные слова не остаются в
конце строки: `а и в к с у о на по из за от до не ни для без при про под над или чем что как`.
Чинится `&nbsp;` после слова (`в&nbsp;2026`, `не&nbsp;тематика`) или `<br>` **перед** словом.
Прогони перед сдачей все заголовки, лиды, буллеты.

## 3 · Шаблон

Слайд — flex-колонка. Шапка фиксированная, тело течёт от верха, футер прижат к низу.

```
Холст   1920 × 1080
Поля    лево/право 120 · верх 90 · низ 70
.hd     высота 230 (зона 90…320), ширина 1520
.bd     старт y=320, прижато к верху, guard 24 над футером
.ft     y=974, высота 36
```

**Content Fit, жёстко.** Содержимое `.bd` ≤ **630px**: `1080 − 90 − 70 − 230 − 36 − 24 = 630`.
Пропорции медиа считай в бюджет **до** вёрстки: `h = ширина_колонки × (h÷w)`.
Не влезает — другая пропорция, другая ширина, или паттерн «фото | текст».
Три фото 4:5 в ряд на полосе 1680 — не влезают (≈676px).

### Скелет CSS

```css
:root{
  --pink:#EF16B0; --navy:#181D31; --body:#3A3F52; --mut:#86868B;
  --grn:#1A9E7A; --coral:#D4635E; --amb:#C98A3F;
  --bg:#FFFFFF; --card:#FFFFFF; --line:rgba(24,29,49,.08);
  --c-lav:#F6F3FF; --c-sky:#ECF6FF; --c-peach:#FFF3EB; --c-rose:#FFF1F1;
  --c-pink:#FFF1FA; --c-lilac:#FCEDFF; --c-mint:#ECFBFA; --c-aqua:#EEF8FA;
  --c-chart:#EBEDF1;
  --r:32px; --r-inner:20px;
  --font:'Gilroy','Manrope',-apple-system,'Segoe UI',sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--font);background:#0E1119;color:var(--body);-webkit-font-smoothing:antialiased}
.holder{position:relative;overflow:hidden;background:#fff}
.slide{position:absolute;top:0;left:0;width:1920px;height:1080px;transform-origin:top left;
  background:var(--bg);overflow:hidden;display:flex;flex-direction:column;padding:90px 120px 70px}
.hd{flex:none;width:1520px;height:230px}
.kick{display:inline-flex;align-items:center;gap:13px;font-size:20px;font-weight:700;
  color:var(--pink);text-transform:uppercase;letter-spacing:.11em;line-height:30px}
.kick::before{content:"";width:26px;height:3px;background:var(--pink);border-radius:3px}
h2{font-size:52px;line-height:1.1;font-weight:700;color:var(--navy);letter-spacing:-1.4px;margin-top:18px}
.src{font-size:19px;font-weight:500;color:var(--mut);margin-top:20px}
.bd{flex:1;min-height:0;display:flex;flex-direction:column;justify-content:flex-start;
  padding-bottom:24px;overflow:hidden}
.ft{flex:none;position:relative;height:36px;display:flex;align-items:center}
.ft .lg{display:flex;align-items:center;gap:11px}
.ft .lg .wm{font-size:24px;font-weight:700;color:var(--navy);letter-spacing:-.5px}
.ft .cap{position:absolute;left:50%;transform:translateX(-50%);font-size:15px;font-weight:500;color:#A6AAB5}
.ft .pg{margin-left:auto;font-size:17px;font-weight:600;color:var(--mut)}
.card{background:var(--card);border:1px solid rgba(24,29,49,.05);border-radius:var(--r);
  box-shadow:0 1px 2px rgba(24,29,49,.05),0 14px 36px rgba(24,29,49,.08);
  padding:46px 48px;display:flex;flex-direction:column;justify-content:flex-start;height:auto}
.card.comfort{padding:69px 48px}
.mint{background:var(--c-mint)} .sky{background:var(--c-sky)} .pinkt{background:var(--c-pink)}
.lav{background:var(--c-lav)} .peach{background:var(--c-peach)} .aqua{background:var(--c-aqua)}
.rose{background:var(--c-rose)} .lilac{background:var(--c-lilac)}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:36px;align-items:stretch}
.grid3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:28px;align-items:stretch}
.h3{font-size:28px;font-weight:700;color:var(--navy);letter-spacing:-.5px}
.big{font-size:72px;line-height:1;font-weight:700;letter-spacing:-1px;color:var(--navy)}
.big.pk{color:var(--pink)}
.lbl-u{font-size:20px;font-weight:600;color:var(--mut);margin-top:16px;line-height:1.45}
.txt{font-size:22px;line-height:1.5;font-weight:500;color:var(--body)}
ul.pts{list-style:none}
ul.pts li{position:relative;padding-left:32px;font-size:21px;line-height:1.45;font-weight:500;
  color:var(--navy);margin-bottom:20px}
ul.pts li::before{content:"";position:absolute;left:0;top:11px;width:9px;height:9px;
  border-radius:50%;background:var(--pink)}
.take{margin-top:20px;padding-top:20px;border-top:1px solid var(--line);font-size:22px;
  font-weight:700;color:var(--navy);line-height:1.35;display:flex;gap:12px;align-items:flex-start}
.take::before{content:"→";color:var(--pink);font-weight:700;flex:none}
.ico-plate{width:120px;height:120px;border-radius:20px;background:#fff;display:flex;
  align-items:center;justify-content:center;flex:none;
  box-shadow:0 1px 2px rgba(24,29,49,.05),0 8px 20px rgba(24,29,49,.06);margin-bottom:18px}
.ico-plate img{width:78px;height:78px;object-fit:contain}
.ico-bare{display:block;width:140px;height:140px;object-fit:contain;margin:0 0 20px;flex:none}
.chip{display:inline-flex;align-items:center;justify-content:center;background:#fff;
  border-radius:999px;padding:10px 18px;font-size:17px;font-weight:700;line-height:1.1;
  box-shadow:0 1px 2px rgba(24,29,49,.05);color:var(--navy)}
.media{width:100%;border-radius:var(--r);overflow:hidden;position:relative}
.media.r45{aspect-ratio:4/5} .media.r34{aspect-ratio:3/4} .media.r11{aspect-ratio:1/1}
.media.r43{aspect-ratio:4/3} .media.r32{aspect-ratio:3/2} .media.r169{aspect-ratio:16/9}
.media>img{width:100%;height:100%;object-fit:cover;display:block;position:absolute;inset:0}
.media.stretch{aspect-ratio:auto;height:100%;min-height:0;align-self:stretch}
.slide.brandbg{background:linear-gradient(150deg,#FF8FC4 0%,#FFAEB6 52%,#FFD3AC 100%);
  justify-content:center}
.brandbg .decostar{position:absolute;left:1020px;top:50%;transform:translateY(-50%);
  width:1350px;height:1350px;opacity:.22;z-index:0;filter:brightness(0) invert(1)}
.brandbg .cwrap{position:relative;z-index:2;width:100%;max-width:920px}
.brandbg .ck{font-size:24px;font-weight:700;color:#fff;text-transform:uppercase;letter-spacing:.14em}
.brandbg h1{font-size:112px;line-height:1;font-weight:700;color:#fff;letter-spacing:-3.5px;margin-top:26px}
.brandbg h1.fin{font-size:96px;letter-spacing:-2.8px}
.brandbg .csub{display:inline-block;margin-top:40px;background:#fff;border-radius:22px;
  padding:18px 34px;font-size:26px;font-weight:600;color:var(--navy)}
.brandbg .fsub{margin-top:32px;font-size:30px;line-height:1.4;font-weight:500;
  color:rgba(255,255,255,.94);max-width:880px}
.brandbg .ft .wm{color:#fff}
.brandbg .ft .lg .st{filter:brightness(0) invert(1)}

/* Печать → PDF. Каждый слайд = страница 1920×1080.
   !important обязателен: скрипт ставит transform и height инлайном. */
@media print{
  @page{size:1920px 1080px;margin:0}
  html,body{background:#fff !important;width:1920px !important;margin:0 !important;
            height:auto !important;overflow:visible !important}
  /* режим показа прячет слайды и зажимает контейнер — иначе PDF выйдет на одной странице */
  .deck{height:auto !important;display:block !important;overflow:visible !important}
  .holder{display:block !important}
  .holder{width:1920px !important;height:1080px !important;overflow:hidden !important;
          break-after:page;page-break-after:always;break-inside:avoid}
  .holder:last-child{break-after:auto;page-break-after:auto}
  .slide{position:relative !important;transform:none !important;
         width:1920px !important;height:1080px !important}
  *{-webkit-print-color-adjust:exact !important;print-color-adjust:exact !important}
}
```

Масштабирование: `.slide` скейлится под ширину `.holder` через `transform:scale(ширина/1920)`,
высота holder = `1080 × scale`.

## 4 · Типографика

| Роль | Кегль | Вес | Трекинг |
|---|---|---|---|
| Kicker | 20 | 700 | caps, .11em |
| Заголовок h2 | 52 (длинный — 46) | 700 | −1.4 |
| Подзаголовок | 19 | 500 | 0 |
| H3 в карточке | 24–28 | 700 | −0.5 |
| Hero-число (один на слайд) | 130–200 | 700 | отриц. |
| Big-число в карточке | 62–88 | 700 | отриц. |
| Body / буллет | 21 | 500 | 0 |
| Подпись числа | 16–20 | 500–600 | 0 |
| Футер caption | 15 | 500 | 0 |
| Обложка h1 | 112 | 700 | −3.5 |
| Финал h1 | 72–96 | 700 | −2.8 |

Gilroy: Regular 400 · Medium 500 · Semibold 600 · Bold 700. **Extrabold и выше не используем.**

**Шрифт подключается ссылкой, ставить его не надо.** В начало `<style>` деки —
ровно этот блок, иначе вёрстка поедет: кегли и межбуквенное рассчитаны под Gilroy.

```css
@font-face{font-family:'Gilroy';src:url('https://raw.githubusercontent.com/evgorlov/fitstars-ai/main/assets/Fonts/Gilroy/Gilroy-Regular.woff2') format('woff2');font-weight:400;font-display:block}
@font-face{font-family:'Gilroy';src:url('https://raw.githubusercontent.com/evgorlov/fitstars-ai/main/assets/Fonts/Gilroy/Gilroy-Medium.woff2') format('woff2');font-weight:500;font-display:block}
@font-face{font-family:'Gilroy';src:url('https://raw.githubusercontent.com/evgorlov/fitstars-ai/main/assets/Fonts/Gilroy/Gilroy-Semibold.woff2') format('woff2');font-weight:600;font-display:block}
@font-face{font-family:'Gilroy';src:url('https://raw.githubusercontent.com/evgorlov/fitstars-ai/main/assets/Fonts/Gilroy/Gilroy-Bold.woff2') format('woff2');font-weight:700;font-display:block}
```

Дека тянет шрифт при открытии, поэтому первый показ требует интернета.
Если деку отправляют вложением или будут смотреть офлайн — шрифт и картинки
надо вшить внутрь файла, это умеет `deck-selfcontained.py` из папочной сборки.

**Правила.** Крупное — число, не заголовок: перепад h2 ≈52 против hero 130+ обязателен.
Заголовок не длиннее двух строк, лучше одна. Ниже 19 на контенте не опускаться, 15 только футер.
Межстрочное: заголовки ~1.1, тело ~1.45. Слабый тезис кеглем не лечится.

## 5 · Цвет

**Заливка карточки — строго один из восьми:** lav `#F6F3FF` · sky `#ECF6FF` · peach `#FFF3EB` ·
rose `#FFF1F1` · pink `#FFF1FA` · lilac `#FCEDFF` · mint `#ECFBFA` · aqua `#EEF8FA`.
Или белая база — **только** на слайдах со свечением. **Серого в палитре нет.**

Текст: navy `#181D31` заголовки · body `#3A3F52` основной · mut `#86868B` подписи.
Розовый `#EF16B0` — **один акцент на слайд**, точечно.
Семантика: рост `#1A9E7A` · спад `#D4635E` · осторожно `#C98A3F` (редко).
Столбцы графика: default `#EBEDF1`, выделенный — pastel из палитры, не яркий.

**Отдельные категории, под правило палитры не подпадают:** точные цвета логотипов соцсетей,
функциональные нейтрали (хейрлайны, плейсхолдер фото), цвет текста.

**Пары пастелей согласованы по тону:** peach↔pink · mint↔aqua · lav↔lilac · sky↔aqua.
Не делай sky+pink единственной парой всей деки и не повторяй одну пару на трёх слайдах подряд.

**Белое на белом:** вторичная плашка на белом слайде не держится на одной тени — хейрлайн
`1.5px solid var(--line)` или пастель из восьми. Серый fill — нет.

## 6 · Карточки

**Два режима, не смешивать в одном смысловом блоке:**
- **Glow + белые карточки** — табло, сравнения, витрина. Свечение только под белыми.
- **Цветные без свечения** — кейсы, пары, эмоция. Фон слайда белый.

Одиночная белая карточка среди цветных запрещена. Больше двух glow-слайдов подряд — нет.

**Auto-layout как в Figma:** ширина Fill (`flex:1 1 0` или `1fr`), высота Hug (по контенту),
ряд Stretch (`align-items:stretch`). Равная высота берётся **только** из stretch.

**Запрещено на карточке по вертикали:** `height`, `min-height`, `height:100%`, `flex:1`
ради заполнения `.bd`, `align-self:start` в ряду, `justify-content:center` ради заполнения пустоты.

**Зазор в ряду по числу карточек:** 2 → **36** · 3 → **28** · 4 → **24** · 5+ → **20**.
Один фиксированный gap на все случаи — ошибка.

**Паддинг:** база 46 верт / 48 гориз. Для метрик и блоков с воздухом — comfort 69 / 48.
Вложенный контейнер легче родительского: радиус 32 → 20, паддинг меньше, тень слабее.

**Icon-plate** — белый квадрат 120×120 r20 с иконкой 78 внутри, **только на цветных** карточках.
На белых — иконка без фрейма и крупнее (`.ico-bare` ~140).

**Мало контента → укрупняй, а не оставляй пусто.** Дыра больше ~40% плашки — дефект,
лечится содержанием и auto-layout, не ручной высотой. Текст в карточке: h3 ≥ 26, тело ≥ 21.

## 7 · Медиа

Высоту фото задаёт **пропорция**, не контент и не остаток `.bd`. Пиксельная высота запрещена.
Одна пропорция на смысловой ряд. Внутри рамки — `object-fit:cover`.
Люди и портреты 4:5 или 3:4 · действие и зал 3:2 или 16:9 · плитки 1:1 · контент 4:3.
Фото рядом с текстовой карточкой — высоту задаёт текст, фото тянется через stretch.

## 8 · Обложка и финал

Градиент `150deg #FF8FC4 → #FFAEB6 → #FFD3AC`, текст белый.
Звезда **белая на 22%**, 1350×1350, левый край x=1020, центр по вертикали, bleed вправо.
Не оставляй розовую заливку с низкой прозрачностью — получится розовая звезда; нужен
`filter:brightness(0) invert(1)`.
Текст в `.cwrap` до 920px, чтобы не залезать на звезду. Логотип внизу слева, белый.

**Фирменная звезда FitStars — с разрывом наверху. Это намеренно, не «чинить».**

## 9 · Иконки и маскот

**Только из библиотеки. С нуля не рисуем, промтом не генерируем.** Разброс от запуска к запуску —
главный источник расфокуса бренда. Всё с прозрачным фоном, без непрозрачной подложки.

База: `https://raw.githubusercontent.com/evgorlov/fitstars-ai/main/assets/`
- иконки: `Icons/opt/256/<Имя>.webp` (мастера `Icons/<Имя>.svg` весят до 3 МБ — не бери)
- маскот: `Cats/named/<имя>.png`

Если адрес не открывается — спроси человека, не подставляй что-то похожее.

**Иконка отвечает за смысл блока, котик — за эмоцию.** Не путай роли.
Иконка не заменяет реальный скриншот, если материал есть.

**Имена иконок по смыслу:**
`Barbell` `Dumbbells` `Weights` `Sports_Mat` `Fabric_Bands` `Massage_Roll` `Tape_measure`
`Meditation_Lotus1/3/5` `Marathon_Cup` `Football` · `Bag_money` `Upward_dynamics`
`Downward_dynamics` `Rocket` `Darts` `Fire` `Bon_Fire` `Lightning_bolt` `Lightning_bolt_circle` ·
`Cloud_Chat2/3` `Mail` `Mail_Open` `Note` `Note_check` `Note_check2` `Notification_bell`
`Profile` `Video_circle` `Locker` `Refresh2` · `Calendar` `Clock2` · `Book` `Book_open`
`Lamp_light` `Sun` `Crescent_moon` `Thermometer` `Trash` `Close_no` `Boat` ·
`FitStar_Star` `FitStar_Star_circle` `Star` `Star2` `Sparkles_stars` `Spinning_stars`
`Confetti` `Confetti_Stars` `Confetti_Petard` `Gift` `Gift2` `Garland_flags` ·
`Avocado` `Banana2` `Broccoli2` `Carrot` `Green_Apple` `Lemon2` `Egg` `Salad` `Fish_Salmon`
`Fish_Sushi` `Coffee_cup` `Tea_cup` · `Hand_Like` `Hand_shake` `Hand_Flexed_biceps`
`Hand_heart` `Hand_Imagination` `Finger_Up` · `Heart` `Heart2` `Broken_heart` `Breath_smile`
`Eye_smile` `Love_eyes_smile` `Sad_smile` `Rest_Sleep_smile`.
Все имена с суффиксом `_img`: `Rocket_img.webp`.

**Выбор маскота — по валентности материала.** Определи `+` / `0` / `−` и бери ту же.
Негативный кот только на негативном слайде. «Задумчивый» ≠ «стратегическая рамка».

| Имя | Вал. | Когда |
|---|---|---|
| `confident` | + | сильный тезис, рамка, board |
| `proud` | + | успех, рост, итоги |
| `excited` | + | новость, запуск, wow |
| `jump-joy` | + | победа, достижение |
| `wave-hi` | + | приветствие, онбординг |
| `heart` · `heart-hands` | + | комьюнити, забота, благодарность |
| `star` | + | награда, звёзды, milestone |
| `celebrate` · `confetti-sit` · `balloon` | + | праздник, поздравление |
| `king` · `king-proud` | + | премиум, топ-тариф |
| `discount` | + | скидка, оффер (табличка 70%) |
| `app` | + | продукт, приложение |
| `hero-flag` · `hero-strong` · `hero-fit` | + | цель, сила, челлендж |
| `dumbbells-up` · `kettlebell` · `mat-step` · `barbell-win` | + | тренировка, прогресс |
| `duo-five` | + | комьюнити, парная работа, рефералы |
| `peek-thumb` · `peek-bottom` | +/0 | угол баннера, врезка |
| `cool` · `cheeky` | + | дерзко, consumer; на board осторожно |
| `sign-pink` · `sign-white` | 0 | носитель произвольной надписи |
| `question` · `thinking` | 0 | вопрос, выбор |
| `business` · `office` | 0 | board, процесс |
| `fix` | 0 | техработы, продукт, техдолг |
| `time` | 0 | дедлайн, таймер акции |
| `reading` | 0 | знание, гайд |
| `meditation` · `sleep-curl` · `sleep-bed` | 0 | отдых, восстановление |
| `neutral-sit` | 0 | базовый кадр |
| `puzzled` | − | непонимание, проблема пользователя |
| `stressed` | − | выгорание, перегрузка |
| `barbell-hard` | − | тяжело, барьер |
| `driving` | − | спешка, нет времени |
| `sad` · `skeptical` · `crying` | − | спад, сомнение, провал |

**Лимит: не больше двух котиков на деку, на board обычно один.** Не ставь котика на KPI,
на деньги и на списки владельцев. Если ставишь — крупно, примерно в половину высоты контента,
не крошечным стикером. Плоский кот 2019 запрещён.

## 10 · Ритм деки

Перед сдачей напиши карту типов слайдов. Лимиты: не больше двух glow подряд; не больше двух
одинаковых цветовых схем подряд; каждые 3–4 информационных слайда — переключатель
(statement, крупное число, скрин, фото, смена режима карточек).

Слайд не должен быть клоном соседа по приёму.

**Если слайд получается текстовым и скучным**, по порядку: скриншоты и реальные материалы →
иконки → схема или шаги → крупная цифра → котик → смена паттерна.

## 11 · Приёмка. Без неё не сдавать

Пройди по каждому слайду.

**Геометрия.** Поля 120/90/70 · шапка 230 · тело стартует y=320 и прижато к верху ·
содержимое ≤630 и не лезет в футер · зазор по таблице Card Group · паддинг 46/48 или 69/48 ·
на карточках нет заданной высоты · у медиа высота только из пропорции.

**Цвет.** Каждая заливка карточки — из восьми или белая на glow. Ни одного серого и ни одного
подобранного на глаз оттенка. Свечение только под белыми. Внутри блока один приём.
Один розовый акцент на слайд. Звёзды обложки и финала белые.

**Композиция.** Есть главный объект, взгляд идёт туда первым. Нет дыр в карточках.
Нет мёртвых зон. Блок не «падает» вниз. Слайд не клон соседа.

**Типографика.** Тело не дублирует число или фразу заголовка. Буллеты ≥21. Крупные числа
не слиплись. Заголовок ≤2 строк.

**Язык.** Регистр выдержан. На board нет сленга. **Висячих предлогов нет.**

**Ассеты.** Иконки и котик из библиотеки, с прозрачностью. Ссылки живые.

**Mobile review** — обязателен, если отдаёшь HTML по ссылке. На узком экране слайд должен
переверстаться в колонку со скроллом, а **не** масштабироваться в миниатюру: текст станет
нечитаем. Триггер `max-width:1100px` или `max-aspect-ratio:1/1`: сбросить transform, слайд во
всю ширину, высота auto, сетки в одну колонку, своя типографическая шкала. Десктопные числа
при этом не трогать. Проверь, что нет горизонтального скролла.

Отчёт критика в конце:

```
AD-pass · <имя деки> · vN
Fail: слайд X — …
Pass: …
```

## 12 · Экспорт в PDF, PNG и PPTX

**PDF — без инструментов.** В шаблоне есть слой `@media print`: каждый слайд печатается
отдельной страницей 1920×1080. Открыть деку в браузере, Cmd+P → «Сохранить как PDF»,
поля «Нет», фон включить. Работает у любого сотрудника, ничего ставить не надо.

**Важно для шаблона с режимом показа.** Если в деке есть режим показа (`body.present`),
он прячет все слайды кроме текущего и зажимает контейнер в высоту экрана — PDF выйдет
на одной странице. В печатном слое это надо снять:
`html,body{height:auto!important}` · `.deck{height:auto!important;display:block!important;overflow:visible!important}`
· `.holder{display:block!important}`.

**PNG и PPTX из этого PDF:**

```
python3 deck-export.py "дека.pdf"            # PNG 144 dpi + PPTX 16:9
python3 deck-export.py "дека.pdf" --pptx     # только PPTX
python3 deck-export.py "дека.pdf" --dpi 220  # крупнее, под печать
```

Браузер не нужен, нужны `pdftoppm` и `python-pptx`. Скрипты `deck-export.py` и `render.js`
лежат в проекте отдела дизайна; если их нет под рукой — хватит печати в PDF, это основной путь.

**Если есть Chromium или Chrome** — можно без ручной печати:

```
node render.js "дека.html"            # PDF и PNG сразу
CHROME_PATH="/path/to/chrome" node render.js "дека.html"
```

**Слайды в PPTX — картинки, текст в PowerPoint не редактируется.** Это осознанный размен:
вёрстка сохраняется один в один. Правки вносятся в HTML, потом экспорт заново. Скажи об этом
человеку, когда отдаёшь PPTX, чтобы он не рассчитывал править текст на месте.

## 13 · Выдача

Версии не перезаписываются: правки → `vN+1`, старая остаётся. Имя: `Имя — тема · vN.html`.

**На согласование нужен URL, не файл.** HTML-вложение в мессенджере не откроется как
презентация, а без ассетов страница развалится. Собери тонкий пакет: `index.html` плюс только
использованные ассеты, пути относительные.

Если показываешь результат внутри Claude — ассеты публикуй вместе со страницей файлами:
ссылки на внешний CDN оттуда не загрузятся.

**Правило ревью.** Внутренняя встреча, отчёт, рабочий материал — ревью дизайнера не нужно.
Борд, инвесторы, партнёры, публикация наружу — **обязательно**. Скажи об этом прямо.

## 14 · Чего не делать

- Не тащить в презентацию продуктовую дизайн-систему: кнопки, инпуты, табы, состояния
  интерфейса, плотные карточки «как в кабинете». Презентация — не экран приложения.
- Не изобретать цвета и не подбирать оттенки на глаз.
- Не «чинить» разрыв в фирменной звезде.
- Не ставить вес шрифта выше 700.
- Не задавать карточке фиксированную высоту.
- Не центрировать тело слайда по вертикали.
- Не оставлять висячие предлоги.
- Не рисовать иконки stroke-SVG «из головы», когда есть библиотека.
- Не компенсировать слабый тезис кеглем — сначала история, потом вёрстка.
