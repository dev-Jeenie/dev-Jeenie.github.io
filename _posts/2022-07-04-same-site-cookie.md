---
published: true
title: "Cookie,Session ๊ทธ๋ฆฌ๊ณ  SameSite ๐ช"
permalink: /life/sameSiteCookie
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-07-04
last_modified_at: 2022-07-04
---
****
![]()

# Cookie์ Session

## 1. ๋ฑ์ฅ๋ฐฐ๊ฒฝ

ํด๋ผ์ด์ธํธ๊ฐ ์ ๋ณด๋ฅผ ์ ์งํ๋ statefulํ ์ฑ๊ฒฉ์ ์๋น์ค๊ฐ ๋ง์์ง<br/>
> (๋ก๊ทธ์ธ์ ํตํด ๋ณผ ์ ์๋ ์๋น์ค, ์ฅ๋ฐ๊ตฌ๋ ๋ฑ)<br/>

๊ทธ๋ฐ๋ฐ <a href="https://dev-jeenie.github.io/CS/whatIsHttp">HTTP์ ํน์ง (๋งํฌ)</a> ์ค **`๋ฌด์ํ(stateless)`**, **`๋น์ฐ๊ฒฐ์ฑ(connectionless)`** ํ์ ์ ๋ณด๋ฅผ ์ ์งํ  ์ ์๋ค. <br/>

์๋ฒ์ ํด๋ผ์ด์ธํธ๊ฐ ํต์ ์ ํ  ๋ ๋ง๋ค ์๋ฒ๋ ํด๋ผ์ด์ธํธ๊ฐ ๋๊ตฌ์ธ์ง ์ธ์ฆ์ ๊ณ์ํด์ผ ํ๋ค. <br/>

๐คท๐ปโโ๏ธ : ์๋ ๋๋ฌด ๋ฒ๊ฑฐ๋กญ์์! ๊ธฐ์ตํ๊ฒ ํ๋ ค๋ฉด ์ด๋ป๊ฒ ํ์ง? <br/>

=> ๊ทธ๋์ ๋์จ ๊ฒ์ด ๋ฐ๋ก **`Cookie`**์ **`session`**! <br/>

ํด๋ผ์ด์ธํธ์ ์ธ์ฆ์ ์ ์งํ๊ธฐ ์ํด ์ฌ์ฉ๋๋ค. <br/>

# ๋ง์ฝ ์ฟ ํค์ ์ธ์์ ์ฌ์ฉํ์ง ์๋๋ค๋ฉด

- ์ผํ๋ชฐ์ ์ ์
- ๋ ๋๊ตฌ์ผ? ๋ก๊ทธ์ธ ํด
- ์ํ ํด๋ฆญ -> ์์ธํ๋ฉด์ผ๋ก ์ด๋
- ๋ ๋๊ตฌ์ผ? ๋ก๊ทธ์ธ ํด
- ์ฃผ๋ฌธ
- ๋ ๋๊ตฌ์ผ? ๋ก๊ทธ์ธ ํด
- ์ ์  ๊ทน๋๋ธ ๐ฅ๐ฅ

=> ์ด๋ฐ์ ์ฌ์ฉ์๋ ์ฌ์ดํธ๋ฅผ ๊บผ๋ฒ๋ฆฌ๊ณ  ๋ง ๊ฒ์ด๋ค. <br/>

# ์ฟ ํค์ ์ธ์์ ์ฌ์ฉํ์ ๊ฒฝ์ฐ

**`์ต์ด ๋ก๊ทธ์ธ`**์ ํ๋ฉด, ์๋ฒ๊ฐ ๊ทธ ์ฌ์ฉ์์ ๋ํ **`์ธ์ฆ์ ์ ์ง`**ํ๋ค. <br/>

