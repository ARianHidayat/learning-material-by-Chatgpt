Berikut adalah materi tentang pembuatan fitur filter di React.js menggunakan input text dan select option.

---

# 📌 Fitur Filter di React.js

Fitur ini memungkinkan pengguna untuk memfilter daftar berdasarkan teks yang diketik atau opsi yang dipilih.

## 🛠️ Teknologi yang Digunakan

- **React.js**
- **useState** untuk menyimpan nilai input dan opsi
- **Array filter** untuk menyaring data

## 🔹 Langkah-Langkah

### 1️⃣ **Siapkan Data untuk Difilter**

```jsx
const data = [
  { id: 1, name: "Apple", category: "Fruit" },
  { id: 2, name: "Carrot", category: "Vegetable" },
  { id: 3, name: "Banana", category: "Fruit" },
  { id: 4, name: "Tomato", category: "Vegetable" },
];
```

Kita memiliki daftar buah dan sayuran yang akan difilter.

---

### 2️⃣ **Buat State untuk Input dan Opsi**

```jsx
import { useState } from "react";

function FilterComponent() {
  const [searchText, setSearchText] = useState("");
  const [selectedCategory, setSelectedCategory] = useState("");
```

- `searchText` menyimpan teks pencarian
- `selectedCategory` menyimpan kategori yang dipilih

---

### 3️⃣ **Buat Input dan Select Option**

```jsx
  return (
    <div>
      <input
        type="text"
        placeholder="Cari..."
        value={searchText}
        onChange={(e) => setSearchText(e.target.value)}
      />

      <select value={selectedCategory} onChange={(e) => setSelectedCategory(e.target.value)}>
        <option value="">Semua</option>
        <option value="Fruit">Buah</option>
        <option value="Vegetable">Sayur</option>
      </select>
    </div>
  );
}
```

- Input text untuk pencarian
- Select option untuk memilih kategori

---

### 4️⃣ **Filter Data Berdasarkan Input dan Opsi**

```jsx
const filteredData = data.filter(
  (item) =>
    item.name.toLowerCase().includes(searchText.toLowerCase()) &&
    (selectedCategory === "" || item.category === selectedCategory)
);
```

- `includes()` digunakan untuk pencarian teks
- Filter kategori hanya diterapkan jika pengguna memilih opsi

---

### 5️⃣ **Tampilkan Hasil Filter**

```jsx
return (
  <div>
    <input
      type="text"
      placeholder="Cari..."
      value={searchText}
      onChange={(e) => setSearchText(e.target.value)}
    />

    <select
      value={selectedCategory}
      onChange={(e) => setSelectedCategory(e.target.value)}
    >
      <option value="">Semua</option>
      <option value="Fruit">Buah</option>
      <option value="Vegetable">Sayur</option>
    </select>

    <ul>
      {filteredData.map((item) => (
        <li key={item.id}>
          {item.name} - {item.category}
        </li>
      ))}
    </ul>
  </div>
);
```

---

## 🎭 **Analogi**

Bayangkan kamu sedang berada di supermarket dan ingin mencari produk:

- **Input teks** = Mencari barang berdasarkan nama
- **Select option** = Memilih kategori rak tertentu (Buah atau Sayur)
- **Filter bekerja** = Hanya menampilkan produk yang sesuai

---

## 🔥 **Kesimpulan**

- Menggunakan `useState` untuk menyimpan input
- Memanfaatkan `filter()` untuk menyaring data
- Menampilkan daftar yang sudah difilter sesuai input pengguna

Kamu bisa menambahkan fitur **"reset filter"** atau **"sortir"** untuk meningkatkan fungsionalitas. 🚀
