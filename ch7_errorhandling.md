> ๐ฅ ์ค๋ฅ ์ฒ๋ฆฌ๋ ์ค์ํ๋ค. ํ์ง๋ง ์ค๋ฅ ์ฒ๋ฆฌ ์ฝ๋๋ก ์ธํด ํ๋ก๊ทธ๋จ ๋ผ๋ฆฌ๋ฅผ ์ดํดํ๊ธฐ ์ด๋ ค์์ง๋ค๋ฉด ํด๋ฆฐ์ฝ๋๋ผ ๋ถ๋ฅด๊ธฐ ์ด๋ ต๋ค.


# ๐ก ์ค๋ฅ ์ฝ๋๋ณด๋ค ์์ธ๋ฅผ ์ฌ์ฉํ๋ผ

์ค๋ฅ๊ฐ ๋ฐ์ํ๋ฉด ์์ธ๋ฅผ ๋์ง๋ ํธ์ด ๋ซ๋ค. 
๊ทธ๋ฌ๋ฉด **ํธ์ถ์ ์ฝ๋๊ฐ ๋ ๊น๋ํด์ง๋ค.** 
๋ผ๋ฆฌ๊ฐ ์ค๋ฅ ์ฒ๋ฆฌ ์ฝ๋์ ๋ค์์ด์ง ์๊ธฐ ๋๋ฌธ์ด๋ค.

---

# ๐ก Try-Catch-Finally ๋ฌธ๋ถํฐ ์์ฑํ๋ผ

**`try` ๋ธ๋ก**์ **transaction**๊ณผ ๋น์ทํ๋ค. `**try**` ๋ธ๋ก์์ ๋ฌด์จ ์ผ์ด ์๊ธฐ๋ ์ง `**catch**` ๋ธ๋ก์ ํ๋ก๊ทธ๋จ ์ํ๋ฅผ ์ผ๊ด์ฑ ์๊ฒ ์ ์งํด์ผ ํ๋ค.
โ ๊ทธ๋ฌ๋ฏ๋ก ์์ธ๊ฐ ๋ฐ์ํ  ์ฝ๋๋ฅผ ์งค ๋๋ `**try-catch-finally**` ๋ฌธ์ผ๋ก ์์ํ๋ ํธ์ด ๋ซ๋ค.

**`try`** ๋ธ๋ก์์ ๋ฌด์จ ์ผ์ด ์๊ธฐ๋ ์ง ํธ์ถ์๊ฐ ๊ธฐ๋ํ๋ ์ํ๋ฅผ ์ ์ํ๊ธฐ ์ฌ์์ง๋ค.

---

# ๐ก ๋ฏธํ์ธ ์์ธ๋ฅผ ์ฌ์ฉํ๋ผ

- ํ์ธ๋ ์์ธ : ์ปดํ์ผ ๋จ๊ณ์์ ํ์ธ๋๋ฉฐ ๋ฐ๋์ ์ฒ๋ฆฌํด์ผ ํ๋ ์์ธ
    - IOException
    - SQLException
- ๋ฏธํ์ธ ์์ธ : ์คํ ๋จ๊ณ์์ ํ์ธ๋๋ฉฐ ๋ช์์ ์ธ ์ฒ๋ฆฌ๋ฅผ ๊ฐ์ ํ์ง ์๋ ์์ธ
    - NullPointerException
    - IllegalArgumentException
    - IndexOutOfBoundException
    - SystemException

ํ์ฌ๋ ์์ ์ ์ธ ์ํํธ์จ์ด๋ฅผ ์ ์ํ๋ ์์๋ก ํ์ธ๋ ์์ธ๊ฐ ๋ฐ๋์ ํ์ํ์ง๋ ์๋ค๋ ์ฌ์ค์ด ๋ถ๋ชํด์ก๋ค. ๊ทธ๋ฌ๋ฏ๋ก ์ฐ๋ฆฌ๋ ํ์ธ๋ ์ค๋ฅ๊ฐ ์น๋ฅด๋ ๋น์ฉ์ ์์ํ๋ ์ด์ต์ ์ ๊ณตํ๋์ง ๋ฐ์ ธ๋ด์ผ ํ๋ค.

๋น์ฉ? ํ์ธ๋ ์์ธ๋ OCP . Open Closed Principle ๋ฅผ ์๋ฐํ๋ค.
(ํ์ ๋จ๊ณ์์ ์ฝ๋๋ฅผ ๋ณ๊ฒฝํ๋ฉด ์์ ๋จ๊ณ ๋ฉ์๋ ์ ์ธ๋ถ๋ฅผ ์ ๋ถ ๊ณ ์ณ์ผ ํ๋ค๋ ๋ง)