์ฆ, <strong style="color:black;background-color:yellow">์ฟ ํค์ ์ธ์์ ํตํด ์๋ฒ๋ ํด๋ผ์ด์ธํธ๋ฅผ ๊ธฐ์ตํ๊ณ  ์๋ ๊ฒ! </strong>


## 2. Cookie๋?

ํด๋ผ์ด์ธํธ ์ธก(๋ธ๋ผ์ฐ์ )์์ ๊ด๋ฆฌ๋๋ **`์์ ๊ธฐ๋ก ์ ๋ณด ํ์ผ`** <br/>

**์ฟ ํค์ ํน์ง**

- ์ฌ์ฉ์ ์ธ์ฆ์ด **`์ ํจํ ์๊ฐ์ ๋ช์`**ํ  ์ ์๋ค
- ํ ๋ฒ ์ ํจ ์๊ฐ์ด ์ ํด์ง๋ฉด **`๋ธ๋ผ์ฐ์ ๋ฅผ ๋๋๋ผ๋ ์ธ์ฆ์ด ์ ์ง`**๋๋ค

### 2-1. ์ฟ ํค ๊ตฌ์ฑ ์์

- ์ด๋ฆ
  - ๊ฐ๊ฐ์ ์ฟ ํค๋ฅผ ๊ตฌ๋ณํ๋ ๋ฐ ์ฌ์ฉ๋๋ ์ด๋ฆ
- ๊ฐ
  - ์ฟ ํค๊ฐ ๊ฐ๊ณ  ์๋ ๊ฐ
- ์ ํจ์๊ฐ
  - ์ฟ ํค์ ์ ์ง์๊ฐ
- ๋๋ฉ์ธ
  - ์ฟ ํค๋ฅผ ์ ์กํ  ๋๋ฉ์ธ
- ๊ฒฝ๋ก
  - ์ฟ ํค๋ฅผ ์ ์กํ  ์์ฒญ ๊ฒฝ๋ก



### 2-2. ์ฟ ํค ๋์ ๋ฐฉ์

์ด์ ์ ํฌ์คํํ <a href="https://dev-jeenie.github.io/cs/CookieSession">cookie, session, token</a> ์ฐธ๊ณ  <br/>

<img src="/assets/images/cookie_works.jpg" /><br/>

- 1) ํด๋ผ์ด์ธํธ๊ฐ ํ์ด์ง๋ฅผ ์์ฒญ
- 2) ์๋ฒ์์ ์ฟ ํค๋ฅผ ์์ฑ
- 3) HTTP ํค๋์ ์ฟ ํค๋ฅผ ํฌํจ์์ผ ์๋ต
  - ์ด ์๋ต์ **`Set-Cookie`** ํค๋๊ฐ ํฌํจ๋์ด ์๋ค
  - ๋ธ๋ผ์ฐ์ ๋ **`Set-Cookie`** ์ ๋ค์ด์๋ ๋ฐ์ดํฐ๋ฅผ ***์ ์ฅ***, ์ด๊ฒ์ด ๋ฐ๋ก **`์ฟ ํค`**
  ```js
    Set-Cookie: normal=yes
  ```

  > ์๋ฒ์์ ์ ์กํ๋ ์๋ต์ ํฌํจ๋ **" Set-Cookie "** ํค๋

<img src="/assets/images/cookie_works_2.jpg" /><br/>

- 4) ๋ธ๋ผ์ฐ์ ๊ฐ ์ข๋ฃ๋์ด๋ ์ฟ ํค ๋ง๋ฃ๊ธฐ๊ฐ์ด ์์ผ๋ ํด๋ผ์ด์ธํธ์์ ๋ณด๊ดํจ
- 5) ์ฟ ํค๊ฐ ์กด์ฌํ๋ฉด, ์์ฒญ์์ HTTP ํค๋์ ์ฟ ํค๋ฅผ ํจ๊ป ๋ณด๋ด์ ์์ฒญ
  ```js
    Cookie: normal=yes;
  ```
  > ๋ธ๋ผ์ฐ์ ์์ ๋ณด๋ด๋ ์์ฒญ์ ํฌํจ๋ **" Cookie "** ํค๋

