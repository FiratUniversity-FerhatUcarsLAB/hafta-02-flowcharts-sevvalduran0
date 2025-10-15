PROGRAM HastaneRandevuTahlilSistemi

    BAŞLAT
        GİRİŞ_EKRANI()
    BİTİR

FONKSİYON GİRİŞ_EKRANI()
    YAZDIR "1 - Giriş Yap"
    YAZDIR "2 - Kayıt Ol"
    YAZDIR "3 - Çıkış"
    SEÇİM ← GİRİŞ("Seçiminizi yapınız: ")

    EĞER SEÇİM = 1 İSE
        GİRİŞ_YAP()
    DEĞİLSE EĞER SEÇİM = 2 İSE
        KAYIT_OL()
    DEĞİLSE
        ÇIKIŞ()

FONKSİYON KAYIT_OL()
    AD ← GİRİŞ("Ad: ")
    TC ← GİRİŞ("TC: ")
    ŞİFRE ← GİRİŞ("Şifre: ")
    VERİTABANI.kullanıcılar → EKLE({ad: AD, tc: TC, şifre: ŞİFRE, rol: "hasta"})
    YAZDIR "Kayıt başarılı!"
    GİRİŞ_EKRANI()

FONKSİYON GİRİŞ_YAP()
    TC ← GİRİŞ("TC: ")
    ŞİFRE ← GİRİŞ("Şifre: ")
    kullanıcı ← VERİTABANI.kullanıcılar[TC]

    EĞER kullanıcı DOĞRU ve kullanıcı.şifre = ŞİFRE İSE
        EĞER kullanıcı.rol = "hasta" İSE
            HASTA_PANELİ(kullanıcı)
        DEĞİLSE EĞER kullanıcı.rol = "doktor" İSE
            DOKTOR_PANELİ(kullanıcı)
        DEĞİLSE EĞER kullanıcı.rol = "admin" İSE
            ADMIN_PANELİ(kullanıcı)
    DEĞİLSE
        YAZDIR "Hatalı giriş!"
        GİRİŞ_EKRANI()

FONKSİYON HASTA_PANELİ(hasta)
    TEKRARLA
        YAZDIR "1 - Randevu Al"
        YAZDIR "2 - Randevularımı Gör"
        YAZDIR "3 - Tahlil Talep Et"
        YAZDIR "4 - Tahlil Sonuçlarını Gör"
        YAZDIR "5 - Ana Menüye Dön"
        SEÇİM ← GİRİŞ()

        EĞER SEÇİM = 1 İSE
            RANDEVU_AL(hasta)
        EĞER SEÇİM = 2 İSE
            RANDEVULARI_GÖR(hasta)
        EĞER SEÇİM = 3 İSE
            TAHLIL_TALEP_ET(hasta)
        EĞER SEÇİM = 4 İSE
            TAHLIL_SONUÇLARINI_GÖR(hasta)
        EĞER SEÇİM = 5 İSE
            ÇIKIŞ_DÖN()

FONKSİYON RANDEVU_AL(hasta)
    BRANŞLAR ← VERİTABANI.branşlar
    BRANŞ ← GİRİŞ("Branş seçin: ")
    DOKTORLAR ← DOKTORLARI_GETİR(BRANŞ)
    DOKTOR ← GİRİŞ("Doktor TC: ")
    TARİH ← GİRİŞ("Randevu Tarihi: ")
    RANDEVU ← {hasta_tc: hasta.tc, doktor_tc: DOKTOR, tarih: TARİH, durum: "Bekliyor"}
    VERİTABANI.randevular → EKLE(RANDEVU)
    YAZDIR "Randevu oluşturuldu."

FONKSİYON RANDEVULARI_GÖR(hasta)
    RANDEVULAR ← VERİTABANI.randevular FİLTRELE(hasta_tc = hasta.tc)
    YAZDIR RANDEVULAR

FONKSİYON TAHLIL_TALEP_ET(hasta)
    RANDEVU_ID ← GİRİŞ("Tahlil istenen randevu ID: ")
    TAHLIL ← {randevu_id: RANDEVU_ID, hasta_tc: hasta.tc, sonuc: "Bekleniyor"}
    VERİTABANI.tahliller → EKLE(TAHLIL)
    YAZDIR "Tahlil talebi gönderildi."

FONKSİYON TAHLIL_SONUÇLARINI_GÖR(hasta)
    TAHLILLER ← VERİTABANI.tahliller FİLTRELE(hasta_tc = hasta.tc)
    YAZDIR TAHLILLER

FONKSİYON DOKTOR_PANELİ(doktor)
    TEKRARLA
        YAZDIR "1 - Randevularımı Gör"
        YAZDIR "2 - Tahlil Sonucu Gir"
        YAZDIR "3 - Ana Menüye Dön"
        SEÇİM ← GİRİŞ()

        EĞER SEÇİM = 1 İSE
            DOKTOR_RANDEVULARINI_GÖR(doktor)
        EĞER SEÇİM = 2 İSE
            TAHLIL_SONUCU_GİR(doktor)
        EĞER SEÇİM = 3 İSE
            ÇIKIŞ_DÖN()

FONKSİYON DOKTOR_RANDEVULARINI_GÖR(doktor)
    RANDEVULAR ← VERİTABANI.randevular FİLTRELE(doktor_tc = doktor.tc)
    YAZDIR RANDEVULAR

FONKSİYON TAHLIL_SONUCU_GİR(doktor)
    TAHLILLER ← VERİTABANI.tahliller FİLTRELE(doktor_tc = doktor.tc AND sonuc = "Bekleniyor")
    YAZDIR TAHLILLER
    TAHLIL_ID ← GİRİŞ("Tahlil ID: ")
    SONUC ← GİRİŞ("Sonuç: ")
    VERİTABANI.tahliller[TAHLIL_ID].sonuc ← SONUC
    YAZDIR "Sonuç başarıyla girildi."

FONKSİYON ADMIN_PANELİ(admin)
    TEKRARLA
        YAZDIR "1 - Doktor Ekle"
        YAZDIR "2 - Branş Ekle"
        YAZDIR "3 - Kullanıcıları Listele"
        YAZDIR "4 - Ana Menüye Dön"
        SEÇİM ← GİRİŞ()

        EĞER SEÇİM = 1 İSE
            DOKTOR_EKLE()
        EĞER SEÇİM = 2 İSE
            BRANŞ_EKLE()
        EĞER SEÇİM = 3 İSE
            KULLANICILARI_LİSTELE()
        EĞER SEÇİM = 4 İSE
            ÇIKIŞ_DÖN()

FONKSİYON DOKTOR_EKLE()
    AD ← GİRİŞ("Ad: ")
    TC ← GİRİŞ("TC: ")
    BRANŞ ← GİRİŞ("Branş: ")
    ŞİFRE ← GİRİŞ("Şifre: ")
    VERİTABANI.kullanıcılar → EKLE({ad: AD, tc: TC, şifre: ŞİFRE, rol: "doktor", branş: BRANŞ})
    YAZDIR "Doktor eklendi."

FONKSİYON BRANŞ_EKLE()
    BRANŞ_ADI ← GİRİŞ("Yeni Branş Adı: ")
    VERİTABANI.branşlar → EKLE(BRANŞ_ADI)
    YAZDIR "Branş eklendi."

FONKSİYON KULLANICILARI_LİSTELE()
    YAZDIR VERİTABANI.kullanıcılar

FONKSİYON ÇIKIŞ_DÖN()
    GİRİŞ_EKRANI()
