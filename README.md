# Project-Fibonacci

Nama   :  Muhamad David Ali
Nim    :  312210291
Kelas  : TI.22.A1
Matakuliah : Pemrograman Mobile 1
Dosen Pengampu : Donny Maulana, S.Kom., M.M.S.I.,

# Membuat Layout
**1.** buat file baru 
Tambahkan ```Button (limit)```, ```Button(count)```, ```Button (Toast)```, ```TextView```
![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/4eac7680-23de-494c-89f7-b90654279709)

**2. Membuat Tampilan Layout** 
Buat pada activity.xml
**Button Set Limit**
Membuat  Tampilan Button untuk Set Limit unutk mengatur Limit Fibonacci,  untuk ukuran ```layout``` tidak harus mengikuti sesuaikan dengan ukuran device cobalah untuk mengatur nya sendiri, lakukan uji coba secara terus menerus sampai sesuai dengan device
```
<Button
  android:id="@+id/button_toast"
  android:layout_width="380dp"
  android:layout_height="49dp"
  android:layout_marginStart="0dp"
  android:layout_marginTop="8dp"
  android:layout_marginEnd="0dp"
  android:background="@color/colorPrimaryDark"
  android:onClick="setLimit"
  android:text="@string/button_label_toast"
  android:textColor="@android:color/white"
  app:layout_constraintEnd_toEndOf="parent"
  app:layout_constraintStart_toStartOf="parent"
  app:layout_constraintTop_toTopOf="parent" />
```

**Button Count**
Membuat  tampilan Button untuk Fibonacci untuk menabah Fibonacci, untuk ukuran ```layout``` tidak harus mengikuti sesuaikan dengan ukuran device cobalah untuk mengatur nya sendiri, lakukan uji coba secara terus menerus sampai sesuai dengan device
```
<Button
  android:id="@+id/button_count"
  android:layout_width="190dp"
  android:layout_height="48dp"
  android:layout_marginStart="8dp"
  android:layout_marginBottom="8dp"
  android:layout_marginEnd="0dp"
  android:background="@color/colorPrimaryDark"
  android:onClick="countUp"
  android:text="@string/button_label_count"
  android:textColor="@android:color/white"
  app:layout_constraintBottom_toBottomOf="parent"
  app:layout_constraintEnd_toEndOf="parent"
  app:layout_constraintHorizontal_bias="0.0"
  app:layout_constraintStart_toStartOf="parent"
  tools:ignore="UsingOnClickInXml,VisualLintButtonSize"
  />
```

**Button Toast**
Membuat tampilan Button Toast untuk reset Fibonacci, untuk ukuran ```layout``` tidak harus mengikuti sesuaikan dengan ukuran device cobalah untuk mengatur nya sendiri, lakukan uji coba secara terus menerus sampai sesuai dengan device
```
<Button
  android:id="@+id/button_finish"
  android:layout_width="190dp"
  android:layout_height="48dp"
  android:layout_marginStart="0dp"
  android:layout_marginEnd="8dp"
  android:layout_marginBottom="8dp"
  android:background="@color/colorPrimaryDark"
  android:onClick="back1"
  android:text="@string/button_label_finish"
  android:textColor="@android:color/white"
  app:layout_constraintBottom_toBottomOf="parent"
  app:layout_constraintEnd_toEndOf="parent"
  app:layout_constraintHorizontal_bias="1.0"
  app:layout_constraintStart_toStartOf="parent"
  tools:ignore="UsingOnClickInXml"
  />
```

**Membuat Layout TextView Fibonacci**
membuat tambpilan layout dan textAngka
```
<TextView
  android:id="@+id/show_count"
  android:layout_width="0dp"
  android:layout_height="0dp"
  android:layout_marginStart="8dp"
  android:layout_marginTop="8dp"
  android:layout_marginEnd="8dp"
  android:layout_marginBottom="8dp"
  android:gravity="center_vertical"
  android:text="@string/count_initial_value"
  android:textAlignment="center"
  android:textColor="@color/colorPrimaryDark"
  android:textSize="160sp"
  android:textStyle="bold"
  app:layout_constraintBottom_toTopOf="@id/button_count"
  app:layout_constraintEnd_toEndOf="parent"
  app:layout_constraintStart_toStartOf="parent"
  app:layout_constraintTop_toBottomOf="@id/button_toast"
  tools:ignore="RtlCompat"
  />
```

