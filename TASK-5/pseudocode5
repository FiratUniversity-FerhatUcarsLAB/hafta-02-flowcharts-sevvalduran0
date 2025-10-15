Başla

// Sistem Başlatma
Initialize System
  Initialize Sensors (DoorSensor, WindowSensor, MotionSensor)
  Initialize Alarm
  Initialize NotificationService (SMS, AppPush)
  Set SystemStatus = "Disarmed"

// Kullanıcıdan sistem durumu alma
Fonksiyon GetUserCommand()
  Komut = Kullanıcıdan giriş al ("arm", "disarm", "status")
  Döndür Komut

// Sensör kontrolü
Fonksiyon CheckSensors()
  Eğer DoorSensor aktif ise
    Döndür "DoorBreached"
  Eğer WindowSensor aktif ise
    Döndür "WindowBreached"
  Eğer MotionSensor aktif ise
    Döndür "MotionDetected"
  Döndür "NoThreat"

// Alarm çalma
Fonksiyon TriggerAlarm()
  Alarm çalıştır
  Gönder Bildirim ("Alarm triggered! Güvenlik ihlali tespit edildi.")

// Bildirim gönderme
Fonksiyon SendNotification(message)
  NotificationService gönder (message)

// Ana döngü
While True
  Komut = GetUserCommand()
  
  Eğer Komut == "arm" ise
    SystemStatus = "Armed"
    SendNotification("Sistem aktif hale getirildi.")
  
  Değilse eğer Komut == "disarm" ise
    SystemStatus = "Disarmed"
    SendNotification("Sistem pasif hale getirildi.")
  
  Değilse eğer Komut == "status" ise
    SendNotification("Sistem durumu: " + SystemStatus)
  
  Eğer SystemStatus == "Armed" ise
    Tehdit = CheckSensors()
    Eğer Tehdit != "NoThreat" ise
      TriggerAlarm()
  
  // Küçük bir gecikme ekle, örneğin 1 saniye
  Wait(1 saniye)

Bitir
