![lacoste](https://user-images.githubusercontent.com/110226567/217969068-c8139fb6-46b8-48cb-b451-e3e480a4d62a.png)

# ๐ Lacoste

๋ผ์ฝ์คํ ๊ณต์ ์จ๋ผ์ธ ๋ถํฐํฌ ๐ [Demo](https://jone-lacoste.netlify.app)

<br />

## ๐ข ํ๋ก์ ํธ ๊ฐ์

๋ผ์ฝ์คํ ๊ณต์ ์น์ฌ์ดํธ์ ๋์์ธ์ ์ฐธ๊ณ ํ์ฌ ์งํํ ์จ๋ผ์ธ ์ผํ๋ชฐ ํ๋ก์ ํธ์๋๋ค.<br />
๋จ์ํ ์ ํ์ ๋ณด์ฌ์ฃผ๋ ๊ฒ๋ง์ด ์๋, ์ฅ๋ฐ๊ตฌ๋๋ฅผ ํตํด ์ค์ ๋ก ์๋น์ค๋ฅผ ์ด์ฉํ๋ ๊ฒ ๊ฐ์ ๋๋์ ์ฃผ๊ณ  ์ถ์์ต๋๋ค.<br />
์ด๋ฅผ ์ํด ๋ฐ์ดํฐ์ ๋ณ๊ฒฝ ์ฌํญ์ด ์ค์๊ฐ์ผ๋ก ํ๋ฉด์์ ๋ฐ๋ก ์๋ฐ์ดํธ๋๋ ๋ถ๋ถ์ ์ด์ ์ ๋ง์ถ๊ณ  ๊ธฐ๋ฅ์ ๊ตฌํํ์์ต๋๋ค.

<br />

## ๐จ๏ธ ์ฌ์ฉ ๊ธฐ์ 

<p>
  <img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=React&logoColor=black"/>
  <img src="https://img.shields.io/badge/React Router-CA4245?style=flat-square&logo=ReactRouter&logoColor=white"/>
  <img src="https://img.shields.io/badge/React Query-FF4154?style=flat-square&logo=ReactQuery&logoColor=white"/>
  <img src="https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=TailwindCSS&logoColor=white"/>
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=Firebase&logoColor=white"/>
</p>

<br />

## ๐ ์ฃผ์ ๊ธฐ๋ฅ

- ๊ตฌ๊ธ ๊ณ์  ๋ก๊ทธ์ธ
- ์ ํ ์ ์ฒด ๋ฆฌ์คํธ
- ์ ํ ์์ธ ํ์ด์ง
- ์ฅ๋ฐ๊ตฌ๋ ์๋น์ค
- ๋ฐ์ดํฐ๋ฒ ์ด์ค ์ฐ๋

<br />

## ๐ป ์์ค ์ฝ๋

์ ์ฒด ์ฝ๋ ๋ณด๋ฌ ๊ฐ๊ธฐ ๐ [Notion](https://imjone.notion.site/Lacoste-9d78c5adf550498580463c0f9d0d82eb)

### ๐ ํ์ด์ด๋ฒ ์ด์ค ์ธํ

ํ์ด์ด๋ฒ ์ด์ค ์ด๊ธฐ ์ค์  ๋ฐ ๋ฐ์ดํฐ๋ฒ ์ด์ค ๊ด๋ จ API๋ฅผ ์์ฒญํ๋ ๊ณณ์๋๋ค.<br />
์ ๋ฌ ๋ฐ์ ์ธ์๋ฅผ ๋ฐํ์ผ๋ก ๊ฐ์ ธ์ค๊ณ  ์ถ์ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ reference๋ฅผ ๋ช์ํฉ๋๋ค.

```javascript
// firebase.js

const app = initializeApp(firebaseConfig); // ํ์ด์ด๋ฒ ์ด์ค ์ด๊ธฐํ
const database = getDatabase(app);

export const getProducts = async () => {
  return get(ref(database, 'products')).then(snapshot => {
    if (snapshot.exists()) {
      return Object.values(snapshot.val());
    }
    return [];
  });
};

export const getCart = async userId => {
  return get(ref(database, `carts/${userId}`)).then(snapshot => {
    const items = snapshot.val() || {};
    return Object.values(items);
  });
};

export const addOrUpdateCart = async (userId, product) => {
  const productInfo = `${product.title} ${product.color} ${product.size}`;
  return set(ref(database, `carts/${userId}/${productInfo}`), product);
};

export const removeFromCart = async (userId, product) => {
  const productInfo = `${product.title} ${product.color} ${product.size}`;
  return remove(ref(database, `carts/${userId}/${productInfo}`));
};
```

### ๐ ์ปค์คํํ ์ฌ์ฉ

`useQuery`์ ํน์ฑ์ ๋ฐ์ดํฐ๋ฅผ staleํ๋ค๊ณ  ๊ฐ์ฃผํ๊ธฐ ๋๋ฌธ์,<br />
`useMutate`๋ฅผ ์ฌ์ฉํ์ฌ ๋ณ๊ฒฝ ์ฌํญ์ด ํ๋ฉด ์์๋ ๋ฐ๋ก ์๋ฐ์ดํธ๋๋๋ก ํด์ฃผ์์ต๋๋ค.

```javascript
export default function useCart() {
  const { uid } = useUserContext();
  const queryClient = useQueryClient();

  const cartQuery = useQuery(['carts', uid || ''], () => getCart(uid), {
    enabled: !!uid,
  });

  const addOrUpdateItem = useMutation(product => addOrUpdateCart(uid, product), {
    // ํ์ฌ ์ฌ์ฉ์์ uid์ ๊ดํ ์บ์๋ง invalidate
    onSuccess: () => queryClient.invalidateQueries(['carts', uid]),
  });

  const removeItem = useMutation(id => removeFromCart(uid, id), {
    onSuccess: () => queryClient.invalidateQueries(['carts', uid]),
  });

  return { cartQuery, addOrUpdateItem, removeItem };
}
```

<br />

## ๐ ๋ฐฐ์ด ์  ๋ฐ ๋๋ ์ 

- ํ์ผ๋ค์ ๋ณด๊ดํ๊ณ , ๋ฐ์ดํฐ๋ฒ ์ด์ค๋ฅผ ์ฐ๋ํ์ฌ ์ค์๊ฐ์ผ๋ก ํต์ ํ๋ ๊ฒฝํ์ ํด๋ณผ ์ ์์์ต๋๋ค.
- ์ด๋ค ์ํฉ์์ ์ด๋ค ์์ผ๋ก ์ปค์คํํ์ ์์ฑํ์ฌ ์ฌ์ฉํ  ์ ์๋์ง ๊ฐ์ ์ตํ ์ ์์์ต๋๋ค.
- Rํค์๋ ๋จ์๋ก ๊ฒ์ํ์ฌ ๋ชจ๋ฅด๋ ๋ถ๋ถ์ ๋ํด ๋น ๋ฅด๊ฒ ์ฐพ์๋๊ฐ๋ ์๋ น์ ์ตํ ์ ์์์ต๋๋ค.
- React Query์ ์บ์ฑ ์ ๋ต ๋ฐ ์ ๋๋ก ๋ ์ฌ์ฉ๋ฒ์ ๋ค์ ๊ณต๋ถํด์ผ๊ฒ ๋ค๊ณ  ๋๊ผ์ต๋๋ค.
