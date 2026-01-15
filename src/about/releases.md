---
outline: deep
---

<script setup>
import { ref, onMounted } from 'vue'

const version = ref()

onMounted(async () => {
  const res = await fetch('https://api.github.com/repos/vuejs/core/releases/latest')
  version.value = (await res.json()).name
})
</script>

# Sürümler {#releases}

<p v-if="version">
Vue’nun şu anki en güncel kararlı sürümü <strong>{{ version }}</strong>.
</p>
<p v-else>
En son sürüm kontrol ediliyor...
</p>

Geçmiş sürümlerin tamamına ait değişiklik günlüğü [GitHub](https://github.com/vuejs/core/blob/main/CHANGELOG.md) üzerinde mevcuttur.

## Sürüm Döngüsü {#release-cycle}

Vue’nun sabit bir sürüm takvimi yoktur.

- **Yama (patch)** sürümleri ihtiyaç oldukça yayımlanır.

- **Küçük (minor)** sürümler her zaman yeni özellikler içerir ve genellikle aralarında 3–6 ay bulunur. Küçük sürümler her zaman bir beta ön sürüm aşamasından geçer.

- **Büyük (major)** sürümler önceden duyurulur ve erken tartışma, ardından alfa ve beta ön sürüm aşamalarından geçer.

## Semantik Sürümleme İstisnaları {#semantic-versioning-edge-cases}

Vue sürümleri, bazı istisnalarla birlikte [Semantic Versioning](https://semver.org/) standardını takip eder.

### TypeScript Tanımları {#typescript-definitions}

**Küçük (minor)** sürümler arasında TypeScript tanımlarında uyumsuz değişiklikler yapabiliriz. Bunun sebepleri şunlardır:

1. TypeScript’in kendisi bazen küçük sürümler arasında uyumsuz değişiklikler yapar ve daha yeni TypeScript sürümlerini desteklemek için türleri uyarlamamız gerekebilir.

2. Bazen yalnızca daha yeni TypeScript sürümlerinde bulunan özellikleri kullanmamız gerekir; bu da minimum gerekli TypeScript sürümünü yükseltir.

TypeScript kullanıyorsanız, mevcut küçük sürümü kilitleyen bir semver aralığı kullanabilir ve Vue’nun yeni bir küçük sürümü çıktığında manuel olarak yükseltebilirsiniz.

### Derlenmiş Kodun Eski Runtime ile Uyumluluğu {#compiled-code-compatibility-with-older-runtime}

Vue derleyicisinin daha yeni bir **küçük (minor)** sürümü, daha eski bir küçük sürüme ait Vue runtime ile uyumlu olmayan kod üretebilir. Örneğin Vue 3.2 derleyicisinin ürettiği kod, Vue 3.1 runtime’ı tarafından tam olarak çalıştırılamayabilir.

Bu durum yalnızca kütüphane yazarları için önemlidir; çünkü uygulamalarda derleyici ve runtime sürümü her zaman aynıdır. Sürüm uyumsuzluğu, yalnızca önceden derlenmiş Vue bileşen kodunu bir paket olarak dağıtıp, bunu daha eski bir Vue sürümü kullanan bir projede tükettiğinizde ortaya çıkar. Bu nedenle, paketiniz Vue için açıkça minimum gerekli küçük sürümü belirtmek zorunda kalabilir.

## Ön Sürümler {#pre-releases}

Küçük sürümler genellikle sabit olmayan sayıda beta sürümden geçer. Büyük sürümler ise bir alfa ve bir beta aşamasından geçer.

Buna ek olarak, GitHub’daki `main` ve `minor` dallarından her hafta **canary** sürümler yayımlarız. Bunlar kararlı kanalın npm metadata’sını şişirmemek için ayrı paketler olarak yayımlanır. Sırasıyla `npx install-vue@canary` veya `npx install-vue@canary-minor` komutlarıyla kurulabilirler.

Ön sürümler entegrasyon / kararlılık testleri ve erken kullanıcıların kararsız özellikler hakkında geri bildirim vermesi için tasarlanmıştır. Ön sürümleri üretim ortamında kullanmayın. Tüm ön sürümler kararsız kabul edilir ve aralarında kırıcı değişiklikler içerebilir; bu nedenle ön sürüm kullanırken her zaman tam sürüm numarasına kilitleyin.

## Kullanımdan Kaldırmalar {#deprecations}

Yeni ve daha iyi alternatifleri bulunan özellikleri, küçük sürümlerde zaman zaman kullanım dışı bırakabiliriz. Kullanımdan kaldırılan özellikler çalışmaya devam eder, ancak kullanım dışı bırakıldıktan sonraki bir sonraki büyük sürümde tamamen kaldırılır.

## RFC’ler {#rfcs}

Geniş API yüzeyine sahip yeni özellikler ve Vue’daki büyük değişiklikler **Request for Comments (RFC)** sürecinden geçer. RFC süreci, yeni özelliklerin framework’e tutarlı ve kontrollü bir şekilde girmesini sağlamak ve kullanıcıların tasarım sürecine katılıp geri bildirim verebilmesine imkân tanımak için tasarlanmıştır.

RFC süreci GitHub üzerindeki [vuejs/rfcs](https://github.com/vuejs/rfcs) deposunda yürütülür.

## Deneysel Özellikler {#experimental-features}

Bazı özellikler Vue’nun kararlı bir sürümünde yayımlanır ve belgelenir, ancak **deneysel** olarak işaretlenir. Deneysel özellikler genellikle bir RFC tartışmasına sahip olan, tasarım problemlerinin büyük ölçüde çözüldüğü fakat gerçek dünya kullanımından henüz yeterli geri bildirim alınmamış özelliklerdir.

Deneysel özelliklerin amacı, kullanıcıların kararsız bir Vue sürümüne geçmek zorunda kalmadan bu özellikleri üretim ortamında test ederek geri bildirim verebilmesini sağlamaktır. Deneysel özellikler kendi başlarına kararsız kabul edilir ve herhangi bir sürüm türü arasında değişebilir; bu nedenle kontrollü şekilde kullanılmaları gerekir.
