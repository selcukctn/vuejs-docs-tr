# Sık Sorulan Sorular {#frequently-asked-questions}

## Vue’yu kim yönetiyor? {#who-maintains-vue}

Vue, bağımsız ve topluluk odaklı bir projedir. 2014 yılında [Evan You](https://x.com/youyuxi) tarafından kişisel bir yan proje olarak oluşturulmuştur.  
Bugün Vue, dünyanın dört bir yanından gelen tam zamanlı ve gönüllü üyelerden oluşan bir [ekip](/about/team) tarafından aktif olarak sürdürülmektedir ve Evan proje lideri olarak görev yapmaktadır. Vue’nun hikâyesini bu [belgeselde](https://www.youtube.com/watch?v=OrxmtDw4pVI) daha ayrıntılı olarak öğrenebilirsiniz.

Vue’nun geliştirilmesi ağırlıklı olarak sponsorluklar ile finanse edilmektedir ve 2016’dan bu yana mali açıdan sürdürülebilirdir. Siz veya şirketiniz Vue’dan fayda sağlıyorsa, Vue’nun gelişimini desteklemek için [bize sponsor olmayı](/sponsor/) düşünebilirsiniz.

## Vue 2 ile Vue 3 arasındaki fark nedir? {#what-s-the-difference-between-vue-2-and-vue-3}

Vue 3, Vue’nun mevcut ve en güncel ana sürümüdür. Vue 2’de bulunmayan Teleport, Suspense ve şablon başına birden fazla kök eleman gibi yeni özellikler içerir. Ayrıca Vue 2 ile uyumsuz olan kırıcı (breaking) değişiklikler de barındırır. Tüm ayrıntılar [Vue 3 Geçiş Rehberi](https://v3-migration.vuejs.org/) içinde belgelenmiştir.

Farklara rağmen Vue API’lerinin büyük bölümü her iki ana sürüm arasında ortaktır; bu nedenle Vue 2 bilginizin çoğu Vue 3’te de geçerli olmaya devam eder. Özellikle Composition API başlangıçta yalnızca Vue 3’e özgüydü, ancak daha sonra Vue 2’ye de geri taşındı ve artık [Vue 2.7](https://github.com/vuejs/vue/blob/main/CHANGELOG.md#270-2022-07-01) içinde mevcuttur.

Genel olarak Vue 3 daha küçük paket boyutları, daha iyi performans, daha iyi ölçeklenebilirlik ve daha iyi TypeScript / IDE desteği sunar. Bugün yeni bir projeye başlıyorsanız önerilen seçim Vue 3’tür. Şu anda Vue 2’yi tercih etmeniz için yalnızca birkaç neden vardır:

- IE11 desteğine ihtiyacınız varsa. Vue 3 modern JavaScript özelliklerinden yararlanır ve IE11’i desteklemez.

Mevcut bir Vue 2 uygulamasını Vue 3’e taşımayı planlıyorsanız, [geçiş rehberine](https://v3-migration.vuejs.org/) bakın.

## Vue 2 hâlâ destekleniyor mu? {#is-vue-2-still-supported}

Temmuz 2022’de yayımlanan Vue 2.7, Vue 2 sürüm ailesinin son küçük sürümüdür. Vue 2 bakım moduna girmiştir: yeni özellikler almayacak, ancak 2.7 sürüm tarihinden itibaren 18 ay boyunca kritik hata düzeltmeleri ve güvenlik güncellemeleri almaya devam edecektir. Bu da **Vue 2’nin 31 Aralık 2023 itibarıyla kullanım ömrünün sona erdiği** anlamına gelir.

Bunun ekosistemin büyük bölümü için Vue 3’e geçiş yapmak adına yeterli süre sunduğuna inanıyoruz. Ancak bazı ekiplerin veya projelerin bu zaman çizelgesine uyamayacağını ve yine de güvenlik ve uyumluluk gereksinimlerini karşılamak zorunda olduğunu da biliyoruz. Bu tür ihtiyaçları olan ekipler için Vue 2’ye uzatılmış destek sağlamak üzere sektör uzmanlarıyla iş birliği yapıyoruz. Eğer ekibinizin 2023 sonrasına kadar Vue 2 kullanmaya devam etmesi gerekiyorsa, [Vue 2 Extended LTS](https://v2.vuejs.org/lts/) hakkında bilgi edinmeniz ve önceden planlama yapmanız önemlidir.

## Vue hangi lisansı kullanıyor? {#what-license-does-vue-use}

Vue, [MIT Lisansı](https://opensource.org/licenses/MIT) altında yayımlanan ücretsiz ve açık kaynaklı bir projedir.

## Vue hangi tarayıcıları destekler? {#what-browsers-does-vue-support}

Vue’nun en güncel sürümü (3.x), yalnızca [yerel ES2016 desteğine sahip tarayıcıları](https://caniuse.com/es2016) destekler. Bu, IE11’i kapsam dışı bırakır. Vue 3.x, eski tarayıcılarda polyfill edilemeyen ES2016 özelliklerini kullandığı için, eski tarayıcıları desteklemeniz gerekiyorsa Vue 2.x kullanmanız gerekir.

## Vue güvenilir mi? {#is-vue-reliable}

Vue olgun ve sahada kendini kanıtlamış bir framework’tür. Bugün dünyada 1,5 milyondan fazla kullanıcıya sahip olup npm üzerinde ayda yaklaşık 10 milyon kez indirilmektedir.

Vue; Wikimedia Foundation, NASA, Apple, Google, Microsoft, GitLab, Zoom, Tencent, Weibo, Bilibili, Kuaishou ve daha pek çok kuruluş tarafından üretim ortamlarında kullanılmaktadır.

## Vue hızlı mı? {#is-vue-fast}

Vue 3, ana akım frontend framework’leri arasında en yüksek performanslı olanlardan biridir ve manuel optimizasyona gerek kalmadan çoğu web uygulaması senaryosunu rahatlıkla karşılar.

Stres testlerinde Vue, [js-framework-benchmark](https://krausest.github.io/js-framework-benchmark/current.html) içinde React ve Angular’ı belirgin bir farkla geride bırakır ve bazı en hızlı sanal DOM kullanmayan framework’lerle başa baş performans gösterir.

Bu tür sentetik benchmark’ların ham render performansına odaklandığını ve gerçek dünya sonuçlarını tam yansıtmayabileceğini unutmayın. Sayfa yükleme performansı sizin için daha önemliyse, bu web sitesini [WebPageTest](https://www.webpagetest.org/lighthouse) veya [PageSpeed Insights](https://pagespeed.web.dev/) ile test edebilirsiniz. Bu site Vue ile çalışır; SSG ön render, tam sayfa hydration ve SPA istemci yönlü gezinme kullanır. Yavaş 4G ve 4× CPU kısıtlamalı Moto G4 simülasyonunda performans skoru 100’dür.

Vue’nun çalışma zamanında performansı nasıl otomatik olarak optimize ettiğini [Render Mekanizması](/guide/extras/rendering-mechanism) bölümünde ve yoğun senaryolar için uygulama optimizasyonunu [Performans Optimizasyon Rehberi](/guide/best-practices/performance) içinde öğrenebilirsiniz.

## Vue hafif mi? {#is-vue-lightweight}

Bir build aracı kullandığınızda Vue API’lerinin büyük kısmı ["tree-shakable"](https://developer.mozilla.org/en-US/docs/Glossary/Tree_shaking) yapıdadır. Örneğin yerleşik `<Transition>` bileşenini kullanmıyorsanız, üretim paketine dahil edilmez.

Sadece en temel API’leri kullanan basit bir “Hello World” Vue uygulaması, minify ve Brotli sıkıştırmasıyla yaklaşık **16kb** boyutundadır. Gerçek uygulama boyutu, kullandığınız opsiyonel özelliklere bağlıdır. Teorik olarak Vue’nun sunduğu tüm özellikleri kullanan bir uygulamanın çalışma zamanı boyutu yaklaşık **27kb**’dır.

Vue’yu bir build aracı olmadan kullandığınızda hem tree-shaking kaybolur hem de şablon derleyicisi tarayıcıya gönderilmek zorunda kalır. Bu durumda boyut yaklaşık **41kb** olur. Eğer Vue’yu yalnızca kademeli iyileştirme (progressive enhancement) için ve build adımı olmadan kullanıyorsanız, bunun yerine yalnızca **6kb** olan [petite-vue](https://github.com/vuejs/petite-vue) kullanmayı düşünebilirsiniz.

Svelte gibi bazı framework’ler tek bileşenli senaryolarda çok küçük çıktılar üreten derleme stratejileri kullanır. Ancak [araştırmamız](https://github.com/yyx990803/vue-svelte-size-analysis), boyut farkının uygulamadaki bileşen sayısına büyük ölçüde bağlı olduğunu göstermektedir. Vue’nun temel boyutu daha büyük olsa da, bileşen başına daha az kod üretir. Gerçek dünyada bir Vue uygulaması pekâlâ daha hafif olabilir.

## Vue ölçeklenebilir mi? {#does-vue-scale}

Evet. Vue’nun yalnızca basit kullanım senaryoları için uygun olduğu yönündeki yaygın yanılgıya rağmen, büyük ölçekli uygulamaları rahatlıkla destekler:

- [Tek Dosyalı Bileşenler](/guide/scaling-up/sfc), uygulamanın farklı bölümlerinin izole şekilde geliştirilmesini sağlayan modüler bir model sunar.
- [Composition API](/guide/reusability/composables), birinci sınıf TypeScript entegrasyonu sağlar ve karmaşık mantığın düzenlenmesi, çıkarılması ve yeniden kullanılması için temiz kalıplar sunar.
- [Kapsamlı araç desteği](/guide/scaling-up/tooling), uygulama büyüdükçe sorunsuz bir geliştirme deneyimi sağlar.
- Düşük giriş bariyeri ve mükemmel dokümantasyon, yeni geliştiriciler için daha düşük adaptasyon ve eğitim maliyeti anlamına gelir.

## Vue’ya nasıl katkıda bulunabilirim? {#how-do-i-contribute-to-vue}

İlginiz için teşekkür ederiz! Lütfen [Topluluk Rehberi](/about/community-guide) sayfasına göz atın.

## Options API mi yoksa Composition API mi kullanmalıyım? {#should-i-use-options-api-or-composition-api}

Vue’ya yeniyseniz, iki yaklaşımın yüksek seviyeli karşılaştırmasını [burada](/guide/introduction#which-to-choose) bulabilirsiniz.

Daha önce Options API kullandıysanız ve Composition API’yi değerlendiriyorsanız, [bu SSS](/guide/extras/composition-api-faq) sayfasına göz atın.

## Vue ile JavaScript mi yoksa TypeScript mi kullanmalıyım? {#should-i-use-javascript-or-typescript-with-vue}

Vue’nun kendisi TypeScript ile yazılmış ve birinci sınıf TypeScript desteği sunuyor olsa da, kullanıcı olarak TypeScript kullanıp kullanmamanız konusunda bir zorunluluk getirmez.

Yeni özellikler eklenirken TypeScript desteği önemli bir kriterdir. TypeScript düşünülerek tasarlanan API’ler, TypeScript kullanmasanız bile IDE’ler ve linter’lar tarafından daha kolay anlaşılır. Kazanan herkes olur. Vue API’leri de mümkün olduğunca JavaScript ve TypeScript’te aynı şekilde çalışacak biçimde tasarlanmıştır.

TypeScript kullanmak, başlangıç karmaşıklığı ile uzun vadeli sürdürülebilirlik kazanımları arasında bir denge gerektirir. Bu dengenin ekibiniz ve proje ölçeğiniz için uygun olup olmadığı değişebilir; ancak bu kararı belirleyen esas unsur Vue değildir.

## Vue, Web Components ile nasıl karşılaştırılır? {#how-does-vue-compare-to-web-components}

Vue, Web Components tarayıcılarda yerel olarak desteklenmeden önce oluşturulmuştur ve Vue’nun bazı tasarım unsurları (örneğin slot’lar) Web Components modelinden esinlenmiştir.

Web Components spesifikasyonları görece düşük seviyelidir ve özel HTML elementleri tanımlamaya odaklanır. Vue ise bir framework olarak verimli DOM render, reaktif durum yönetimi, araçlar, istemci yönlü yönlendirme ve sunucu tarafı render gibi daha üst seviye ihtiyaçları da ele alır.

Vue ayrıca yerel custom element’leri kullanmayı veya dışa aktarmayı tam olarak destekler. Daha fazla bilgi için [Vue ve Web Components Rehberi](/guide/extras/web-components) sayfasına bakın.

<!-- ## TODO Vue, React ile nasıl karşılaştırılır? -->

<!-- ## TODO Vue, Angular ile nasıl karşılaştırılır? -->