- 6) ์๋ฒ์์ ์ฟ ํค๋ฅผ ์ฝ์ด ์ด์  ์ํ ์ ๋ณด๋ฅผ ๋ณ๊ฒฝํ  ํ์๊ฐ ์์ ๊ฒฝ์ฐ, ์ฟ ํค๋ฅผ ์๋ฐ์ดํธํด์ ๋ณ๊ฒฝ๋ ์ฟ ํค๋ฅผ HTTP ํค๋์ ํฌํจ์์ผ ์๋ต


์ฟ ํค๋ ์๋ฒ์์ **`์ฌ์ฉ์๋ฅผ ์๋ณํ๊ธฐ ์ํ ์๋จ`**์ผ๋ก ์ฌ์ฉ๋๋ค. </br>

### 2-3. ์ฟ ํค ์ฌ์ฉ ์

- ๋ก๊ทธ์ธ ์, "์์ด๋์ ๋น๋ฐ๋ฒํธ๋ฅผ ์ ์ฅํ์๊ฒ ์ต๋๊น?"
- ์ผํ๋ชฐ์ ์ฅ๋ฐ๊ตฌ๋ ๊ธฐ๋ฅ


## 3. Session์ด๋?
์ธ์์ **์ฟ ํค๋ฅผ ๊ธฐ๋ฐ**์ผ๋ก ํ๊ณ  ์์ง๋ง, `์ฟ ํค`๋ ์ฌ์ฉ์ ์ ๋ณด ํ์ผ์ **`๋ธ๋ผ์ฐ์ ์ ์ ์ฅ`**ํ๊ณ  `์ธ์`์ **`์๋ฒ ์ธก์์ ๊ด๋ฆฌ`**ํ๋ค. <br/>

์๋ฒ์์๋ ํด๋ผ์ด์ธํธ๋ฅผ ๊ตฌ๋ถํ๊ธฐ ์ํด **`์ธ์ ID๋ฅผ ๋ถ์ฌ`**ํ๋ฉฐ ์น ๋ธ๋ผ์ฐ์ ๊ฐ ์๋ฒ์ ์ ์ํด์ ***๋ธ๋ผ์ฐ์ ๋ฅผ ์ข๋ฃํ  ๋๊น์ง*** **`์ธ์ฆ์ํ๋ฅผ ์ ์ง`**ํ๋ค. <br/>

๋ฌผ๋ก  ์ ์ ์๊ฐ์ ์ ํ์ ๋์ด ์ผ์  ์๊ฐ ์๋ต์ด ์๋ค๋ฉด ์ธ์์ ๋๋๋ก ์ค์ ์ด ๊ฐ๋ฅํ๋ค. <br/>

- **์ฌ์ฉ์์ ๋ํ ์ ๋ณด๋ฅผ ์๋ฒ์ ์ ์ฅ**ํ๊ธฐ ๋๋ฌธ์...
  - ์ฟ ํค๋ณด๋ค `๋ณด์`์ ์ข๋ค
  - ์ฌ์ฉ์๊ฐ ๋ง์์ง์๋ก `์๋ฒ ๋ฉ๋ชจ๋ฆฌ`๋ฅผ ๋ง์ด ์ฐจ์งํ๋ค

๋์ ์ ์๊ฐ ๋ง์ ์น ์ฌ์ดํธ์ธ ๊ฒฝ์ฐ ์๋ฒ์ ๊ณผ๋ถํ๋ฅผ ์ฃผ๊ฒ ๋๋ฏ๋ก **`์ฑ๋ฅ ์ ํ์ ์์ธ`** <br/>


### 3-1. ์ธ์ ๋์ ๋ฐฉ์

<img src="/assets/images/Cookie_login.jpeg" /><br/>