๋๋ก๋ ํ์ธ๋ ์์ธ๋ ์ ์ฉํ๋ค. ์์ฃผ ์ค์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์์ฑํ๋ค๋ฉด ๋ชจ๋  ์์ธ๋ฅผ ์ก์์ผ ํ๋ค. ํ์ง๋ง ์ผ๋ฐ์ ์ธ ์ ํ๋ฆฌ์ผ์ด์์ ์์กด์ฑ์ด๋ผ๋ ๋น์ฉ์ด ์ด์ต๋ณด๋ค ํฌ๋ค.

---

# ๐ก ์์ธ์ ์๋ฏธ๋ฅผ ์ ๊ณตํ๋ผ

์์ธ๊ฐ ๋ฐ์ํ๋ค๋ฉด ๊ตฌ์ฒด์ ์ธ ์ ๋ณด๋ฅผ ์ ๊ณตํ๋ฉด ์ค๋ฅ์ ๋ฐ์ ์์ธ๊ณผ ์์น๋ฅผ ์ฐพ๊ธฐ ์ฌ์์ง๋ค.

- ์ค๋ฅ ๋ฉ์์ง์ ์ ๋ณด๋ฅผ ๋ด๋๋ค.
- ์คํจํ ์ฐ์ฐ ์ด๋ฆ, ์คํจ ์ ํ ์ธ๊ธํ๋ค.


---

# ๐ก ํธ์ถ์๋ฅผ ๊ณ ๋ คํด ์์ธ ํด๋์ค๋ฅผ ์ ์ํ๋ผ

์ค๋ฅ๋ฅผ ์ ์ํ  ๋ ํ๋ก๊ทธ๋๋จธ์๊ฒ ๊ฐ์ฅ ์ค์ํ ๊ด์ฌ์ฌ๋ ์ค๋ฅ๋ฅผ ์ก์๋ด๋ ๋ฐฉ๋ฒ์ด ๋์ด์ผ ํ๋ค.

ํํ ์์ธ ํด๋์ค ํ๋๋ง ์์ด๋ ์ถฉ๋ถํ ์ฝ๋๊ฐ ๋ง๋ค. ์์ธ ํด๋์ค์ ํฌํจ๋ ์ ๋ณด๋ก ์ค๋ฅ๋ฅผ ๊ตฌ๋ถํด๋ ๊ด์ฐฎ์ ๊ฒฝ์ฐ๊ฐ ๊ทธ๋ ๋ค. 

ํ ์์ธ๋ ์ก์๋ด๊ณ  ๋ค๋ฅธ ์์ธ๋ ๋ฌด์ํด๋ ๊ด์ฐฎ์ ๊ฒฝ์ฐ๋ผ๋ฉด ์ฌ๋ฌ ์์ธ ํด๋์ค๋ฅผ ์ฌ์ฉํ๋ผ.

### โจ ๊ฐ์ธ๊ธฐ Wrapper

์ค์ ๋ก ์ธ๋ถ API๋ฅผ ์ฌ์ฉํ  ๋๋ ๊ฐ์ธ๊ธฐ ๊ธฐ๋ฒ์ด ์ต์ ์ด๋ค. ์ธ๋ถ API๋ฅผ ๊ฐ์ธ๋ฉด ์ธ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ํ๋ก๊ทธ๋จ ์ฌ์ด์์ ์์กด์ฑ์ด ํฌ๊ฒ ์ค์ด๋ ๋ค. 

๋ค๋ฅธ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก ๊ฐ์ํ๋ ๋น์ฉ์ด ์ ๋ค. 

์ธ๋ถ API๋ฅผ ํธ์ถํ๋ ๋์  ํ์คํธ ์ฝ๋๋ฅผ ๋ฃ์ด์ฃผ๋ ๋ฐฉ๋ฒ์ผ๋ก ํ๋ก๊ทธ๋จ์ ํ์คํธํ๊ธฐ๋ ์ฌ์์ง๋ค.

ํน์  ์์ฒด๊ฐ API๋ฅผ ์ค๊ณํ ๋ฐฉ์์์ ๋ฐ๋ชฉ ์กํ์ง ์๋๋ค. ํ๋ก๊ทธ๋จ์ด ์ฌ์ฉํ๊ธฐ ํธ๋ฆฌํ API๋ฅผ ์ ์ํ๋ฉด ๊ทธ๋ง์ด๋ค.

