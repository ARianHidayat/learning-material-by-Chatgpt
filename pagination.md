### **🛠️ Panduan Membuat Pagination dengan Tombol yang Terbatas**

Pagination adalah teknik yang membagi data ke dalam beberapa halaman agar lebih mudah diakses. Dalam pagination yang baik, jumlah tombol halaman harus dibatasi agar UI tetap rapi.

Agar pagination bekerja dengan baik, perhatikan **4 aspek utama**:

1. **Data yang Dipaginasi**
   - Tentukan **jumlah total data** dan **jumlah data per halaman**.
2. **Menentukan Halaman Saat Ini**
   - Gunakan **state untuk menyimpan halaman saat ini**.
3. **Menentukan Jumlah Total Halaman**
   - Hitung total halaman berdasarkan total data dan jumlah data per halaman.
4. **Mengontrol Tombol Pagination**
   - **Batasi jumlah tombol** yang ditampilkan agar tidak terlalu panjang.

---

## **📌 Langkah-langkah Membuat Pagination yang Bagus**

Berikut adalah langkah-langkah lengkap beserta analoginya agar lebih mudah dipahami.

### **1️⃣ Hitung Total Halaman**

**🔹 Langkah:**

- Gunakan rumus:  
  **Total Halaman = (Total Data) / (Data Per Halaman)** (dibulatkan ke atas).

**🛠️ Kode:**

```js
const totalPages = Math.ceil(totalPosts / limit);
```

**📖 Analogi:**  
Bayangkan kamu memiliki **100 halaman buku** dan ingin membaca **5 halaman per hari**.  
Maka, **total hari yang dibutuhkan** untuk menyelesaikan buku adalah:  
100 ÷ 5 = 20  
Ini mirip dengan cara kita menghitung **jumlah total halaman pada pagination**.

---

### **2️⃣ Tentukan Rentang Tombol Pagination**

**🔹 Langkah:**

- Tentukan **berapa banyak tombol yang terlihat** (misalnya **5 tombol**).
- Hitung **halaman awal dan halaman akhir** yang akan ditampilkan.

**🛠️ Kode:**

```js
const visiblePages = 5;
let startPage = Math.max(1, currentPage - Math.floor(visiblePages / 2));
let endPage = Math.min(totalPages, startPage + visiblePages - 1);

if (endPage - startPage + 1 < visiblePages) {
  startPage = Math.max(1, endPage - visiblePages + 1);
}
```

**📖 Analogi:**  
Bayangkan kamu sedang **berjalan di trotoar**, dan ada **5 lampu jalan** yang menerangi sekelilingmu.

- Jika kamu **berjalan ke depan**, lampu di belakang **menghilang**, dan lampu baru muncul di depan.
- Jika kamu **mundur**, lampu di depan **menghilang**, dan lampu di belakang muncul kembali.

Begitulah cara tombol pagination bekerja! **Tombol yang ditampilkan selalu berpusat di sekitar halaman saat ini**.

---

### **3️⃣ Buat Array Tombol Halaman**

**🔹 Langkah:**

- Gunakan **loop atau array method** untuk membuat daftar tombol yang akan ditampilkan.

**🛠️ Kode:**

```js
const pageNumbers = Array.from(
  { length: endPage - startPage + 1 },
  (_, index) => startPage + index
);
```

**📖 Analogi:**  
Bayangkan kamu sedang **berjalan di sepanjang peron kereta api**, dan ada **5 papan informasi** yang menunjukkan tujuan kereta.

- Jika kamu **berpindah ke peron berikutnya**, **papan informasi ikut bergeser**.
- Jika kamu kembali, **papan informasi yang lama muncul kembali**.

---

### **4️⃣ Menangani Perubahan Halaman**

**🔹 Langkah:**

- Buat fungsi yang akan memperbarui **halaman saat ini** ketika tombol diklik.

**🛠️ Kode:**

```js
const handlePageChange = (page) => {
  if (page >= 1 && page <= totalPages) {
    setCurrentPage(page);
  }
};
```

**📖 Analogi:**  
Bayangkan kamu berada di **lift dengan 10 lantai**, dan kamu hanya bisa naik atau turun **ke lantai yang tersedia**.

- Jika kamu menekan tombol **di luar jangkauan (misalnya lantai 11)**, lift **tidak bergerak**.
- Jika kamu memilih **lantai dalam jangkauan**, lift akan bergerak ke sana.

---

### **5️⃣ Tampilkan Tombol Pagination dengan Navigasi**

**🔹 Langkah:**

- Tambahkan tombol **Prev dan Next** untuk berpindah halaman.

**🛠️ Kode:**

```jsx
<button
  onClick={() => handlePageChange(currentPage - 1)}
  disabled={currentPage === 1}
>
  Prev
</button>;

{
  pageNumbers.map((item) => (
    <button
      key={item}
      className={item === currentPage ? "active" : ""}
      onClick={() => handlePageChange(item)}
    >
      {item}
    </button>
  ));
}

<button
  onClick={() => handlePageChange(currentPage + 1)}
  disabled={currentPage === totalPages}
>
  Next
</button>;
```

**📖 Analogi:**  
Bayangkan kamu membaca buku dengan **pembatas halaman**.

- Kamu bisa **maju ke halaman berikutnya** (Next).
- Kamu bisa **mundur ke halaman sebelumnya** (Prev).
- Kamu bisa langsung **melompat ke halaman tertentu** dengan memilih angka halaman.

---

## **🎯 Kesimpulan**

1. **Hitung total halaman** berdasarkan jumlah data.
2. **Tentukan rentang tombol** pagination yang akan ditampilkan.
3. **Buat daftar tombol pagination** dengan array.
4. **Tampilkan tombol "Prev" dan "Next"** agar pengguna dapat berpindah dengan mudah.
5. **Gunakan `handlePageChange` untuk menangani navigasi antar halaman**.

Dengan mengikuti langkah-langkah ini, pagination yang kamu buat akan **rapi, responsif, dan nyaman digunakan**! 🚀🔥
