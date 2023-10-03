## Assignment 3

| Nama | NRP |  Kelas |
|:----:|:---:|:---:|
| Fadilla Rizky Nurhidayah | 5025211110 | Grafkom A |

## RGB Triangle in WebGL

```
function draw() { 
        gl.clearColor(0,0,0,1);  // specify the color to be used for clearing
        gl.clear(gl.COLOR_BUFFER_BIT);  // clear the canvas (to black)
    
        /* Set up values for the "coords" attribute */
    
        let  coords = new Float32Array( [ -0.5,-0.5, 0.5,-0.5, -0.5,0.5 ] );
       
        gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
        gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW);
        gl.vertexAttribPointer(attributeCoords, 2, gl.FLOAT, false, 0, 0);
        gl.enableVertexAttribArray(attributeCoords); 
       
        /* Set up values for the "color" attribute */
       
        let  color = new Float32Array( [ 0,0,1, 0,1,0, 1,0,0 ] );
    
        gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
        gl.bufferData(gl.ARRAY_BUFFER, color, gl.STREAM_DRAW);
        gl.vertexAttribPointer(attributeColor, 3, gl.FLOAT, false, 0, 0);
        gl.enableVertexAttribArray(attributeColor); 
        
        /* Draw the triangle. */
       
        gl.drawArrays(gl.TRIANGLES, 0, 3);
    
        // Second triangle
        let  coords2 = new Float32Array( [ 0.5,0.5, 0.5,-0.5, -0.5,0.5 ] );
    
        gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
        gl.bufferData(gl.ARRAY_BUFFER, coords2, gl.STREAM_DRAW);
        gl.vertexAttribPointer(attributeCoords, 2, gl.FLOAT, false, 0, 0);
        gl.enableVertexAttribArray(attributeCoords);
    
        let  color2 = new Float32Array( [ 0,0,1, 0,1,0, 1,0,0 ] );
    
        gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
        gl.bufferData(gl.ARRAY_BUFFER, color2, gl.STREAM_DRAW);
        gl.vertexAttribPointer(attributeColor, 3, gl.FLOAT, false, 0, 0);
        gl.enableVertexAttribArray(attributeColor);
    
        gl.drawArrays(gl.TRIANGLES, 0, 3);
    
    }
```
- `gl.clearColor(0, 0, 0, 1);` Fungsi ini mengatur warna latar belakang (clear color) pada canvas WebGL. Nilai-nilai RGBA (Red, Green, Blue, Alpha) digunakan di sini. Nilai `(0, 0, 0, 1)` menunjukkan bahwa latar belakang akan diatur menjadi hitam dengan opasitas penuh (tanpa transparansi).
- `gl.clear(gl.COLOR_BUFFER_BIT);` Fungsi ini membersihkan buffer warna (COLOR_BUFFER) pada canvas WebGL dengan menggunakan warna latar belakang yang telah diatur sebelumnya, sehingga menghapus semua gambar yang ada sebelumnya di layar.
- `let coords = new Float32Array([-0.5, -0.5, 0.5, -0.5, -0.5, 0.5]);` mendefinisikan tiga titik dalam bentuk array Float32Array. Setiap titik terdiri dari dua komponen koordinat (x, y) yang mewakili posisi vertex (titik sudut) dari segitiga pertama.
- menghubungkan data koordinat dengan buffer WebGL, menetapkan pointer atribut, dan mengaktifkan atribut "coords" dengan cara berikut: <br>
```
  gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
  gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW);
  gl.vertexAttribPointer(attributeCoords, 2, gl.FLOAT, false, 0, 0);
  gl.enableVertexAttribArray(attributeCoords);
```
  - `gl.bindBuffer():` Mengikat buffer koordinat ke ARRAY_BUFFER WebGL.
  - `gl.bufferData():` Mengisi buffer dengan data koordinat yang telah didefinisikan.
  - `gl.vertexAttribPointer():` Menetapkan pointer atribut "coords" untuk mengambil data dari buffer koordinat.
  - `gl.enableVertexAttribArray():` Mengaktifkan atribut "coords" sehingga data dapat digunakan dalam program shader.
