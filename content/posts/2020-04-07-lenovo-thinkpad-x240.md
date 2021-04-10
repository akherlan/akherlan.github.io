---
title: "Lenovo ThinkPad X240 & Xubuntu"
date: '2020-04-07'
---

{{< figure src="https://telegra.ph/file/800992a81592fc3081224.png" caption="Logo Lenovo Thinkpad" alt="Lenovo ThinkPad" >}}

Pekan lalu saya memesan mesin baru, Lenovo ThinkPad X240. _Secondhand_. Harganya lumayan miring juga dengan spesifikasi nggak jelek-jelek amat:

- Model prosesor Intel® Core™ i5-4300U CPU @ 1.90GHz (artinya multi CPU generasi 4)
- Arsitektur prosesor `x86_64` (artinya dari Intel)
- Memori HDD SATA 500GB (versi lain ada yang pakai SSD)
- Memori RAM 4GB (sebetulnya saya mau pesan yang 8GB)
- VGA Intel Haswell-ULT Integrated Graphics Controller
- Adaptor WiFi
- Adaptor Bluetooth
- Ukuran layar `361x203 mm` (12 inci) dengan resolusi sampai `1366x768 pixel`
- Beratnya nggak tau pasti karena belum ditimbang, tapi termasuk ringan dibanding laptop lama
- Port-nya banyak dan lengkap sampai ada yang saya belum tau fungsinya.

## Kondisi fisik

Kondisinya secara fisik masih bagus. Cuma engsel kanan yang bunyi _krek-krek_ saat dibuka-tutup. Juga baterainya agak sedikit longgar/goyang. Tapi jarang ada kelihatan lecet.

{{< figure src="https://telegra.ph/file/9f4175b0997d39cd40df3.png" caption="Fisik bagian atas" alt="Lenovo ThinkPad" >}}

## Kelebihan

- Baterainya ada dua, yang tertanam dengan yang bisa dilepas dari luar. Jadi bisa tahan lama saat dibawa bepergian. Sehari-semalam dipakai biasanya cuma saya isi daya 1x.
- _Gesture allowed_ pada TrackPad, ketika dicoba di Windows 10 (OS bawaan toko) dan Xubuntu 18.04, tidak ada bedanya, sama-sama yahood!
- TrackPoint, entah ini kelebihan atau bukan karena sebenarnya jarang saya pakai, ini juga berfungsi dengan baik di Xubuntu 18.04.

{{< figure src="https://akherlan.github.io/blog/post/2020-04-07-lenovo-thinkpad-x240_files/trackpoint.jpg" caption="TrackPoint" alt="Lenovo ThinkPad" >}}

{{< figure src="https://telegra.ph/file/bc98d92c8370d20dcb6dd.png" caption="Baterai ganda" alt="Lenovo ThinkPad" >}}

## Kebiasaan

Saya agak _kagok_ dengan papan ketiknya karena belum terbiasa. Bukan ketika mengetik huruf dan angka, tapi ketika menggunakan tombol-tombol seperti:

- `Ctrl` kiri, karena letaknya di posisi kedua dari pojok kiri bawah. Biasanya di laptop lama letak tombol `Ctrl` kiri berada di paling pojok kiri. Jadi sangat mudah ditemukan pakai kelingking kiri. Sekarang saya harus biasakan pakai jari manis.
- `Shift` kiri, lagi-lagi kiri. ThinkPad X240 punya `Shift` kiri yang sangat pendek karena ada tombol karakter tambahan di sebelahnya, antara `Shift` dan `Z`, yaitu tombol `<` / `>` (`Shft + <`). Ddefault keyboard US. Padahal pada tombol ini tertulis `\` atau `|` (default mana ini?).
- Sebaliknya, `Shift` kanan sangat panjang. Mungkin saya harus mulai biasakan diri pakai `Shift` kanan saja.
- `Home` jadi di atas dekat `delete`, bukan di tepi bawah sekitar arrow.
- Apalagi `End`, menggunakannya jadi agak susah karena gabung dengan `Insert` (menekan `End` harus dengan `Fn + Insert`).
- `Enter` (`return`) yang sedikit berbeda bentuknya, walaupun tetap masih lebar, tapi ramping.
- Dan tombol lain yang tertulis berbeda antara teks di stiker dengan yang muncul setelah ditekan (default US). Saya kurang tahu ini stiker default negara mana.
  - `@` tertulis `"` pada tombol numerik `2 + Shift`
  - `#` tertulis `£` pada tombol numerik `3 + Shift`
  - `"` tertulis `@` pata tombol `' + Shift`, sekitar `Enter`

