İsim - Soy isim ŞEVVAL DURAN
Öğrenci No:240541088

sistemin kısa açıklaması (maks. 5-6 satır)
BAŞLAT

Öğrenci = GirişYap(öğrenciNumarası, şifre)

EĞER Öğrenci.GirişBaşarılı MI?
    DERS_LİSTESİ = DersleriYükle(Öğrenci.Bölüm, Öğrenci.Sınıf)
    ALINAN_DERSLER = []

    YAZDIR "Kayıtlı olduğunuz bölüm: " + Öğrenci.Bölüm
    YAZDIR "Açılan dersler:"

    DÖNGÜ her DERS içinde DERS_LİSTESİ
        YAZDIR DERS.Kodu + " - " + DERS.Adı + " (" + DERS.Kredi + " kredi)"

    MAKS_KREDİ = Öğrenci.SınıfBazlıKrediHakkı

    KREDİ_TOPLAMI = 0

    TEKRAR
        DERS = KullanıcıdanDersSeç()

        EĞER DERS zaten ALINAN_DERSLER içinde mi?
            YAZDIR "Bu dersi zaten seçtiniz."
        DEĞİLSE
            EĞER KREDİ_TOPLAMI + DERS.Kredi <= MAKS_KREDİ
                ALINAN_DERSLER'e DERS ekle
                KREDİ_TOPLAMI = KREDİ_TOPLAMI + DERS.Kredi
                YAZDIR DERS.Adı + " dersi eklendi. Toplam kredi: " + KREDİ_TOPLAMI
            DEĞİLSE
                YAZDIR "Kredi sınırını aşıyorsunuz. Bu dersi alamazsınız."

        DEVAM_ET = KullanıcıyaSor("Ders eklemeye devam etmek istiyor musunuz? (E/H)")
    SONRAKİNE KADAR DEVAM_ET == 'H'

    YAZDIR "Seçilen dersler:"
    DÖNGÜ DERS içinde ALINAN_DERSLER
        YAZDIR DERS.Kodu + " - " + DERS.Adı

    ONAY = KullanıcıyaSor("Kayıt işlemini onaylıyor musunuz? (E/H)")

    EĞER ONAY == 'E'
        KayıtlarıKaydet(Öğrenci.ID, ALINAN_DERSLER)
        YAZDIR "Ders kayıt işlemi başarıyla tamamlandı."
    DEĞİLSE
        YAZDIR "Kayıt işlemi iptal edildi."

DEĞİLSE
    YAZDIR "Giriş başarısız. Lütfen kullanıcı bilgilerinizi kontrol edin."

BİTİR
