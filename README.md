# ORDER-FLOW-ABSORPTION-LIVE-DDS
========================================================================
 ORDER FLOW ABSORPTION MONITOR [Delta Divergence Scalper]
 Panduan Penggunaan
========================================================================

--------------------------------------------------------------------
1. APA YANG DILAKUKAN INDIKATOR INI
--------------------------------------------------------------------
Indikator ini mendeteksi "Passive Absorption" — kondisi di mana harga
mencoba menembus level likuiditas penting (PDH/PDL atau Pivot High/Low)
disertai lonjakan volume delta yang kuat, tapi harga GAGAL melanjutkan
pergerakan tersebut (muncul sumbu panjang / rejection candle), dan
bar berikutnya menunjukkan delta melemah/berbalik.

Pola ini sering menandakan pihak besar sedang "menyerap" order lawan
di area tersebut sebelum harga berbalik arah.

Ada 2 jenis sinyal:
  • Lingkaran kuning kecil (⚪)  = "Warning" / kandidat absorption,
    baru terdeteksi, MASIH MENUNGGU konfirmasi bar berikutnya.
  • Segitiga hijau/merah + label "ABS" = Sinyal SUDAH TERKONFIRMASI
    pada bar yang closed (non-repainting, aman untuk dieksekusi).

--------------------------------------------------------------------
2. CARA MEMBACA DASHBOARD
--------------------------------------------------------------------
Dashboard terbagi 4 section (bisa di on/off satu-satu di Input > Dashboard):

  A. DELTA GAUGE (LIVE)
     - Gauge [SELL |███░░|░░░██| BUY] menunjukkan dominasi buy/sell
       volume secara real-time (update tiap tick).
     - "Delta / Rel. Vol" = nilai delta bar saat ini + status
       🟢 Normal / 🟡 Elevated / 🔴 SPIKE.

  B. ORDER FLOW CONTEXT
     - CVD Trend: apakah Cumulative Volume Delta sedang naik
       (Bullish/Accumulating) atau turun (Bearish/Distributing).
     - Volume Surge: volume bar sekarang vs rata-rata volume.
     - Absorption State: NORMAL / 🔥 BULL ABSORPTION / ⚡ BEAR
       ABSORPTION (artinya sedang menunggu bar konfirmasi).

  C. MARKET CONTEXT
     - Session aktif (London/New York/Asia/Off-Hours).
     - HTF Bias: arah tren timeframe lebih besar (EMA cepat vs lambat).
     - Liquidity Proximity: jarak (dalam pips) ke level terdekat
       (PDH/PDL/Pivot).
     - ADR Used: berapa persen range harian rata-rata yang sudah
       "terpakai" hari ini — makin tinggi %, makin besar kemungkinan
       pergerakan lanjutan mulai terbatas.

  D. TRADE DECISION
     - Action Status: NEUTRAL / READY BUY / READY SELL.
     - Entry, Stop Loss (harga + pips), TP1, TP2.
     - Risk $ dan Recommended Lot berdasarkan Account Size & Risk %
       yang kamu isi di input (murni bantuan hitung, bukan saran
       finansial — sesuaikan dengan broker/instrumen kamu).

--------------------------------------------------------------------
3. CARA MENGGUNAKAN SINYAL (ALUR KERJA)
--------------------------------------------------------------------
  1) Tunggu muncul lingkaran kuning (kandidat absorption) di area
     PDH/PDL/Pivot.
  2) Tunggu 1 bar berikutnya close — jika delta mengecil drastis atau
     berbalik arah, sinyal akan terkonfirmasi (segitiga + label ABS).
  3) Cek dashboard Section C (HTF Bias & Session) untuk konfirmasi
     tambahan sebelum entry — sebaiknya jangan melawan HTF Bias yang
     kuat.
  4) Gunakan Entry/SL/TP1/TP2 dari Section D sebagai acuan level.
  5) Aktifkan alert TradingView pada kondisi "Bullish/Bearish
     Absorption Triggered" agar tidak perlu memelototi chart.

--------------------------------------------------------------------
4. SARAN SETTING (STARTING POINT — SESUAIKAN DENGAN BACKTEST SENDIRI)
--------------------------------------------------------------------

