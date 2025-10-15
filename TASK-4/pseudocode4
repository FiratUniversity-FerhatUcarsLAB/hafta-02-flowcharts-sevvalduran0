Başla

// 1. Öğrenci Girişi
ÖğrenciGirisi()
    kullanıcıAdi <- KullanıcıdanAl()
    sifre <- KullanıcıdanAl()
    eğer (kullanıcıAdi ve sifre doğruysa) 
        GirişBaşarılı()
    değilse
        GirişHatasıMesajı()
        TekrarDeneme()

// 2. Ders Listesini Göster
DersListesi <- DersleriGetir()
DersListesiniGoster(DersListesi)

// 3. Ders Seçimi ve Kontroller
SeçilenDersler <- BoşListe
ToplamKredi <- 0
KrediLimiti <- ÖğrencininKrediLimitiGetir()

while (DersSeçmekİstiyorMu())
    DersID <- KullanıcıdanDersIDAl()
    seçilenDers <- DersListesindenBul(DersID)
    
    // Ön Koşul Kontrolü
    eğer (ÖnKoşulKontrol(seçilenDers, Öğrenci) == FALSE)
        HataMesajı("Ön koşul sağlanmamış.")
        devamEt
    
    // Zaman Çakışması Kontrolü
    eğer (ZamanÇakışmasıVarMi(seçilenDers, SeçilenDersler) == TRUE)
        HataMesajı("Ders zamanları çakışıyor.")
        devamEt
    
    // Kredi Limiti Kontrolü
    eğer (ToplamKredi + seçilenDers.Kredi > KrediLimiti)
        HataMesajı("Kredi limitini aşıyorsunuz.")
        devamEt
    
    // Ders eklenebilir
    SeçilenDersler.Ekle(seçilenDers)
    ToplamKredi <- ToplamKredi + seçilenDers.Kredi
    BilgiMesajı("Ders başarıyla eklendi.")

// 4. Kayıt Onayı
eğer (SeçilenDersler boş değilse)
    OnaySor("Seçilen dersleri kaydetmek istiyor musunuz?")
    eğer (kullanıcı Onay verirse)
        KayıtlarıKaydet(Öğrenci, SeçilenDersler)
        BilgiMesajı("Dersler başarıyla kaydedildi.")
    değilse
        BilgiMesajı("Kayıt işlemi iptal edildi.")
değilse
    BilgiMesajı("Seçilen ders yok.")

// 5. Çıkış
ÇıkışYap()

Bitir