- 1) ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์ ์ ์ ์ ์ธ์ ID๋ฅผ ๋ฐ๊ธ
  - **`Set-Cookie`** ํค๋๋ก ์ธ์ ID๋ฅผ ๋ฃ์ด๋๋ค
- 2) ํด๋ผ์ด์ธํธ๋ ์ธ์ ID์ ๋ํด ์ฟ ํค๋ฅผ ์ฌ์ฉํด์ ์ ์ฅ ( ์ด๋ ์ฟ ํค์ ์ด๋ฆ์ JSESSIONID)

<img src="/assets/images/Cookie_login_2.jpeg" /><br/>

- 3) ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์ ๋ค์ ์ ์ ์ ์ด ์ฟ ํค๋ฅผ ์ด์ฉํด์ ์ธ์ ID ๊ฐ์ ์๋ฒ์ ์ ๋ฌ
  - **`Cookie`** ํค๋์ ์ธ์ ID๋ฅผ ๋ฃ์ด์ ์๋ฒ์๊ฒ ์์ฒญ
  - ์๋ฒ๋ ๊ทธ ์ธ์ ID๋ฅผ ์ฝ์ด ์ด๋ค ์ฌ์ฉ์๊ฐ ๋ณด๋ธ ์์ฒญ์ธ์ง ํ๋จํ๋ค


### 3-2. ์ธ์ ํน์ง

- 1) ๊ฐ ํด๋ผ์ด์ธํธ์๊ฒ ๊ณ ์  ID๋ฅผ ๋ถ์ฌ
- 2) ์ธ์ ID๋ก ํด๋ผ์ด์ธํธ๋ฅผ ๊ตฌ๋ถํด์ ํด๋ผ์ด์ธํธ์ ์๊ตฌ์ ๋ง๋ ์๋น์ค ์ ๊ณต
- 3) ์๋ฒ์ ์ ์ฅํ๊ธฐ ๋๋ฌธ์, ์ฟ ํค๋ณด๋ค ๋ณด์ ์ฐ์
- 4) ์ฌ์ฉ์๊ฐ ๋ง์ ์๋ก ์๋ฒ ๋ฉ๋ชจ๋ฆฌ ๋ง์ด ์ฐจ์งํจ

### 3-3. ์ธ์ ์ฌ์ฉ ์

๋ก๊ทธ์ธ ๊ฐ์ ๋ณด์์ ์ค์ํ ์์ ์ํ ์ ์ฌ์ฉ </br>

<!-- **`Set-Cookie`** ํค๋๋ก ์ธ์ ID๋ฅผ ๋ฃ์ด๋๊ณ  -->
์ดํ ์์ฒญ๋ถํฐ ์ ์ก๋  Cookie ํค๋์ ์ธ์ ID๋ฅผ ์ฝ์ด ์ด๋ค ์ฌ์ฉ์์ ์์ฒญ์ธ์ง๋ฅผ ํ๋จํ๋ ๋ฐฉ์์ ์ฌ์ฉํ๋ค. </br>

๋๋ถ๋ถ์ ์น ์ฌ์ดํธ์ ๋ก๊ทธ์ธ ๊ตฌํ์ด ์ด๋ฐ ๋ฐฉ์์ผ๋ก ๊ตฌ์ฑ๋์ด ์๋ค. </br>

## 4. ์ฟ ํค์ ์ธ์์ ์ฐจ์ด

์ญํ ์ด ๋น์ทํ๊ณ , ๋์์๋ฆฌ๋ ๋น์ทํ๋ค. <br/>
๊ทธ ์ด์ ๋ ์ธ์๋ ๊ฒฐ๊ตญ ์ฟ ํค๋ฅผ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ! <br/>

