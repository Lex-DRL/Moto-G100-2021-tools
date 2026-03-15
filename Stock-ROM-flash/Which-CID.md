# Какой CID качать

- [China](https://mirrors-obs-1.lolinet.com/firmware/lenomola/2021/nio_retcn/official/RETCN/)
- [Global](https://mirrors-obs-1.lolinet.com/firmware/lenomola/2021/nio/official/)

У глобалки вот эти всякие `AMXCL`, `AMXCO`, `AMXMX`, ... `TELEU`, `TIMIT` - это вариант прошивки под разные регионы, aka CID (Customer ID). Полный список:
```
AMXCL
AMXCO
AMXMX
AMXPE
ATTMX
OPENCL
OPENMX
OPENPE
RETAIL
RETAPAC
RETAR
RETBR
RETCA
RETEU
RETGB
RETLA
RETUS
TELEU
TIMIT
```

У Китая - соответственно, он один: `RETCN`.

> [!NOTE]
> В архиве с `Tiny-Fastboot-Script` есть файл `tools/aboutcid.txt`, который призван прояснить ситуацию. Но там всё на китайском.
> 
> Я сложил его [распакованный прямо тут](AboutCID-v1.10.6.txt) - пользуйтесь переводчиком, кому интересно.

> [!TIP]
> Узнать, какой именно CID установлен конкретно на вашем телефоне сейчас - можно с помощью этих команд:
> ```
> adb shell getprop ro.build.fingerprint
> adb shell getprop ro.mot.build.customerid
> ```
> 
> Первая выдаст что-то вроде:
> > motorola/nio_**retail**/nio:11/RRTS31.Q1-84-24-1-12/17d50:user/release-keys
> 
> У второй же - будет просто:
> > retail

Однако, результаты выше - это с телефона, купленного в **Бразилии** (на котором, по идее, должен быть `RETBR`).

Я проверил последнюю прошивку для 11 и 12 андроидов у следующих:
- `RETAIL` (универсальная глобальная),
- `RETEU` (общая для EU),
- `RETLA` (общая для латинской америки),
- `RETBR` (типа своя для Бразилии)

... и оказалось, что это **байт-в-байт** один и тот же архив, зачем-то сдублированный в разные папки. Нахрена так сделано - без понятия. 🤷🏻‍♂️

Касаемо же остальных - [Грок](https://grok.com/) выдал следующее:
> - `AMX*`: Claro (America Móvil) LATAM carrier versions — carrier bloat, network-specific apps, slower carrier-dependent updates.
> - `ATT*`: AT&T US carrier — carrier bloat, US-specific apps/setup.
> - `OPEN*`: Open/unlocked retail — no carrier branding/lock, minimal bloat, direct Motorola updates.
> - `RET*`: Retail (direct Motorola, unbranded) — sub-variants by region (RETUS, RETBR, RETEU, RETGB, RETAPAC, etc.); fast updates, low bloat.
> - `TELEU` / `TIMIT`: Specific operators (Telenor, TIM) — operator bloat/apps.

А также:
> `OPEN*` CIDs (`OPENCL`: Chile open retail; `OPENMX`: Mexico open retail; `OPENPE`: Peru open retail) are unlocked, no-network-lock variants for LATAM countries, per docs. Minimal bloat, direct updates, similar to RETLA but country-specific.

Т.е., это, по сути, опять то же самое, что и `RETAIL` (даже если файлы отличаются).
