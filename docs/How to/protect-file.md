---
sidebar_position: 3
---

# Cara Memperoteksi file kamu

**Untuk memberikan password pada file langkah yang dapat dilakukan adalah berikut:**

:::danger[Perhatikan!]

protect file hanya  bisa dilakukan dengan sistem operasi 64 bit

:::

1.  Download **[file enkripsi](https://drive.google.com/file/d/1hjEFjHfWJfd11TVkQaxpnRd1McERsjcH/view?usp=sharing)** dan simpan file di local disk D 📂

:::tip[Note]

Pastikan file di simpan pada path localdisk D:\

<details>
  <summary>Jika file disimpan pada path lain</summary>

  ```js title="ubah path encrypt"
Call Shell("D:\encrypt_pdf.exe " & Chr(34) & .Cells(row_number, "A").Value & Chr(34) & " " & Chr(34) & .Cells(row_number, "B").Value & Chr(34), vbNormalFocus)

```

ubah `"D:\`encrypt_pdf.exe " ke path tempat kamu menyimpan file enkripsi tersebut. 
contoh: di ganti ke path berikut: `"C:\`encrypt_pdf.exe "

     
</details>
:::

2.  Masuk ke halaman (sheet) password file

3.  Input path file yang akan di password pada kolom A

    :::danger[PERHATIKAN]
     file yang dapat di password hanya dalam format .pdf saja
    :::

4.  Input password

    :::tip[Note]
    password dapat di input karakter atau angka dengan panjang password  minimal 1 dan  
    maksimal adalah 34 baris
    :::


`Contoh:`
    
     | file Name| Password | 
    |---|---|
    | D:\zein_slip.pdf |123|
    | D:\anomali_slip.pdf  |123| 
    

    :::danger[Perhatikan]
    untuk memperoteksi file maka pada kolom A atau **file name** perlu di input path file atau lokasi dokumen disimpan
    :::

5.  Klik button RUN

    ![alt text](image-1.png)

6.  Akan muncul windows (comand prompt) untuk proses enkripsi, proses enkripsi selesai 
     dilakukan jika semua windows  sudah tertutup. 

    :::tip[Note]
     Sistem operasi dan banyaknya file menentukan lama atau tidaknya proses enkripsi
    :::