---

# ๐ก ์ ์ ํ๋ฆ์ ์ ์ํ๋ผ

### โจ ํน์ ์ฌ๋ก ํจํด Special Case Pattern

: ํด๋์ค๋ฅผ ๋ง๋ค๊ฑฐ๋ ๊ฐ์ฒด๋ฅผ ์กฐ์ํด ํน์ ์ฌ๋ก๋ฅผ ์ฒ๋ฆฌํ๋ ๋ฐฉ์์ด๋ค.
  ํด๋ผ์ด์ธํธ ์ฝ๋๊ฐ ์์ธ์ ์ธ ์ํฉ์ ์ฒ๋ฆฌํ  ํ์๊ฐ ์์ด์ง๋ค.
  ํด๋์ค๋ ๊ฐ์ฒด๊ฐ ์์ธ์ ์ธ ์ํฉ์ ์บก์ํํด์ ์ฒ๋ฆฌํ๋ค.

---

# ๐ก `null`์ ๋ฐํํ์ง ๋ง๋ผ

์ค๋ฅ๋ฅผ ์ ๋ฐํ๋ ํํ ํ์ โ null์ ๋ฐํํ๋ ์ต๊ด

null์ ๋ฐํํ๋ ์ฝ๋๋ ์ผ๊ฑฐ๋ฆฌ๋ฅผ ๋๋ฆด ๋ฟ๋ง ์๋๋ผ ํธ์ถ์์๊ฒ ๋ฌธ์ ๋ฅผ ๋ ๋๊ธด๋ค. โ null ํ์ธ์ ๋นผ๋จน๋๋ค๋ฉด ํต์  ๋ถ๋ฅ์ด ๋ ์ง๋..

null์ ๋ฐํํ๊ณ  ์ถ๋ค๋ฉด โ **์์ธ๋ฅผ ๋์ง๊ฑฐ๋ ํน์ ์ฌ๋ก ๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค.**

---

# ๐ก `null`์ ์ ๋ฌํ์ง ๋ง๋ผ

๋ฉ์๋์์ null ๋ฐํ๋ณด๋ค ๋ฉ์๋๋ก null์ ์ ๋ฌํ๋ ๋ฐฉ์์ด ๋ ๋์๋ค.

์ ์์ ์ธ ์ธ์๋ก null์ ๊ธฐ๋ํ๋ API๊ฐ ์๋๋ผ๋ฉด ๋ฉ์๋๋ก null์ ์ ๋ฌํ๋ ์ฝ๋๋ ์ต๋ํ ํผํ๋ค.

ํธ์ถ์๊ฐ ์ค์๋ก ๋๊ธฐ๋ null์ ์ ์ ํ ์ฒ๋ฆฌํ๋ ๋ฐฉ๋ฒ์ด ์๋ค.

์ธ์๋ก null์ด ๋์ด์ค๋ฉด ์ฝ๋์ ๋ฌธ์ ๊ฐ ์๋ค. ์ ์ด์ null์ ๋๊ธฐ์ง ๋ชปํ๋๋ก ๊ธ์งํ๋ ์ ์ฑ์ด ํฉ๋ฆฌ์ ์ด๋ค. ์ด๋ฐ ์ ์ฑ์ ๋ฐ๋ฅด๋ฉด ์ค์ํ  ํ๋ฅ ๋ ์ค์ด๋ ๋ค.

---

# ๊ฒฐ๋ก 

๊นจ๋ํ ์ฝ๋๋ ์ฝ๊ธฐ๋ ์ข์์ผ ํ์ง๋ง ์์ ์ฑ๋ ๋์์ผ ํ๋ค.

์ค๋ฅ ์ฒ๋ฆฌ๋ฅผ ํ๋ก๊ทธ๋จ ๋ผ๋ฆฌ์ ๋ถ๋ฆฌํด ๋์์ ์ธ ์ฌ์์ผ๋ก ๊ณ ๋ คํ๋ฉด ํผํผํ๊ณ  ๊นจ๋ํ ์ฝ๋๋ฅผ ์์ฑํ  ์ ์๋ค.

์ค๋ฅ ์ฒ๋ฆฌ๋ฅผ ํ๋ก๊ทธ๋จ ๋ผ๋ฆฌ์ ๋ถ๋ฆฌํ๋ฉด ๋๋ฆฝ์ ์ธ ์ถ๋ก ์ด ๊ฐ๋ฅํด์ง๋ฉฐ ์ฝ๋ ์ ์ง๋ณด์์ฑ๋ ๋์์ง๋ค.