- menggunakan gl.drawArrays() untuk menggambar segitiga pertama dengan menggunakan data yang telah ditentukan sebelumnya `gl.drawArrays(gl.TRIANGLES, 0, 3);`
- mengulangi proses yang sama untuk menggambar segitiga kedua dengan koordinat dan warna yang berbeda.

### Output
<img width="641" alt="Screenshot 2023-10-03 at 13 56 42" src="https://github.com/fadillaarn/GRAFKOM-WEBGL/assets/91003946/8982ef10-1044-434d-9bc7-f75893941b9f">

## 3D Cube WebGL
 ```
 function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    drawPrimitive( gl.TRIANGLE_FAN, [0,1,1,1], [ -0.5,-0.4,-0.5, -0.5,0.4,-0.5, 0.3,0.4,-0.5, 0.3,-0.4,-0.5 ]); // depan
    drawPrimitive( gl.TRIANGLE_FAN, [0,1,0,1], [ -0.3,-0.2,0.5, 0.5,-0.2,0.5, 0.5,0.6,0.5, -0.3,0.6,0.5 ]); // belakang
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,0,1], [ -0.3,0.6,-0.5, -0.5,0.4,0.5, 0.3,0.4,0.5, 0.5,0.6,-0.5 ]); // atas
    drawPrimitive( gl.TRIANGLE_FAN, [0,0,1,1], [ -0.3,-0.2,-0.5, 0.5,-0.2,-0.5, 0.3,-0.4,0.5, -0.5,-0.4,0.5 ]); // bawah
    drawPrimitive( gl.TRIANGLE_FAN, [1,1,0,1], [ 0.5,-0.2,-0.5, 0.5,0.6,-0.5, 0.3,0.4,0.5, 0.3,-0.4,0.5 ]); // sisi kanan
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,1,1], [ -0.3,-0.2,-0.5, -0.5,-0.4,0.5, -0.5,0.4,0.5, -0.3,0.6,-0.5 ]); // sisi kiri

}
```
- `gl.clearColor(0,0,0,1);` Fungsi ini mengatur warna latar belakang (clear color) pada canvas WebGL. Nilai-nilai RGBA (Red, Green, Blue, Alpha) digunakan di sini. Nilai `(0, 0, 0, 1)` menunjukkan bahwa latar belakang akan diatur menjadi hitam dengan opasitas penuh (tanpa transparansi).
- `gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);` Fungsi ini membersihkan buffer warna (COLOR_BUFFER) dan buffer kedalaman (DEPTH_BUFFER) pada canvas WebGL. Ini digunakan untuk menghapus semua gambar yang ada sebelumnya di layar serta mengatur buffer kedalaman untuk tampilan 3D.
- fungsi `drawPrimitive` untuk menggambar enam sisi kubus dengan berbagai warna. Setiap sisi digambar dengan menggunakan `gl.TRIANGLE_FAN`, yang berarti menggambar segitiga dengan titik pusat yang sama untuk setiap sisi.

### Output
<img width="627" alt="Screenshot 2023-10-03 at 13 54 37" src="https://github.com/fadillaarn/GRAFKOM-WEBGL/assets/91003946/218fa79f-8257-4eff-a555-24da41836000">

### Sisi Depan Belakang
<img width="631" alt="Screenshot 2023-10-03 at 13 51 19" src="https://github.com/fadillaarn/GRAFKOM-WEBGL/assets/91003946/60092d48-8b02-42d5-86f1-6ebf03f9c8e2">

### Sisi Atas Bawah
<img width="637" alt="Screenshot 2023-10-03 at 13 51 45" src="https://github.com/fadillaarn/GRAFKOM-WEBGL/assets/91003946/eac2dca3-996f-4f9b-aa8f-8ac06ad4e1a8">

### Sisi Kanan Kiri
<img width="623" alt="Screenshot 2023-10-03 at 13 52 01" src="https://github.com/fadillaarn/GRAFKOM-WEBGL/assets/91003946/a9da4af7-fd95-4f9c-8636-d663017964c3">