--- A. SCALPING (M1 - M5, memegang posisi dalam hitungan menit) ---
  Timeframe chart              : M1 atau M5
  Lower TF utk agregasi delta  : 1 (centang "Use Lower Timeframe")
  Delta SMA Length             : 10-14 (lebih responsif)
  Relative Delta Spike Mult.   : 1.8 - 2.2
  Exhaustion Shrink Ratio      : 0.3 - 0.4 (harus cepat melemah)
  Wick/Body Ratio              : 1.2 - 1.5 (rejection candle lebih toleran)
  Max Distance ke Liquidity    : 2 - 4 pips
  Pivot Left/Right             : 3 / 3 (lebih sensitif)
  HTF Bias Timeframe           : 15 atau 30 menit
  SL Buffer                    : 1 - 2 pips
  TP1 / TP2 (R:R)              : 1:1.5 / 1:2.5
  Restrict to Killzone         : ON (London/NY overlap paling ideal)
  Risk % per Trade             : 0.25% - 0.5% (frekuensi entry tinggi)

--- B. DAY TRADING (M5 - M15, posisi ditutup di hari yang sama) ---
  Timeframe chart              : M5 atau M15
  Lower TF utk agregasi delta  : 1 atau 5
  Delta SMA Length             : 20 (default)
  Relative Delta Spike Mult.   : 2.0 - 2.5
  Exhaustion Shrink Ratio      : 0.4 - 0.5
  Wick/Body Ratio              : 1.5 - 2.0
  Max Distance ke Liquidity    : 4 - 7 pips
  Pivot Left/Right             : 5 / 5 (default)
  HTF Bias Timeframe           : 60 menit (H1)
  SL Buffer                    : 3 - 5 pips
  TP1 / TP2 (R:R)              : 1:2 / 1:3 (default)
  Restrict to Killzone         : Opsional (ON jika ingin lebih selektif)
  Risk % per Trade             : 0.5% - 1%

--- C. SWING TRADING (H1 - H4/D1, posisi dipegang berhari-hari) ---
  Timeframe chart              : H1 atau H4
  Lower TF utk agregasi delta  : 5 atau 15
  Delta SMA Length             : 20 - 30 (lebih smooth, kurangi noise)
  Relative Delta Spike Mult.   : 2.5 - 3.0 (butuh spike lebih ekstrem)
  Exhaustion Shrink Ratio      : 0.5 - 0.6 (lebih toleran)
  Wick/Body Ratio              : 2.0 - 2.5 (rejection candle harus jelas)
  Max Distance ke Liquidity    : 10 - 20 pips (skala relatif terhadap TF)
  Pivot Left/Right             : 8 - 10 / 8 - 10
  HTF Bias Timeframe           : Daily (D) atau Weekly (W)
  ADR Lookback                 : 14 - 20 hari
  SL Buffer                    : 10 - 20 pips (atau % dari ATR)
  TP1 / TP2 (R:R)              : 1:2 / 1:4 (biarkan profit berjalan)
  Restrict to Killzone         : OFF (swing tidak terlalu tergantung sesi)
  Risk % per Trade             : 0.5% - 1% (durasi lebih lama = risiko
                                  per trade sebaiknya tidak lebih besar)

--------------------------------------------------------------------
5. CATATAN PENTING
--------------------------------------------------------------------
  • Angka-angka di atas adalah TITIK AWAL, bukan patokan mutlak.
    Setiap pair/instrumen punya karakter volatilitas & likuiditas
    berbeda — selalu backtest/forward-test dulu sebelum live.
  • "Pip Size" di Input harus disesuaikan dengan instrumen (mis.
    0.0001 untuk mayor FX, 0.01 untuk pair JPY/indeks), atau centang
    "Use Symbol Tick Size" untuk aset non-forex (crypto/saham/indeks).
  • "Pip Value per Lot" di Risk Calculator adalah estimasi kasar —
    sesuaikan dengan spesifikasi kontrak/lot broker kamu agar
    perhitungan lot size akurat.
  • Delta yang dihitung adalah APROKSIMASI dari data volume candle
    (bukan data tape/order book asli), jadi anggap sebagai alat bantu
    konfirmasi, bukan sinyal berdiri sendiri — tetap gunakan
    manajemen risiko dan konfirmasi price action.
========================================================================
