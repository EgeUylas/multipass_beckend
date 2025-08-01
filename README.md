# Multipass VM Yönetimi & AI Proxy API

Bu proje, Multipass sanal makinelerini (VM) yönetmek ve Ollama tabanlı bir yapay zeka (AI) ile etkileşim kurmak için geliştirilmiş birleşik bir FastAPI tabanlı API sunucusudur. API, hem standart VM yönetim işlemlerini (oluşturma, başlatma, durdurma, silme) hem de AI destekli komut yürütme özelliklerini destekler.

## Özellikler

- **VM Yönetimi:** Multipass VM'lerini listeleme, oluşturma, başlatma, durdurma ve silme.
- **Asenkron İşlemler:** Uzun süren VM oluşturma işlemleri için arka planda asenkron görev desteği.
- **AI Entegrasyonu:** Kullanıcıdan gelen doğal dil girdilerini işleyerek Multipass komutları üreten ve yürüten Ollama entegrasyonu.
- **Sağlık Kontrolü:** API'nin ve bağımlı servislerin (Multipass, Ollama) durumunu kontrol eden endpoint'ler.
- **Yapılandırılabilirlik:** `.env` dosyası üzerinden kolayca yapılandırılabilir sunucu portu, Multipass yolu ve Ollama API adresi.

## Gereksinimler

- [Python 3.8+](https://www.python.org/downloads/)
- [Multipass](https://multipass.run/install)
- [Ollama](https://ollama.com/) (AI özelliklerini kullanmak için gereklidir ve bir modelin çalışıyor olması gerekir, örn: `ollama run llama3`)

## Kurulum

1.  **Projeyi Klonlayın:**

    ```bash
    git clone <repository-url>
    cd BACKEND
    ```

2.  **Sanal Ortam Oluşturun ve Aktive Edin:**

    ```bash
    # Windows
    python -m venv venv
    venv\Scripts\activate
    
    # macOS / Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Bağımlılıkları Yükleyin:**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Ortam Değişkenlerini Yapılandırın:**

    `.env.example` dosyasını kopyalayarak `.env` adında yeni bir dosya oluşturun:

    ```bash
    # Windows
    copy .env.example .env
    
    # macOS / Linux
    cp .env.example .env
    ```

    Oluşturduğunuz `.env` dosyasını kendi sisteminize göre düzenleyin. Özellikle `MULTIPASS_BIN` yolunun doğru olduğundan emin olun.

## Uygulamayı Çalıştırma

Sunucuyu başlatmak için aşağıdaki komutu kullanabilirsiniz:

```bash
uvicorn api_server:app --reload --port 8001
```

Alternatif olarak, doğrudan Python ile de çalıştırabilirsiniz:

```bash
python api_server.py
```

Sunucu varsayılan olarak `http://127.0.0.1:8001` adresinde çalışmaya başlayacaktır.

## API Endpoint'leri

API'nin interaktif dokümantasyonuna (Swagger UI) sunucu çalışırken [http://127.0.0.1:8001/docs](http://127.0.0.1:8001/docs) adresinden ulaşabilirsiniz.

### Başlıca Endpoint'ler

- `GET /`: API'nin çalıştığını doğrular.
- `GET /health`: API ve bağımlılıkların (Multipass, Ollama) sağlık durumunu kontrol eder.
- `GET /vms/list`: Tüm Multipass VM'lerini listeler.
- `POST /vms/create-async`: Asenkron olarak yeni bir VM oluşturur.
- `POST /chat`: AI ile sohbet ederek komutların (örn: "create a new vm named test-vm") çalıştırılmasını sağlar.

