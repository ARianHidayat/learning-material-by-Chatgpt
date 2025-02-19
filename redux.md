Oke, kita akan membahas **cara install dan menggunakan Redux di Next.js**, termasuk:  
✅ **Instalasi Redux** di proyek Next.js  
✅ **Konfigurasi store dan penyimpanan data global**  
✅ **Penjelasan `useSelector` dan `useDispatch`**  
✅ **Best practice struktur folder dalam proyek Next.js**

---

## **1️⃣ Instalasi Redux di Next.js**

Buka terminal di root proyek Next.js, lalu jalankan perintah berikut untuk menginstal Redux dan Redux Toolkit:

```bash
npm install @reduxjs/toolkit react-redux
```

atau jika menggunakan **yarn**:

```bash
yarn add @reduxjs/toolkit react-redux
```

📌 **Penjelasan:**

- `@reduxjs/toolkit` → Memudahkan konfigurasi Redux
- `react-redux` → Untuk menghubungkan Redux dengan komponen React

---

## **2️⃣ Setup Redux Store di Next.js**

Kita buat **Redux Store** yang akan menyimpan state global.

### **📂 Struktur Folder Redux yang Direkomendasikan**

```
/project-root
 ├── /redux
 │   ├── store.js       # Store utama Redux
 │   ├── /slices
 │   │   ├── counterSlice.js  # Contoh slice untuk counter
 │   │   ├── authSlice.js     # Contoh slice untuk autentikasi
```

### **📌 a. Buat `store.js` (Redux Store)**

Buat folder `redux`, lalu buat file `store.js` di dalamnya.

```javascript
// redux/store.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./slices/counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

📌 **Penjelasan:**

- Kita menggunakan `configureStore` dari Redux Toolkit.
- Semua **reducers** (data global) akan dimasukkan ke dalam `reducer` di store ini.

---

### **📌 b. Buat `counterSlice.js` (Contoh State)**

Buat folder `slices`, lalu buat file `counterSlice.js` di dalamnya.

```javascript
// redux/slices/counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    reset: (state) => {
      state.value = 0;
    },
  },
});

export const { increment, decrement, reset } = counterSlice.actions;
export default counterSlice.reducer;
```

📌 **Penjelasan:**

- `createSlice()` digunakan untuk membuat state global yang bernama **counter**.
- `reducers` berisi fungsi-fungsi untuk mengubah state (seperti `increment`, `decrement`, dan `reset`).
- Fungsi-fungsi tersebut harus diekspor (`export const`) agar bisa digunakan di komponen lain.

---

## **3️⃣ Pasang Redux ke Next.js**

Di **Next.js**, Redux harus dibungkus dengan **Provider** agar state bisa digunakan di seluruh aplikasi.

### **📌 Modifikasi `_app.js`**

Buka atau buat file `_app.js` di dalam folder `pages`, lalu edit seperti ini:

```javascript
// pages/_app.js
import { Provider } from "react-redux";
import { store } from "../redux/store";

export default function App({ Component, pageProps }) {
  return (
    <Provider store={store}>
      <Component {...pageProps} />
    </Provider>
  );
}
```

📌 **Penjelasan:**

- Redux membutuhkan **Provider** agar seluruh aplikasi bisa mengakses state global.
- `store` berisi semua data global yang kita buat.

---

## **4️⃣ Menggunakan Redux di Komponen**

Sekarang kita bisa menggunakan **Redux di dalam komponen Next.js**.

### **📌 a. Menggunakan `useSelector` untuk Mengambil Data**

`useSelector` digunakan untuk **mengambil** data dari Redux.

Misalnya, kita ingin menampilkan **nilai counter** di halaman utama `index.js`:

```javascript
// pages/index.js
import { useSelector } from "react-redux";

export default function Home() {
  const counter = useSelector((state) => state.counter.value);

  return (
    <div>
      <h1>Counter: {counter}</h1>
    </div>
  );
}
```

📌 **Penjelasan:**

- `useSelector((state) => state.counter.value)` → Mengambil nilai counter dari store Redux.

---

### **📌 b. Menggunakan `useDispatch` untuk Mengubah State**

`useDispatch` digunakan untuk **memanggil action** yang mengubah state.

Sekarang, tambahkan tombol **increment dan decrement** di halaman `index.js`:

```javascript
// pages/index.js
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement, reset } from "../redux/slices/counterSlice";

export default function Home() {
  const counter = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>Counter: {counter}</h1>
      <button onClick={() => dispatch(increment())}>Tambah</button>
      <button onClick={() => dispatch(decrement())}>Kurang</button>
      <button onClick={() => dispatch(reset())}>Reset</button>
    </div>
  );
}
```

📌 **Penjelasan:**

- `useDispatch()` → Digunakan untuk mengakses Redux dispatcher.
- `dispatch(increment())` → Memanggil fungsi **increment** dari `counterSlice.js`.

---

## **5️⃣ Best Practice Penempatan Folder Redux di Next.js**

Berikut **struktur folder terbaik** untuk proyek Next.js dengan Redux:

```
/project-root
 ├── /pages
 │   ├── _app.js      # Memasukkan Redux Provider
 │   ├── index.js     # Menggunakan Redux untuk Counter
 │   ├── about.js     # Halaman lain
 │
 ├── /redux
 │   ├── store.js     # Store utama Redux
 │   ├── /slices
 │   │   ├── counterSlice.js  # Counter state
 │   │   ├── authSlice.js     # Contoh auth state
 │
 ├── /components
 │   ├── Navbar.js    # Navbar yang bisa pakai Redux
 │   ├── Footer.js    # Footer
 │
 ├── /styles
 │   ├── global.css   # Styling global
 │
 ├── package.json
 ├── next.config.js
 ├── README.md
```

📌 **Alasan menggunakan struktur ini:**

- **Folder `/redux`** → Menyimpan semua konfigurasi Redux di satu tempat.
- **Folder `/slices`** → Setiap state disimpan di file terpisah untuk kemudahan pemeliharaan.
- **Folder `/components`** → Komponen yang bisa menggunakan Redux di dalamnya.

---

## **Kesimpulan**

🚀 Sekarang kamu sudah tahu cara menggunakan Redux di Next.js!

- **Instal Redux** menggunakan `@reduxjs/toolkit`.
- **Buat Redux Store** dan gunakan di `_app.js`.
- **Gunakan `useSelector`** untuk mengambil data Redux.
- **Gunakan `useDispatch`** untuk mengubah state Redux.
- **Gunakan best practice struktur folder** agar proyek tetap rapi.
