# Python-Programlama-Ansiklopedisi
.NET 8 ve Avalonia UI ile C# kullanılarak geliştirilen bu masaüstü uygulaması, 12 haftalık Python ve yazılım mimarisi müfredatını yapılandırılmış bir veri bankasında sunar; anlık LINQ araması, kod kopyalama ve JSON kayıt özellikleri içerir.




# Python Programlama Ansiklopedisi

.NET 8 ve Avalonia UI çatısı altında C# ile geliştirilen bu çapraz platform masaüstü uygulaması, 12 haftalık Python ve yazılım mimarisi müfredatını yapılandırılmış bir veri bankası üzerinde sunar. LINQ tabanlı anlık çoklu alan araması, hafta filtreleme, tek tıkla kod kopyalama ve yerel diske kalıcı JSON kaydı ile **yeni madde ekleme / mevcut madde silme** özelliklerini modern koyu tema (Dark Mode) arayüzüyle birleştirir.

---

## Temel Özellikler

- **6 Katmanlı Yapılandırılmış Konu Kartları:** Her ansiklopedi maddesi; *Kavramsal Anlatım*, *Gerçek Hayat Analojisi*, *Teknik Mekanizma ve Kurallar*, *Python Uygulama Örneği*, *Satır Satır Kod Analizi* ve *Sık Yapılan Hatalar ve İpuçları* başlıklarında sunulur.
- **25 Yerleşik Müfredat Maddesi:** Hafta 1'den Hafta 12'ye kadar modüler tasarım, LEGB kapsam kuralları, OOP (kapsülleme, `@property`, kalıtım, MRO, polimorfizm, soyutlama), istisna yönetimi, dosya I/O, yığın/kuyruk/ağaç/graf veri yapıları ve arama/sıralama algoritmalarını içerir.
- **Anlık Çoklu Alan Arama ve Filtreleme:** Başlık, hafta, kategori, kavramsal anlatım, analoji, Python kodu ve hata ipuçları içinde büyük/küçük harf duyarsız gerçek zamanlı LINQ filtrelemesi yapar.
- **Tek Tıkla Kod Kopyalama:** Aktif konunun Python kodunu doğrudan sistem panosuna kopyalar.
- **Kalıcı Madde Ekleme ve Silme (JSON):**
  - Uygulama içindeki **+ Yeni Ansiklopedi Maddesi Ekle** formuyla eklenen notlar `ekstra_maddeler.json` dosyasına kaydedilir.
  - Sağ üstteki **Maddeyi Sil** butonu ve onay penceresi ile hem özel eklenen maddeler hem de yerleşik maddeler (`silinen_maddeler.json` üzerinden) kalıcı olarak listeden kaldırılabilir.

---

## 1. Bilgisayara Kurulması Gereken Ön Gereksinimler

Bu projeyi ilk defa bilgisayarınızda çalıştıracaksanız aşağıdaki temel aracın kurulu olması gerekir:

1. **.NET 8.0 SDK (Zorunlu):**
   - C# kodlarını derlemek, NuGet paketlerini indirmek ve uygulamayı çalıştırmak için gereklidir.
   - Microsoft'un resmi indirme sayfasından işletim sisteminize (Windows, Linux veya macOS) uygun **.NET 8.0 SDK** paketini indirip kurun.
   - Kurulum bittikten sonra yeni bir terminal (CMD, PowerShell veya Bash) açarak kurulumu doğrulayın:
     ```bash
     dotnet --version
     ```
     *(Ekranda `8.0.xxx` şeklinde bir sürüm numarası görüyorsanız kurulum başarılıdır.)*

