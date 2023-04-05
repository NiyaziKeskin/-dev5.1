"""
Dekoratörler
Yöntem 1: @decorator def func(): pass

Yöntem 2: def func(): pass
func = decorator(func)
Yukarıdaki örnekte; üstteki pie syntax ile yazılmış dekoratörün yaptığı iş aslında hemen altındaki bölümün yaptığı iş ile aynıdır. Kullanım kolaylığı sağlamak ve okunabilirliği artırmak açısından böyle bir söz dizimi tercih edilmiş.

Python Decorator Örnekleri Python’da decorator fonksiyonları yazabilmemiz için gerekli bir konsept vardır. First-class everything konsepti.

def say_hello_decorator(func): def wrapper(): print("Hello ", end="") func() return wrapper First-class everything konseptinde, nesneler değişkene atanabilir, başka nesneler içinde saklanabilir, parametre olabilir ve geri dönüş değeri olabilirler. Decoratorlerin yaptığı şey, decorator fonksiyonuna parametre olarak bir fonksiyon alınır. Bu fonksiyon, başka bir fonksiyon içinde çağırılır ancak, ekstra işlevler ile birlikte. Daha sonra decorate edilmiş fonksiyon geri döndürülür.

Fikstür Bazı veri kümelerini somutlaştırmanın ilk ve en kolay yolu, pytest fikstürlerini kullanmaktır. pytest.fixture dekoratör, dönüş değerinin, imzalarında dekore edilmiş fonksiyon adı bulunan test fonksiyonlarına enjekte edilmesini mümkün kılar. Anlamak, onu çalışırken görmekten gerçekten daha zor: def get_gender_heading(name):

Decoratorler aslında birer wrapperdır. Fonksiyonun davranışı değiştirmeye yararlar. Fonksiyon çalışmadan önce yapılması gereken bir şey varsa veya fonksiyonları dinamik olarak bir yerlere kayıt etmek istiyorsanız decoratorler bu iş için biçilmiş kaftandır.

Dekoratörler, kapsamasını istediğimiz fonksiyonların üzerine, önünde @ karakteri konularak yazılır. Buna pie syntax denir. Aslında bu yazım stili sadece bir kısayoldan ibarettir.

# süper AI tabanlı algoritma (2018 gibi, çok AI) 
# Verilen bir isim için "Bay" veya "Bayan" döndürür.
@pytest.fixture def male_name(): 'Phil'i döndür @pytest.fixture def female_name(): 'Claire' değerini döndür def test_male_prefix(male_name): 'Bay' deyin. == get_gender_heading(erkek_adı) def test_female_prefix(female_name): 'Bayan' deyin. == get_gender_heading(kadın_adı)

Bu fikstürü parametre ile test etmeden çalıştırın autouse. Bu, işlevlere yama/alaycı ekleme yaparken özellikle yararlıdır: @pytest.fixture(autouse=True, scope='function') def common_patches(): mock.patch(...)

Parametreli testler pytest.mark.parametrize kurtarmak için! Yukarıdaki dekoratör çok güçlü bir işlevselliktir, her yinelemede girilen parametreleri değiştirerek bir test işlevini birden çok kez çağırmaya izin verir. İlk bağımsız değişken, dekore edilmiş işlevin bağımsız değişkenlerini virgülle ayrılmış bir dizeyle listeler. İkinci bağımsız değişken, çağrı değerleri için yinelenebilir.

@pytest.mark.parametrize('isim', ['Claire', 'Gloria', 'Haley']) def test_female_prefix_v2(name): 'Bayan' iddiası == get_gender_heading(isim)

Böylece, pytest birden çok kez arayacaktır test_female_prefix_v2: önce ile name='Claire', sonra ile name='Gloria'vb. Bu, özellikle aynı anda birden çok bağımsız değişken kullanıldığında kullanışlıdır:

@pytest.mark.parametrize( 'isim, bekleniyor', [('Claire', 'Mrs'), ('Jay', 'Mr')] )
def test_both_sex_v2(isim, bekleniyor): iddia bekleniyor == get_gender_heading(name )

Birden çok bağımsız değişkenle, pytest.mark.parametrizedizine dayalı basit bir ilişkilendirme gerçekleştirir, bu nedenle while önce ve sonra değerleri namevarsayar , ve değerleri alır .ClaireJayexpectedMrsMr

Bazı Dekoratörler

pytest.approx(): İki veya ikiden fazla sayının sayı kümeleri yaklaşık olarak bazı farklılıklara eşitler.

pytest.fail(): Yürütülmekte olan test açıkça başarısız olursa, mesaj gösterir.

pytest.skip(): Gösterilen mesajla yürütme testini atlatır.

pytest.exit(): Test sürecinden çıkartır.

pytest.main(): İşlem içi test yürütmesi tamamlandığında çıkış kodunu döndürür

pytest.raises(): Bir kod bloğu çağrısının beklenen istisnayı ortaya çıkardığını veya bir hata istisnası oluşturduğunu ileri sürer.

pytest.mark.skip(): Bu dekoratör bir test fonksiyonunda belirlenen testi atlamak için kullanılır.

pytest.mark.timeout(): Bir testin belirli bir sürede tamamlanması gerektiğini belirlemek için kullanılır.