| -- | -- |
| -- | ์ฟ ํค | ์ธ์ |
| **`์ ์ฅ์์น`** | ๋ธ๋ผ์ฐ์  | ์๋ฒ |
| **`์ ์ง๊ธฐ๊ฐ`** | ์ฟ ํค ๋ง๋ฃ๊ธฐ๊ฐ๊น์ง | ๋ธ๋ผ์ฐ์  ์ข๋ฃ์๊น์ง |
| **`๋ณด์`** | ๋น๊ต์  ๋์จ | ๋น๊ต์  ์ข์ |
| **`์์ฒญ์๋`** | ๋น๊ต์  ๋น ๋ฆ | ๋น๊ต์  ๋๋ฆผ |

- 1) ์ฌ์ฉ์ ์ ๋ณด ํ์ผ ์ ์ฅ์์น
  - ์ฟ ํค : ๋ธ๋ผ์ฐ์ 
  - ์ธ์ : ์๋ฒ

- 2) ์ธ์ฆ์ํ ์ ์ง ์๊ฐ
  - ์ฟ ํค : ์ฟ ํค๋ง๋ฃ๊ธฐ๊ฐ๊น์ง
  - ์ธ์ : ๋ธ๋ผ์ฐ์  ์ข๋ฃ ์๊น์ง ์ธ์ฆ์ํ ์ ์ง
    - (์ ์ ์๊ฐ ์ ํ์ผ๋ก ์ผ์ ์๊ฐ ์๋ต์์ผ๋ฉด ์ธ์ ์ข๋ฃ ์ค์  ๊ฐ๋ฅ)

- 3) ๋ณด์
  - ์ฟ ํค : ๋ธ๋ผ์ฐ์ ์ ์ ์ฅํ๊ธฐ ๋๋ฌธ์ ์ข์ง ์์
  - ์ธ์ : ์๋ฒ์ ์ ์ฅ๋๊ธฐ ๋๋ฌธ์ ์ฟ ํค๋ณด๋จ ์ข์
    - (ํ์ง๋ง ์ค๊ฐ์ ํ์ทจ๋นํ  ์ ์์ด์ ์์ ํ์ง ์๋ค)

- 3) ์์ฒญ์๋
  - ์ฟ ํค : ๋น ๋ฆ
  - ์ธ์ : ์ฟ ํค๋ณด๋ค ๋๋ฆผ
    - (์๋ฒ์์ ์ฒ๋ฆฌ๊ฐ ํ์ํ๊ธฐ ๋๋ฌธ์)


์ธ์์ ์ฌ์ฉ์ ์ ๋งํผ ์๋ฒ ๋ฉ๋ชจ๋ฆฌ๋ฅผ ์ฐจ์งํ๊ธฐ ๋๋ฌธ์ <br/>
์์ฆ์ **`ํ ํฐ ๊ธฐ๋ฐ์ ์ธ์ฆ๋ฐฉ์`**์ ์ฌ์ฉํ๋ค. <br/>

๊ทธ ์ค **`JWT(Json Web Token)`**์ด ์๋ค. <br/>
<a href="">JWT ํฌ์คํธ (๋งํฌ)</a>๋ ๋ณ๋๋ก ์ ๋ฆฌํ๋ค. <br/>



# ***๋ฐ์ ํ๋ ์ฟ ํค***, SameSite

์ฟ ํค๋ ๋ณด์๊ณผ ๊ฐ์ธ์ ๋ณด๋ณดํธ๊ฐ ์ทจ์ฝํ๋ค. <br/>
๋ฐ๋ผ์ ๋ธ๋ผ์ฐ์ ๊ฐ ์ฟ ํค๋ฅผ ๋ค๋ฃจ๋ ๋ฐฉ์์ด ์ ์ฐจ ๋ฐ๋์ด๊ฐ๊ณ  ์๋ค. <br/>

๊ทธ ์ค ์ฟ ํค์ ์ถ๊ฐ๋ sameSite ์์ฑ์ ์์๋ณด์. <br/>
## 4. SameSite ์์ฑ


