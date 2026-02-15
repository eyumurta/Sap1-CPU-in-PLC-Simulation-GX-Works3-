🇺🇸 English | 🇹🇷 Türkçe

[English Version](README_EN.md)
[Turkish Version](README_TR.md)

# Sap1-CPU-in-PLC-Simulation-GX-Works3

PLC üzerinde SAP1 CPU simülasyonu

<img width="467" height="562" alt="Ekran görüntüsü 2026-02-14 143216" src="https://github.com/user-attachments/assets/392da0bf-5a58-47f6-9c65-1b377633b1b4" />

SAP1 eğitim amaçlı tasarlanmış,basit bir CPU öreğidir. PLC (Mitsubishi Electrix GXWorks3) üzerinde bir simülasyon oluşturdum. SAP1 CPU’nun temel mimarisini görselde görebilirsiniz.

<img width="2278" height="374" alt="Ekran görüntüsü 2026-02-14 143110" src="https://github.com/user-attachments/assets/636d57b0-857a-4a2c-a3ca-4006940dcf69" /> <img width="2205" height="1034" alt="Ekran görüntüsü 2026-02-14 143121" src="https://github.com/user-attachments/assets/8cc69e92-0812-4e54-9e13-43ca9928ee5b" />

CPU komutları 6 T state'de işlenir. İlk 3 T state tüm komutlar için ortaktır.

## SAP1 Register’ları
##### Program Counter:

Bellekteki program adresini gösterir.
Cp girişi aktif olduğunda sayaç artar.
Ep girişi aktif olduğunda PC değeri WBus üzerine yüklenir.

##### Input ve MAR:

Bu register RAM’de hangi adrese erişileceğini belirtir.
Lm sinyali aktif olduğunda WBus değeri MAR register’ına yüklenir.

##### RAM:

RAM kullanıcı programını ve verileri saklar.
RAM 16 hücreye sahiptir, her hücre 8 bit uzunluğundadır.
Ce sinyali düşük olduğunda RAM değeri WBus üzerine yüklenir.

##### Instruction Register:

Instruction Register komut kodunu ve adres değerini çözümler.
4 bit MSB komutu , 4 bit LSB adresi temsil eder.
Ei sinyali düşük olduğunda WBus değeri IR register’ına yüklenir.
Li sinyali aktif olduğunda decode edilen adres değeri WBus üzerine yüklenir.
Hazırladığım simülasyonda IR değeri her zaman kontrol matrisine yüklenir.

##### Accumulator:

Bu register LDA komutu tarafından kullanılır.
Aynı zamanda toplama ve çıkarma sonuçları burada saklanır.
LA sinyali aktif olduğunda WBus değeri Accumulator register’ına yüklenir.
EA sinyali aktif olduğunda Accumulator değeri WBus üzerine yüklenir.

##### Adder/Subtractor:

Bu birimin CPU’nun ALU (Arithmetic Logic Unit) parçasıdır.
Eu sinyali aktif olduğunda toplama/çıkarma sonucu WBus üzerine yüklenir.
Su sinyali pasif olduğunda toplama modunda çalışır.
Su sinyali aktif olduğunda çıkarma modunda çalışır.

##### B Register:

B register, ADD ve SUB komutları için bir buffer register’dır.
LB sinyali aktif olduğunda WBus değeri B register’ına yüklenir.

##### Output Register:

Bu register OUT komutu tarafından kullanılır.
Lo sinyali aktif olduğunda WBus değeri Output register’ına yüklenir.

## T-Durumları
##### T1 Durumu:

Program Counter değerini MAR register’ına yükler (MAR RAM adresini seçer).

##### T2 Durumu:

Bir sonraki komut için Program Counter artırılır.

##### T3 Durumu:

İşaret edilen RAM değeri Instruction Register’a yüklenir (Instruction Register komutu ve adresi çözümler).

##### T4 Durumu (LDA, ADD, SUB için ortaktır):

Decode edilen komut kontrol matrisine yüklenir.
Decode edilen adres MAR’a yüklenir (RAM işaret edilen adrese gider).

<img width="1889" height="605" alt="Ekran görüntüsü 2026-02-14 143237" src="https://github.com/user-attachments/assets/235c5631-13e6-402c-85ea-6e0111baaaa0" />

## Komutlar
##### LDA Komutu:

Bu komut değeri Accumulator register’ına yükler.
T5 Durumu: İşaret edilen RAM adresini Accumulator register’ına yükler.

<img width="1911" height="622" alt="Ekran görüntüsü 2026-02-14 143246" src="https://github.com/user-attachments/assets/42bfd495-6391-4ed8-b501-e280698dbd4c" />
##### ADD Komutu:

Bu komut değeri B register’ına yükler. Daha sonra Adder (A+B) işlemini hesaplar. Hesaplanan değer Accumulator register’ında saklanır.
T5 Durumu: İşaret edilen RAM adresini B register’ına yükler.

##### SUB Komutu:

Bu komut değeri B register’ına yükler. Daha sonra (A-B) işlemini hesaplar. Hesaplanan değer Accumulator register’ında saklanır.
T5 Durumu: İşaret edilen RAM adresini B register’ına yükler.

<img width="2156" height="1199" alt="Ekran görüntüsü 2026-02-15 102730" src="https://github.com/user-attachments/assets/4fae1b53-3e05-4140-a843-ee4748f59029" />
##### OUT Komutu:

Bu komut Accumulator değerini Output register’ına yükler.

<img width="536" height="481" alt="Ekran görüntüsü 2026-02-14 145642" src="https://github.com/user-attachments/assets/1631f86c-0200-4f34-b2ff-a0717b25c4fa" />

##### HLT Komutu:

Bu komut CPU clock’unu durdurur.

Her T durumunda farklı kontrol sinyalleri vardır: Simüle edilen programdaki CASE yapısını kontrol edebilirsiniz.

##### SAP1 CPU hakkında daha fazla detay:
Digital Computer Electronics – Third Edition – Albert Paul Malvino, Jerald A. Brown / Sayfa 140