| Tekan 	|  +Shft 	| Muncul 	|  +Shft 	|             Letak             	|
|:------:	|:------:	|:------:	|:------:	|:------------------------------:	|
|    \   	|   \|   	|    <   	|    >   	|    di antara `Shift` dan `Z`   	|
|    ~   	|    #   	|    \   	|   \|   	| di samping `Enter` (`Return`) 	|
|        	|        	|        	|        	|                               	|

{{< figure src="https://telegra.ph/file/7625018745418685863ca.png" caption="Tombol Fn dengan LED, dekat Ctrl" alt="Lenovo ThinkPad" >}}

Selain itu malah jadi sangat nyaman:

- `PgUp` dan `PgDn` yang dekat dengan arrow, memudahkan saat membaca dan skrol halaman.
{{< figure src="https://telegra.ph/file/447e608ed95f5b2060bce.png" caption="Arrow, PgUp, PgDn" alt="Lenovo ThinkPad" >}}
- `Alt` kanan, `PrtSc`, dan `Ctrl` kanan yang berdekatan sehingga mudah untuk ambil tangkapan layar. Saya terbiasa dengan `shortcut` kombinasi tombol-tombol ini.
{{< figure src="https://telegra.ph/file/87b65ae01a70162541733.png" caption="Tombol-tombol shortcut tangkapan layar" alt="Lenovo ThinkPad" >}}

## Informasi Hardware

### Prosesor

```bash
$ lscpu
```

```
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  2
Core(s) per socket:  2
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               69
Model name:          Intel(R) Core(TM) i5-4300U CPU @ 1.90GHz
Stepping:            1
CPU MHz:             936.269
CPU max MHz:         2900,0000
CPU min MHz:         800,0000
BogoMIPS:            4988.62
Virtualization:      VT-x
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            3072K
NUMA node0 CPU(s):   0-3
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid xsaveopt dtherm ida arat pln pts md_clear flush_l1d
```

### Monitor & audio

```bash
$ xdpyinfo | grep "dimensions:"
```

```
dimensions:    1366x768 pixels (361x203 millimeters)
```

```bash
$ lspci -v | grep "VGA" -A 12
```

```
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b) (prog-if 00 [VGA controller])
	Subsystem: Lenovo ThinkPad X240
	Flags: bus master, fast devsel, latency 0, IRQ 48
	Memory at f0000000 (64-bit, non-prefetchable) [size=4M]
	Memory at e0000000 (64-bit, prefetchable) [size=256M]
	I/O ports at 3000 [size=64]
	[virtual] Expansion ROM at 000c0000 [disabled] [size=128K]
	Capabilities: <access denied>
	Kernel driver in use: i915
	Kernel modules: i915

00:03.0 Audio device: Intel Corporation Haswell-ULT HD Audio Controller (rev 0b)
	Subsystem: Lenovo ThinkPad X240
```

Perangkat lainnya...

```bash
$ lspci
```

```
00:00.0 Host bridge: Intel Corporation Haswell-ULT DRAM Controller (rev 0b)
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)
00:03.0 Audio device: Intel Corporation Haswell-ULT HD Audio Controller (rev 0b)
00:14.0 USB controller: Intel Corporation 8 Series USB xHCI HC (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series HECI #0 (rev 04)
00:16.3 Serial controller: Intel Corporation 8 Series HECI KT (rev 04)
00:19.0 Ethernet controller: Intel Corporation Ethernet Connection I218-LM (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series HD Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 6 (rev e4)
00:1c.1 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 3 (rev e4)
00:1d.0 USB controller: Intel Corporation 8 Series USB EHCI #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation 8 Series LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series SMBus Controller (rev 04)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)
03:00.0 Network controller: Intel Corporation Wireless 7260 (rev 83)
```

## Sistem operasi

Meskipun tertulis di _casing_ bahwa mesin laptop Lenovo ini dilengkapi dengan Windows 7 sebagai sistem operasi original, tetapi penjual mendistribusikan mesin second ini dengan sistem operasi Windows 10.

{{< figure src="https://telegra.ph/file/d264bf026a0f9265f6ce2.png" caption="Casing dengan logo sistem operasi bawaan Windows7" alt="Lenovo ThinkPad" >}}

Tetap saja. Satu hari setelah cek keadaan *hardware* sebisanya, untuk memastikan kondisi benar-benar baik dan tidak cacat, saya langsung instal sistem operasi [Xubuntu 18.04](https://xubuntu.org/).

Yaa... Begitulah...
