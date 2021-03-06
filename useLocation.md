# ๐ useLocation

ํ์ฌ URL ์ ๋ณด๋ฅผ ๊ฐ์ ธ์จ๋ค.<br />
`useLocation`์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ ๋ผ์ฐํฐ ์ค์น ํ์

```
npm install react-router-dom
```

## ๐์ฌ์ฉ๋ฐฉ๋ฒ

1. useLocation์ import ํ๋ค. <br />
   ```jsx
   import { useLocation } from "react-router-dom";
   ```
2. ๋ณ์์ useLocation ์ ๋ณด๋ฅผ ๋ด๋๋ค.
   ```jsx
   const location = useLocation();
   ```
3. console.log์์ ์ถ๋ ฅํด๋ณด๊ณ , ์ํ๋ ์ ๋ณด๋ฅผ ๊ฐ์ ธ๋ค ์ฌ์ฉํ๋ฉด ๋๋ค.

   ```jsx
   const location = useLocation();

   console.log(locaiton);
   ```

   ์ถ๋ ฅ๊ฒฐ๊ณผ
   ![](/images/useLocation.JPG)

- hash : ์ฃผ์์ #๋ฌธ์์ด ๋ค์ ๊ฐ
- key : location ๊ฐ์ฒด์ ๊ณ ์ ๊ฐ, ์ด๊ธฐ๊ฐ์ default ํ์ด์ง๊ฐ ๋ณ๊ฒฝ๋  ๋ ๋ง๋ค ๊ณ ์ ์ ๊ฐ์ด ์์ฑ๋๋ค.
- pathname : ํ์ฌ ์ฃผ์ ๊ฒฝ๋ก
- search : ?๋ฅผ ํฌํจํ ์ฟผ๋ฆฌ์คํธ๋ง
- state : ํ์ด์ง๋ก ์ด๋์ ์์๋ก ๋ฃ์ ์ ์๋ ์ํ ๊ฐ

https://goddaehee.tistory.com/305

## ๐ useLocation ร TypeScript

โป react-router-dom v6๋ถํฐ ์ ๋ค๋ฆญ์ ์ง์ํ์ง ์๋๋ค.

```tsx
//Coins component
<Link to={`/${coin.id}`} state={{ name: coin.name }}></Link>;
//state์์ ์๋ ๊ฐ์ฒด๊ฐ url์ ๋๊ฒจ์ฃผ๊ธฐ.

//Coin component
interface LoactionParams {
  state: {
    name: string;
  };
}

const state = useLocation() as LocationParams;
```

## ๐ useLocation ร Link state ์์ฑ์ ๋ฌธ์ ์ 

์ํญ์ผ๋ก URL์ ์๋ ฅํ์ฌ ํ๋ฉด์ ์ด์ด๋ณด๋ฉด ์๋ฌ๊ฐ ๋ฐ์ ํ  ๊ฒ์ด๋ค.<br />
์๋ฌ๊ฐ ๋๋ ์ด์ ๋ ์ ํญ์ผ๋ก ํ๋ฉด์ ์ด ๊ฒฝ์ฐ ํด๋น URL์ state๊ฐ์ด ์ ์ ๋์ง ์์์๋ค.<br />
state๊ฐ ์์ฑ๋๋ ค๋ฉด Home ํ๋ฉด์ ๋จผ์  ์ด์ด์ผ ํ๋ค.

```tsx
//coins component

import { Link } from "react-router-dom";
function Coins() {
  return (
    <Link to={`/${coin.id}`} state={{ name: coin.name }}></Link>
    // to๋ก ์ค์ ๋ Url๋ก state๋ฅผ ๋ณด๋ธ๋ค.
  );
}
export default Coins;
```

```tsx
//coin component
import { useState } from "react";
import { useLocation } from "react-router-dom";

interface LocationParams {
  state: {
    name: string;
  };
}

function Coin() {
  const { state } = useLocation() as LocationParams;

  return (
    <>
      <div>{state.name}</div>
      //์ฌ์ฉโ, TypeError:Cannot read properties of undefined(reading name)
      <div>{state?.name || "Loading..."}</div>
      // ํด๊ฒฐ ๋ฐฉ๋ฒ: ์ํญ์์ ์์ธํ๋ฉด URL์ ์๋ ฅํ์ฌ ํ๋ฉด์ ๋ค์ด์ค๋ฉด Loadingํ๋ฉด์
      ๋ณด๊ฒ ๋ง๋ค์ด ์ฃผ์๋ค. // ๊ฒฐ๋ก  : Homeํ๋ฉด์ ํตํด์ ๋ค์ด์จ๋ค๋ฉด, Link๋ก ํด๋น URL๋ก
      ์ด๋ํ๊ธฐ ๋๋ฌธ์ Home์์ ๊ฐ์ ธ์จ state๊ฐ์ ๋ณผ ์ ์์ ๊ฒ์ด๋ค.
    </>
  );
}

export default Coin;
```
