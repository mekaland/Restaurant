# 🧆 Lezzet Durağı Restoranı WhatsApp Rezervasyon Asistanı (n8n Workflow)

Bu proje, **n8n** üzerinde kurulu bir **WhatsApp Rezervasyon Asistanı** sistemidir.  
Kullanıcılar WhatsApp üzerinden mesaj attıklarında, yapay zeka destekli bir asistan tarafından yönlendirilerek **rezervasyon yapabilir**, **menüyü öğrenebilir**, ve bilgileri **Google Calendar** ve **Google Sheets** üzerine kaydedilir.

---

## 🔧 Kullanılan Araçlar ve Servisler

| Bileşen                 | Açıklama                                                                 |
|-------------------------|--------------------------------------------------------------------------|
| n8n                     | Otomasyon altyapısı                                                      |
| WhatsApp Trigger        | Gelen mesajları dinler (Meta API üzerinden)                              |
| AI Agent                | Yapay zeka destekli doğal konuşma üretimi                               |
| Google Gemini API       | Gemini 2.5 Flash modeli ile AI Agent’ı destekler                        |
| Google Calendar         | Rezervasyonları takvime işler                                            |
| Google Sheets           | Ad, telefon, tarih ve saat bilgilerini tabloya kaydeder                  |
| Memory Node             | Kısa süreli konuşma geçmişi sağlar (AI Agent'a bağlanır)                |
| Ngrok                   | Lokal n8n’i dış dünyaya açar, WhatsApp Webhook’u ile haberleşmeyi sağlar|

---

## 📲 Kullanıcı Akışı

1. Müşteri WhatsApp’tan mesaj gönderir (örn. “Bu akşam 2 kişilik masa var mı?”).
2. **WhatsApp Trigger** tetiklenir ve mesaj **AI Agent**’a iletilir.
3. **AI Agent**, Google Gemini modeliyle doğal ve adım adım bir cevap üretir.
4. Eğer rezervasyon bilgisi tamamlanırsa:
   - **Takvimle** node’u, Google Calendar’a rezervasyonu kaydeder.
   - **Sheets** node’u, bilgileri (isim, telefon, tarih, saat) Google Sheets’e yazar.
5. **Send Message** node’u, AI Agent’ın cevabını tekrar WhatsApp üzerinden kullanıcıya gönderir.

---

## 📁 Node Açıklamaları

| Node Adı           | İşlevi                                                                 |
|--------------------|------------------------------------------------------------------------|
| WhatsApp Trigger   | Kullanıcıdan gelen mesajı dinler, süreci başlatır                     |
| AI Agent           | Mesajları anlayıp uygun adımlarla cevap oluşturur                     |
| Google Gemini      | LLM desteği sağlayarak doğal dil üretimi sağlar                        |
| Simple Memory      | Önceki mesajları kısa süreli hafızada tutar                            |
| RandevuAl          | Takvimdeki uygun saatleri kontrol eder (Kullanıcıya gösterilmez)       |
| Takvimle           | Rezervasyon bilgisini Google Calendar'a işler                          |
| Sheets             | İsim, telefon, tarih ve saat bilgilerini Google Sheets'e kaydeder      |
| Code               | AI cevabını alır, düzenler                                              |
| Send message       | AI cevabını tekrar WhatsApp’a iletir                                   |

---

## 🧠 AI Agent Prompt

AI Agent aşağıdaki kurallara göre eğitilmiştir:

- Kendini asistan veya yapay zeka olarak tanıtma.
- Kullanıcıyla sade, doğal, profesyonel ama samimi bir dille sohbet et.
- Her adımda tek bir bilgi iste (önce saat, sonra kişi sayısı, sonra isim vb.).
- Randevu netleşince şu alanları döndür: `Start`, `End`, `output` (Bu bilgiler kullanıcıya gösterilmez, sadece takvim ve sheets için kullanılır).

---

## 🍽️ Menü (Kişi Başı Ortalama)

- Izgara Köfte – 280₺  
- Tavuk Şiş – 260₺  
- Karışık Kebap – 380₺  
- Fırın Lazanya – 300₺  
- Mevsim Salata – 120₺  
- Çorba – 90₺  
- Tatlı (Künefe / Sufle) – 130₺  
- Meşrubat – 50₺  

---

## 🗓️ Adres ve Rezervasyon Saatleri

- **Adres:** Ahmet Taner Kışlalı Cad. No:34, Nilüfer / BURSA  
- **Saatler:** Hafta içi ve cumartesi 12:00 – 22:00  
- **Pazar günü kapalıdır**

---

## 🛠️ Kurulum Gereksinimleri

- n8n (v1.100.1 veya üstü)
- WhatsApp Business API bağlantısı
- Google Sheets ve Google Calendar API erişimi
- Ngrok veya dış IP erişimi
- Google Gemini / PaLM API

---

Hazırsan rezervasyonları almaya başlayabilirsin! 🍽️📲  
