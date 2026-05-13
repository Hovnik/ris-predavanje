# Okvirni projektni plan — IS Program lojalnosti Maestro

## Dokumentni podatki

| Polje        | Vrednost        |
| ------------ | --------------- |
| Verzija      | 1.0             |
| Status       | Delovni osnutek |
| Datum izdaje | 2026-04-15      |
| Avtor        | Martin Hovnik   |

---

## 1. Parametri projekta

| Parameter        | Vrednost                             |
| ---------------- | ------------------------------------ |
| Trajanje         | 12 mesecev (april 2026 – marec 2027) |
| Ekipa            | 5 razvijalcev                        |
| Metodologija     | Scrum, sprinti po 2 tedna            |
| Število sprintov | 26                                   |
| Število izdaj    | 5                                    |
| Ritem izdaj      | Vsake ~2,5 meseca                    |

---

## 2. Sestava ekipe

| Vloga                | Število | Odgovornosti                                      |
| -------------------- | ------- | ------------------------------------------------- |
| Tech lead / arhitekt | 1       | Arhitektura, code review, DevOps, CI/CD           |
| Backend razvijalec   | 2       | Node.js/Express API, Oracle DB, batch processing  |
| Frontend razvijalec  | 2       | Članski portal, administratorski portal (SLO/ANG) |

---

## 3. Pregled izdaj

| Izdaja | Obdobje                  | Sprinti | Fokus                                         |
| ------ | ------------------------ | ------- | --------------------------------------------- |
| R1     | april – junij 2026       | 1–6     | Temelji: infrastruktura, avtentikacija, baza  |
| R2     | julij – september 2026   | 7–12    | Mesečni obračun: uvoz nakupov, statusi, točke |
| R3     | september – oktober 2026 | 13–16   | Admin panel: člani, statistika, nagrade       |
| R4     | november – december 2026 | 17–22   | Pravila, unovčevanje nagrad, izvoz kartic     |
| R5     | januar – marec 2027      | 23–26   | Lokalizacija, zmogljivost, varnost, poliranje |

---

## 4. Podrobnosti po izdajah

---

### R1 — Temelji sistema (sprinti 1–6, april–junij 2026)

**Cilj:** Delujoča infrastruktura, podatkovna baza in registracija/prijava člana.

#### Sprint 1–2: Infrastruktura in podatkovna baza

- Vzpostavitev repozitorija, CI/CD pipeline, okolja (dev / staging / prod)
- Kreacija Oracle DB shem: T1 Stranka, T2 Kraj, T3 Kartica_lojalnosti, T4 Status_stranke, T5 Nivo_lojalnosti
- Node.js/Express projekt: osnovna struktura, `oracledb` connection pool, `.env` konfiguracija
- Seeder: začetni šifranti (T2 kraji, T5 nivoji lojalnosti)

#### Sprint 3–4: Registracija in e-poštna verifikacija

- `POST /api/auth/register` — vnos osebnih podatkov, kreacija T1, T3, T4 z nivojem `osnovni`
- E-poštna verifikacija: generiranje žetona, pošiljanje prek SMTP (`nodemailer`), `POST /api/auth/verify-email`
- `POST /api/auth/login` — bcrypt, JWT z vlogo
- `POST /api/auth/refresh`
- Middleware: `auth.js`, `requireRole.js`, `validate.js`, `errorHandler.js`

#### Sprint 5–6: Članski portal — osnove (frontend)

- Zaslonske maske: registracija (ZM1), prijava, moj-portal (ZM3)
- `GET /api/member/profile` — prikaz profila in trenutnega statusa
- `GET /api/member/points` — prikaz skupnih točk (transakcije bodo prazne do R2)
- `GET /api/member/loyalty-card` — prikaz podatkov o kartici

**Merilo uspešnosti R1:** Stranka se registrira, potrdi e-naslov, prijavi in vidi profil s statusom `osnovni`.

---

### R2 — Mesečni obračun točk in statusov (sprinti 7–12, julij–september 2026)

**Cilj:** Delujoč mesečni obračun — uvoz nakupov, izračun statusov in dodelitev točk.

**Merilo uspešnosti R2:** Administrator uvozi CSV, sproži obračun, sistem pravilno posodobi statuse in dodeli točke.

---

### R3 — Administratorski panel (sprinti 13–16, september–oktober 2026)

**Cilj:** Administrator ima pregled nad člani, statistikami in nagradami.

**Merilo uspešnosti R3:** Administrator vidi člane s filtri, statistike in upravlja katalog nagrad.

---

### R4 — Pravila, unovčevanje nagrad, izvoz kartic (sprinti 17–22, november–december 2026)

**Cilj:** Konfigurabilnost sistema in unovčevanje nagrad za člane.

**Merilo uspešnosti R4:** Član unovči nagrado; administrator nastavi nova pravila točkovnika in pragove prehodov.

---

### R5 — Lokalizacija, zmogljivost in zaključek (sprinti 23–26, januar–marec 2027)

**Cilj:** Produkcijsko pripravljen sistem z lokalizacijo in potrjeno zmogljivostjo.

**Merilo uspešnosti R5:** Sistem uspešno opravi mesečni obračun za 500.000 članov, oba portala delujeta v dveh jezikih, produkcijsko okolje je pripravljeno.

---

## 5. Podrobnosti prvih sprintov

### Sprint 1 (teden 1–2): Infrastruktura

| Naloga                                               | Kdo        |
| ---------------------------------------------------- | ---------- |
| Repozitorij, branching strategija (main/dev/feature) | Tech lead  |
| CI/CD pipeline (build, lint, test)                   | Tech lead  |
| Oracle DB: kreacija shem T1, T2, T3, T4, T5          | Backend 1  |
| Node.js/Express boilerplate, `oracledb` pool         | Backend 2  |
| Seeder: T2 (kraji), T5 (nivoji lojalnosti)           | Backend 1  |
| Osnova frontend projekta, router, layout             | Frontend 1 |
| Zaslonska maska: landing page in navigacija          | Frontend 2 |

### Sprint 2 (teden 3–4): Avtentikacija backend

| Naloga                                                    | Kdo        |
| --------------------------------------------------------- | ---------- |
| `POST /api/auth/register` — validacija, vpis T1 + T3 + T4 | Backend 1  |
| E-poštni servis (`nodemailer`), generiranje žetona        | Backend 2  |
| `POST /api/auth/verify-email`                             | Backend 2  |
| `POST /api/auth/login` — bcrypt, JWT generiranje          | Backend 1  |
| `POST /api/auth/refresh`                                  | Backend 1  |
| Middleware: `auth.js`, `requireRole.js`, `errorHandler`   | Tech lead  |
| Zaslonska maska: registracija (ZM1) — osnova              | Frontend 1 |
| Zaslonska maska: prijava — osnova                         | Frontend 2 |

### Sprint 3 (teden 5–6): Integracija registracije in profil

| Naloga                                                       | Kdo        |
| ------------------------------------------------------------ | ---------- |
| Integracija registracijske forme z `POST /api/auth/register` | Frontend 1 |
| Potek e-poštne verifikacije na frontendu                     | Frontend 1 |
| Prijavni obrazec, shranjevanje JWT, redirect po vlogi        | Frontend 2 |
| `GET /api/member/profile` — endpoint in controller           | Backend 1  |
| `GET /api/member/loyalty-card`                               | Backend 2  |
| Zaslonska maska: moj-portal (ZM3) — profil in status         | Frontend 2 |
| Unit testi: authService, middleware                          | Tech lead  |

---