# Membuat String Name
buat pada string.xml
agar bisa memanggil nama.
```
<resources>
    <string name="app_name">appFibonacci</string>
    <string name="button_label_finish">Toast</string>
    <string name="button_label_count">Count</string>
    <string name="toast_massage">Bilangan Fibonacci</string>
    <string name="button_label_toast">Set Limit</string>
    <string name="count_initial_value">1</string>
</resources>
```

# Membuat String Color
buat pada color.xml
membuat string agar dapat membuat color sesaui yg diinginkan
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#000000</color>
    <color name="white">#ffffff</color>
    <color name="colorPrimary">#FF0000</color>
    <color name="colorPrimaryDark">#8A2BE2</color>
</resources>
```

# Membuat JasaScript
buat pada MainActivity.java
Membuat JavaScript agar app bisa berfungsi
```
package com.app2toast;

import android.app.AlertDialog;
import android.content.DialogInterface;
import android.graphics.Color;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private TextView showCount;
    private int count = 1;
    private long fibNMinus1 = 1;
    private long fibNMinus2 = 1;
    private int limit = -1; // Inisialisasi limit dengan nilai default

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showCount = findViewById(R.id.show_count);
    }

    public void countUp(View view) {
        if (count == 0) {
            showCount.setText("0");
        } else if (count == 1) {
            showCount.setText("1");
        } else {
            if (limit != -1 && count > limit) {
                // Jika count melebihi limit, atur ulang perhitungan
                count = 0;
                fibNMinus1 = 1;
                fibNMinus2 = 0;
                showCount.setText(getString(R.string.count_initial_value));
            } else {
                long fibCurrent = fibNMinus1 + fibNMinus2;
                fibNMinus2 = fibNMinus1;
                fibNMinus1 = fibCurrent;

                // Mengubah warna teks menjadi warna RGB dengan warna yang berbeda setiap kali angka berubah
                int black = (int) (Math.random() * 256);
                int grey = (int) (Math.random() * 256);
                int gold = (int) (Math.random() * 256);
                showCount.setTextColor(Color.rgb(black, grey, gold));

                showCount.setText(String.valueOf(fibCurrent));
            }
        }

        count++;
    }

    public void back1(View view) {
        count = 1;
        fibNMinus1 = 1;
        fibNMinus2 = 0;
        showCount.setText(getString(R.string.count_initial_value));
    }

    public void setLimit(View view) {
        // Create and display a dialog to set the limit
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Set Limit");

        final EditText input = new EditText(this);
        input.setInputType(android.text.InputType.TYPE_CLASS_NUMBER);
        builder.setView(input);

        builder.setPositiveButton("OK", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                // Get the limit from the input and set it for calculations
                String limitStr = input.getText().toString();
                limit = Integer.parseInt(limitStr);
            }
        });

        builder.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                dialog.cancel();
            }
        });


        builder.show();
    }
}
```

# Membuat Background dengan Gambar
Unduh gambar, ganti nama dengan huruf kecil dan tanpa spasi, copy 

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/ffe356f4-7a49-4f84-b8ee-76214b399a48)

Paste pada **Drawable**

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/17248230-fd95-4ab0-89a7-3995c12394de)

Tambahkan ``` android:background="drawable/name``` pada activity.xml

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/c645b812-37ec-4adb-8efa-2921e97609fa)

# Build Project
Build Project, aktifkan mode developer pada device anda, aktifkan usb debug, sambungkan laptop/pc dengan device menggunakan usb, izinkan device ponsel untuk melakukan penginstalan usb, Run project 

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/143f7d62-21a9-4b60-95e4-cf46475ab6b5)

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/22bbc751-e68a-4fb2-b9ab-f1fd65431d6f)

![image](https://github.com/Luxcario/Project-Fibonacci/assets/116184002/b74dbd96-e98d-41a5-9f34-6172c5def48b)

# Hasil Run

https://github.com/Luxcario/Project-Fibonacci/assets/116184002/84efa86f-cc8d-4496-998c-116dcac48cc5