2. **Kod Editörü / IDE (İsteğe Bağlı — Kodları İncelemek veya Düzenlemek İçin):**
   - **Visual Studio Code** (yanında **C# Dev Kit** eklentisi ile) veya **Visual Studio 2022**.

---

## 2. Projede Kullanılan Kütüphaneler ve Paketler

Bu projede Python'daki `pip` yerine C# / .NET ekosisteminin paket yöneticisi olan **NuGet** kullanılır. Dışarıdan el ile DLL indirmenize gerek yoktur; tüm paketler tek komutla otomatik indirilir:

### Dış NuGet Paketleri (Otomatik İndirilir)

| Paket Adı | Sürüm | Ne İşe Yarar? |
| :--- | :--- | :--- |
| **`Avalonia`** | `11.2.3` | Çapraz platform kullanıcı arayüzü (UI) motoru, pencere ve kontrol altyapısı. |
| **`Avalonia.Desktop`** | `11.2.3` | Uygulamanın Windows, Linux ve macOS masaüstü ortamlarında yerel pencere olarak çalışmasını sağlar. |
| **`Avalonia.Themes.Fluent`** | `11.2.3` | Modern Fluent tasarım sistemini ve koyu tema (`Dark`) bileşen stillerini sağlar. |
| **`Avalonia.Fonts.Inter`** | `11.2.3` | Uygulama arayüzündeki metinlerin tüm işletim sistemlerinde net görünmesi için gömülü yazı tipini sağlar. |

### Yerleşik .NET 8 Kütüphaneleri (Ek Kurulum Gerektirmez)
- **`System.Text.Json`:** Yeni eklenen (`ekstra_maddeler.json`) ve silinen (`silinen_maddeler.json`) maddelerin yerel diske JSON formatında kaydedilip okunmasını sağlar.
- **`System.Linq` & `System.Collections.ObjectModel`:** Anlık arama filtrelemesi ve arayüz listesinin otomatik güncellenmesi (`ObservableCollection`) için kullanılır.

---

## 3. Adım Adım Kurulum ve Çalıştırma Rehberi

Projeyi bilgisayarınızda sıfırdan ayağa kaldırıp ekranda görene kadar aşağıdaki adımları sırasıyla uygulayın.

### Adım 1: Proje Dosyalarını Bilgisayarınıza Alın
Git kurulumuna gerek kalmadan aşağıdaki iki yöntemden biriyle proje dosyalarını bilgisayarınıza hazırlayabilirsiniz:

- **Yöntem A — ZIP Olarak İndirme (Önerilen ve En Hızlı Yöntem):**
  1. Bu sayfanın sağ üst kısmındaki yeşil **`<> Code`** butonuna tıklayın ve açılan menüden **`Download ZIP`** seçeneğini seçin.
  2. İnen `.zip` dosyasına sağ tıklayıp **"Tümünü Ayıkla" (Extract All)** diyerek klasöre çıkartın.
  3. Çıkarttığınız klasörün içine girin (`ProgramlamaAnsiklopedisi.csproj` dosyasının bulunduğu dizin).
  4. Klasör penceresinin üst adres çubuğuna tıklayıp `cmd` (veya `powershell`) yazarak Enter'a basın; terminal doğrudan proje klasörünün içinde açılacaktır.

- **Yöntem B — Klasörü Kendiniz Oluşturarak Başlatma:**
  1. Bilgisayarınızda `ProgramlamaAnsiklopedisi` adında boş bir klasör oluşturun ve bu klasör içinde terminali açın.
  2. Temel .NET 8 proje iskeletini oluşturmak için şu komutu çalıştırın:
     ```bash
     dotnet new console -f net8.0
     ```
  3. Bu depodaki 6 ana dosyayı (`ProgramlamaAnsiklopedisi.csproj`, `Program.cs`, `App.axaml`, `App.axaml.cs`, `MainWindow.axaml`, `MainWindow.axaml.cs`) indirip veya içeriklerini kopyalayarak bu klasörün içine kaydedin (otomatik oluşan `Program.cs` dosyasının üzerine yazın).

### Adım 2: Gerekli Avalonia Kütüphanelerini Yükleyin (`restore`)
Proje klasörü içindeyken aşağıdaki komutu çalıştırarak `.csproj` dosyasında tanımlı tüm NuGet paketlerini (`Avalonia 11.2.3` ve bağımlılıklarını) indirin:
```bash
dotnet restore
```
*(Eğer **Yöntem B** ile sıfırdan proje oluşturduysanız ve `.csproj` dosyasını el ile düzenlemediyseniz, paketleri tek tek eklemek için şu 4 komutu çalıştırabilirsiniz:)*
```bash
dotnet add package Avalonia --version 11.2.3
dotnet add package Avalonia.Desktop --version 11.2.3
dotnet add package Avalonia.Themes.Fluent --version 11.2.3
dotnet add package Avalonia.Fonts.Inter --version 11.2.3
```

### Adım 3: Projeyi Derleyin (`build`)
Tüm kodların ve kütüphanelerin hatasız eşleştiğini doğrulamak için projeyi derleyin:
```bash
dotnet build
```
Çıktının sonunda **`Build succeeded. 0 Warning(s) 0 Error(s)`** mesajını görmelisiniz.

### Adım 4: Uygulamayı Çalıştırın (`run`)
Aşağıdaki komutu çalıştırarak masaüstü uygulamasını başlatın:
```bash
dotnet run
```

---

## 4. Uygulama Çalıştıktan Sonra Doğrulama ve Kullanım

`dotnet run` komutundan birkaç saniye sonra **Python Programlama Ansiklopedisi** masaüstü penceresi açılacaktır. Uygulamanın tüm bileşenlerinin doğru çalıştığını şu adımlarla test edebilirsiniz:

1. **Arayüz Kontrolü:**
   - **Sol Panel:** Arama kutusu, hafta filtresi ve `25 madde listeleniyor` sayacı ile konu listesi görünür.
   - **Sağ Panel:** Seçili konunun hafta/kategori rozetleri, gezinme butonları ve 6 ayrı içerik kartı görünür.
2. **Arama ve Filtreleme:** Sol üstteki arama kutusuna `LEGB`, `Binary` veya `Stack` yazarak listenin anlık filtrelendiğini doğrulayın.
3. **Kod Kopyalama:** Sağ paneldeki **Kodu Kopyala** butonuna basın; buton `Kopyalandı ✓` olarak değişir ve Python kodu sistem panonuza aktarılır.
4. **Yeni Madde Ekleme:** Sol alttaki **+ Yeni Ansiklopedi Maddesi Ekle** butonuna tıklayıp başlık ve içerik girerek kaydedin. Kayıt anında listeye eklenir ve uygulama dizinine `ekstra_maddeler.json` olarak kaydedilir.
5. **Madde Silme:** Sağ üstteki **Maddeyi Sil** butonuna tıklayıp onay penceresinde **Evet, Sil** seçeneğini onaylayın. Madde listeden kaldırılır ve uygulama kapatılıp tekrar açıldığında da silinmiş olarak kalır.

---

## 5. Proje Dosya Yapısı

```text
ProgramlamaAnsiklopedisi/
├── ProgramlamaAnsiklopedisi.csproj   # .NET 8 hedef çerçevesi ve Avalonia NuGet paket tanımları
├── Program.cs                        # Uygulama giriş noktası (Main & AppBuilder)
├── App.axaml                         # Genel koyu tema (Dark) ve FluentTheme stili
├── App.axaml.cs                      # Masaüstü yaşam döngüsü ve ana pencere başlatıcı
├── MainWindow.axaml                  # Sol liste, sağ 6 kartlı detay paneli, ekleme ve silme modalları
├── MainWindow.axaml.cs               # Veri modeli, LINQ arama, JSON kalıcılığı ve 25 maddelik veri bankası
├── ekstra_maddeler.json              # (Çalışma zamanında oluşur) Kullanıcının eklediği özel maddeler
└── silinen_maddeler.json             # (Çalışma zamanında oluşur) Kullanıcının sildiği yerleşik maddeler
```
