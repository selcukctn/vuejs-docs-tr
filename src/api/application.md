# Uygulama API’si {#application-api}

## createApp() {#createapp}

Bir uygulama örneği oluşturur.

- **Tür**

  ```ts
  function createApp(rootComponent: Component, rootProps?: object): App
  ```

- **Detaylar**

  İlk argüman kök bileşendir. İkinci (isteğe bağlı) argüman, kök bileşene geçirilecek props nesnesidir.

- **Örnek**

  Satır içi kök bileşen ile:

  ```js
  import { createApp } from 'vue'

  const app = createApp({
    /* kök bileşen seçenekleri */
  })
  ```

  İçe aktarılmış bileşen ile:

  ```js
  import { createApp } from 'vue'
  import App from './App.vue'

  const app = createApp(App)
  ```

- **Ayrıca bakınız** [Rehber – Vue Uygulaması Oluşturma](/guide/essentials/application)

## createSSRApp() {#createssrapp}

[SSR Hydration](/guide/scaling-up/ssr#client-hydration) modunda bir uygulama örneği oluşturur. Kullanımı birebir aynıdır. `createApp()`.

## app.mount() {#app-mount}

Uygulama örneğini bir kapsayıcı elemana bağlar (mount eder).

- **Tip**

  ```ts
  interface App {
    mount(rootContainer: Element | string): ComponentPublicInstance
  }
  ```

- **Detaylar**

  Argüman ya gerçek bir DOM elemanı ya da bir CSS seçicisi olabilir (ilk eşleşen eleman kullanılır). Kök bileşen örneğini döndürür.

  Bileşenin bir şablonu veya bir `render` fonksiyonu tanımlıysa, kapsayıcı içindeki mevcut DOM düğümlerinin tamamı bununla değiştirilir. Aksi hâlde, runtime derleyici mevcutsa kapsayıcının `innerHTML` içeriği şablon olarak kullanılır.

  SSR hydration modunda, kapsayıcı içindeki mevcut DOM düğümleri hydrate edilir. Eğer [uyuşmazlıklar](/guide/scaling-up/ssr#hydration-mismatch) varsa, mevcut DOM düğümleri beklenen çıktıyla eşleşecek şekilde dönüştürülür.

  Her uygulama örneği için `mount()` yalnızca bir kez çağrılabilir.

- **Örnek**

  ```js
  import { createApp } from 'vue'
  const app = createApp(/* ... */)

  app.mount('#app')
  ```

  Gerçek bir DOM elemanına da bağlanabilir:

  ```js
  app.mount(document.body.firstChild)
  ```

## app.unmount() {#app-unmount}

Bağlanmış (mount edilmiş) bir uygulama örneğini kaldırır ve uygulamanın bileşen ağacındaki tüm bileşenler için unmount yaşam döngüsü kancalarını tetikler.

- **Tip**

  ```ts
  interface App {
    unmount(): void
  }
  ```

## app.onUnmount() <sup class="vt-badge" data-text="3.5+" /> {#app-onunmount}

Uygulama kaldırıldığında çağrılacak bir geri çağırma (callback) fonksiyonu kaydeder.

- **Tip**

  ```ts
  interface App {
    onUnmount(callback: () => any): void
  }
  ```

## app.component() {#app-component}

Hem bir ad dizesi hem de bir bileşen tanımı verildiğinde genel (global) bir bileşen kaydeder; yalnızca ad verildiğinde ise daha önce kaydedilmiş olanı döndürür.

- **Tip**

  ```ts
  interface App {
    component(name: string): Component | undefined
    component(name: string, component: Component): this
  }
  ```

- **Örnek**

  ```js
  import { createApp } from 'vue'

  const app = createApp({})

  // register an options object
  app.component('MyComponent', {
    /* ... */
  })

  // retrieve a registered component
  const MyComponent = app.component('MyComponent')
  ```

- **Ayrıca bakınız** [Component Registration](/guide/components/registration)

## app.directive() {#app-directive}

Hem bir ad dizesi hem de bir yönerge tanımı verildiğinde genel (global) bir özel yönerge kaydeder; yalnızca ad verildiğinde ise daha önce kaydedilmiş olanı döndürür.

- **Tip**

  ```ts
  interface App {
    directive(name: string): Directive | undefined
    directive(name: string, directive: Directive): this
  }
  ```

- **Örnek**

  ```js
  import { createApp } from 'vue'

  const app = createApp({
    /* ... */
  })

  // register (object directive)
  app.directive('myDirective', {
    /* custom directive hooks */
  })

  // register (function directive shorthand)
  app.directive('myDirective', () => {
    /* ... */
  })

  // retrieve a registered directive
  const myDirective = app.directive('myDirective')
  ```

- **Ayrıca bakınız** [Custom Directives](/guide/reusability/custom-directives)

## app.use() {#app-use}

Installs a [plugin](/guide/reusability/plugins).

- **Tip**

  ```ts
  interface App {
    use(plugin: Plugin, ...options: any[]): this
  }
  ```

- **Detaylar**

İlk argüman olarak eklentiyi (plugin), ikinci argüman olarak ise isteğe bağlı eklenti seçeneklerini bekler.

Eklenti, bir `install()` metoduna sahip bir nesne olabileceği gibi, doğrudan `install()` metodu olarak kullanılacak bir fonksiyon da olabilir. Seçenekler (`app.use()` metodunun ikinci argümanı) eklentinin `install()` metoduna iletilir.

Aynı eklenti için `app.use()` birden fazla kez çağrılsa bile, eklenti yalnızca bir kez yüklenir.

- **Örnek**

  ```js
  import { createApp } from 'vue'
  import MyPlugin from './plugins/MyPlugin'

  const app = createApp({
    /* ... */
  })

  app.use(MyPlugin)
  ```

- **Ayrıca bakınız** [Plugins](/guide/reusability/plugins)

## app.mixin() {#app-mixin}

Uygulama kapsamına özel bir genel (global) mixin uygular. Bir global mixin, içerdiği seçenekleri uygulamadaki her bileşen örneğine uygular.

:::warning Önerilmez
Mixin’ler Vue 3’te ağırlıklı olarak ekosistem kütüphanelerinde yaygın kullanımları nedeniyle geriye dönük uyumluluk amacıyla desteklenmektedir. Mixin kullanımı — özellikle global mixin’ler — uygulama kodunda kaçınılmalıdır.

Mantık paylaşımı için bunun yerine [Composables](/guide/reusability/composables) tercih edilmelidir.
:::

- **Tip**

  ```ts
  interface App {
    mixin(mixin: ComponentOptions): this
  }
  ```

## app.provide() {#app-provide}

Uygulama içindeki tüm alt (descendant) bileşenlerde enjekte edilebilecek bir değer sağlar.

- **Tip**

  ```ts
  interface App {
    provide<T>(key: InjectionKey<T> | symbol | string, value: T): this
  }
  ```

- **Detaylar**

İlk argüman olarak enjeksiyon anahtarını, ikinci argüman olarak sağlanan değeri bekler. Uygulama örneğinin kendisini döndürür.

- **Örnek**

  ```js
  import { createApp } from 'vue'

  const app = createApp(/* ... */)

  app.provide('message', 'hello')
  ```

  Uygulama içindeki bir bileşen içerisinde:

  <div class="composition-api">

  ```js
  import { inject } from 'vue'

  export default {
    setup() {
      console.log(inject('message')) // 'hello'
    }
  }
  ```

  </div>
  <div class="options-api">

  ```js
  export default {
    inject: ['message'],
    created() {
      console.log(this.message) // 'hello'
    }
  }
  ```

  </div>

- **Ayrıca bakınız**
  - [Provide / Inject](/guide/components/provide-inject)
  - [App-level Provide](/guide/components/provide-inject#app-level-provide)
  - [app.runWithContext()](#app-runwithcontext)

## app.runWithContext() {#app-runwithcontext}

- Yalnızca 3.3+ sürümlerinde desteklenir

Geçerli uygulamayı enjeksiyon bağlamı olarak kullanarak bir geri çağırma (callback) fonksiyonunu çalıştırır.

- **Tip**

  ```ts
  interface App {
    runWithContext<T>(fn: () => T): T
  }
  ```

- **Detaylar**

  Bir geri çağırma (callback) fonksiyonu bekler ve bu fonksiyonu hemen çalıştırır. Callback’in senkron çalışması sırasında, geçerli aktif bir bileşen örneği olmasa bile `inject()` çağrıları mevcut uygulama tarafından sağlanan değerleri bulabilir. Callback’in döndürdüğü değer de ayrıca döndürülür.

- **Örnek**

  ```js
  import { inject } from 'vue'

  app.provide('id', 1)

  const injected = app.runWithContext(() => {
    return inject('id')
  })

  console.log(injected) // 1
  ```

## app.version {#app-version}

Uygulamanın hangi Vue sürümüyle oluşturulduğunu sağlar. Bu bilgi, farklı Vue sürümlerine göre koşullu mantık gerekebileceği durumlarda [plugin](/guide/reusability/plugins) içinde özellikle faydalıdır.

- **Tip**

  ```ts
  interface App {
    version: string
  }
  ```

- **Örnek**

  Bir eklenti (plugin) içinde sürüm kontrolü yapılması:

  ```js
  export default {
    install(app) {
      const version = Number(app.version.split('.')[0])
      if (version < 3) {
        console.warn('This plugin requires Vue 3')
      }
    }
  }
  ```

- **Ayrıca bakınız** [Global API - version](/api/general#version)

## app.config {#app-config}

Her uygulama örneği, o uygulamaya ait yapılandırma ayarlarını içeren bir `config` nesnesi sunar. Uygulamanızı bağlamadan (mount etmeden) önce bu nesnenin özelliklerini (aşağıda belgelenmiştir) değiştirebilirsiniz.

```js
import { createApp } from 'vue'

const app = createApp(/* ... */)

console.log(app.config)
```

## app.config.errorHandler {#app-config-errorhandler}

Uygulama içinden yayılan yakalanmamış hatalar için genel (global) bir işleyici atar.

- **Tip**

  ```ts
  interface AppConfig {
    errorHandler?: (
      err: unknown,
      instance: ComponentPublicInstance | null,
      // `info` is a Vue-specific error info,
      // e.g. which lifecycle hook the error was thrown in
      info: string
    ) => void
  }
  ```

- **Detaylar**

  Hata işleyicisi üç argüman alır: hata nesnesi, hatayı tetikleyen bileşen örneği ve hatanın kaynağını belirten bir bilgi dizesi.

  Aşağıdaki kaynaklardan gelen hataları yakalayabilir:

  - Bileşen render işlemleri
  - Olay (event) işleyicileri
  - Yaşam döngüsü (lifecycle) kancaları
  - `setup()` fonksiyonu
  - Watcher’lar
  - Özel yönerge (directive) kancaları
  - Transition kancaları

  :::tip
  Üretim ortamında üçüncü argüman (`info`), tam bilgi dizesi yerine kısaltılmış bir kod olur. Kod → metin eşlemesini [Üretim Hata Kodu Referansı](/error-reference/#runtime-errors) sayfasında bulabilirsiniz.
  :::

- **Örnek**

  ```js
  app.config.errorHandler = (err, instance, info) => {
    // handle error, e.g. report to a service
  }
  ```

## app.config.warnHandler {#app-config-warnhandler}

Vue’dan gelen çalışma zamanı (runtime) uyarıları için özel bir işleyici atar.

- **Tip**

  ```ts
  interface AppConfig {
    warnHandler?: (
      msg: string,
      instance: ComponentPublicInstance | null,
      trace: string
    ) => void
  }
  ```

- **Detaylar**

  Uyarı işleyicisi; ilk argüman olarak uyarı mesajını, ikinci argüman olarak kaynağı olan bileşen örneğini ve üçüncü argüman olarak bileşen izleme (trace) dizesini alır.

  Konsoldaki yoğunluğu azaltmak için belirli uyarıları filtrelemek amacıyla kullanılabilir. Tüm Vue uyarıları geliştirme sırasında ele alınmalıdır; bu nedenle bu özellik yalnızca hata ayıklama oturumlarında, çok sayıdaki uyarı arasından belirli olanlara odaklanmak için önerilir ve hata ayıklama tamamlandıktan sonra kaldırılmalıdır.

  :::tip
  Uyarılar yalnızca geliştirme modunda çalışır; bu nedenle bu yapılandırma üretim modunda yok sayılır.
  :::

- **Örnek**

  ```js
  app.config.warnHandler = (msg, instance, trace) => {
    // `trace` is the component hierarchy trace
  }
  ```

## app.config.performance {#app-config-performance}

Bunu `true` olarak ayarladığınızda, tarayıcı geliştirici araçlarının performans/zaman çizelgesi panelinde bileşen başlatma, derleme, render ve patch işlemleri için performans izleme etkinleştirilir. Yalnızca geliştirme modunda ve [performance.mark](https://developer.mozilla.org/en-US/docs/Web/API/Performance/mark) API’sini destekleyen tarayıcılarda çalışır.

- **Tip:** `boolean`

- **Ayrıca bakınız** [Guide - Performance](/guide/best-practices/performance)

## app.config.compilerOptions {#app-config-compileroptions}

Çalışma zamanı (runtime) derleyici seçeneklerini yapılandırır. Bu nesne üzerinde ayarlanan değerler tarayıcı içi şablon derleyicisine aktarılır ve yapılandırılmış uygulamadaki tüm bileşenleri etkiler. Bu seçeneklerin, bileşen bazında [`compilerOptions` seçeneği](/api/options-rendering#compileroptions) ile geçersiz kılınabileceğini unutmayın.

::: warning Önemli
Bu yapılandırma seçeneği yalnızca tam derleme (yani tarayıcıda şablon derleyebilen bağımsız `vue.js`) kullanıldığında geçerlidir. Bir build kurulumuyla runtime-only sürüm kullanıyorsanız, derleyici seçenekleri bunun yerine build aracınızın yapılandırması üzerinden `@vue/compiler-dom`’a iletilmelidir.
:::

- `vue-loader` için: [`compilerOptions` loader seçeneği] üzerinden iletin  
  (https://vue-loader.vuejs.org/options.html#compileroptions).  
  Ayrıca [`vue-cli` içinde nasıl yapılandırılacağını]  
  (https://cli.vuejs.org/guide/webpack.html#modifying-options-of-a-loader) da inceleyin.

- `vite` için: [`@vitejs/plugin-vue` seçenekleri] üzerinden iletin  
  (https://github.com/vitejs/vite-plugin-vue/tree/main/packages/plugin-vue#options).
  :::

### app.config.compilerOptions.isCustomElement {#app-config-compileroptions-iscustomelement}

Yerel (native) özel elemanları tanımak için bir kontrol yöntemi belirtir.

- **Tip:** `(tag: string) => boolean`

- **Detaylar**

  Bir etiketin yerel bir özel eleman olarak ele alınması gerekiyorsa `true` döndürmelidir. Eşleşen bir etiket için Vue, onu bir Vue bileşeni olarak çözmeye çalışmak yerine yerel bir eleman olarak render eder.

  Yerel HTML ve SVG etiketlerinin bu fonksiyonla eşleştirilmesine gerek yoktur — Vue’nun ayrıştırıcısı (parser) bunları otomatik olarak tanır.

- **Örnek**

  ```js
  // treat all tags starting with 'ion-' as custom elements
  app.config.compilerOptions.isCustomElement = (tag) => {
    return tag.startsWith('ion-')
  }
  ```

- **Ayrıca bakınız** [Vue and Web Components](/guide/extras/web-components)

### app.config.compilerOptions.whitespace {#app-config-compileroptions-whitespace}

Şablondaki boşluk (whitespace) işleme davranışını ayarlar.

- **Tip:** `'condense' | 'preserve'`

- **Varsayılan:** `'condense'`

- **Detaylar**

  Vue, daha verimli bir derlenmiş çıktı üretmek için şablonlardaki boşluk karakterlerini kaldırır veya sıkıştırır. Varsayılan strateji `"condense"` olup aşağıdaki davranışları içerir:

  1. Bir eleman içindeki baştaki ve sondaki boşluk karakterleri tek bir boşluğa indirgenir.
  2. Satır sonu içeren elemanlar arasındaki boşluk karakterleri kaldırılır.
  3. Metin düğümlerindeki ardışık boşluk karakterleri tek bir boşluğa indirgenir.

  Bu seçeneğin `'preserve'` olarak ayarlanması (2) ve (3) numaralı davranışları devre dışı bırakır.

- **Örnek**

  ```js
  app.config.compilerOptions.whitespace = 'preserve'
  ```

### app.config.compilerOptions.delimiters {#app-config-compileroptions-delimiters}

Şablon içindeki metin interpolasyonu için kullanılan ayraçları (delimiter) ayarlar.

- **Tip:** `[string, string]`

- **Varsayılan:** `{{ "['\u007b\u007b', '\u007d\u007d']" }}`

- **Detaylar**

  Bu genellikle mustache sözdizimini kullanan sunucu tarafı framework’lerle çakışmayı önlemek için kullanılır.

- **Örnek**

  ```js
  // Delimiters changed to ES6 template string style
  app.config.compilerOptions.delimiters = ['${', '}']
  ```

### app.config.compilerOptions.comments {#app-config-compileroptions-comments}

Şablonlardaki HTML yorumlarının (comment) nasıl ele alınacağını ayarlar.

- **Tür:** `boolean`

- **Varsayılan:** `false`

- **Ayrıntılar**

  Varsayılan olarak Vue, üretim ortamında yorumları kaldırır. Bu seçeneği `true` olarak ayarlamak, üretimde bile yorumların korunmasını sağlar. Yorumlar geliştirme sırasında her zaman korunur. Bu seçenek genellikle Vue’nun HTML yorumlarına dayanan diğer kütüphanelerle birlikte kullanıldığı durumlarda tercih edilir.

- **Örnek**

  ```js
  app.config.compilerOptions.comments = true
  ```

## app.config.globalProperties {#app-config-globalproperties}

Uygulama içindeki herhangi bir bileşen örneğinde erişilebilen genel (global) özellikleri kaydetmek için kullanılabilen bir nesnedir.

- **Tip**

  ```ts
  interface AppConfig {
    globalProperties: Record<string, any>
  }
  ```

- **Detaylar**

  Bu, Vue 2’deki `Vue.prototype`’ın Vue 3’te artık bulunmayan karşılığıdır. Tüm global yapılar gibi, dikkatli ve sınırlı şekilde kullanılmalıdır.

  Bir global özellik bir bileşenin kendi özelliğiyle çakışırsa, bileşenin kendi özelliği öncelikli olur.

- **Kullanım**

  ```js
  app.config.globalProperties.msg = 'hello'
  ```

  Bu, `msg` değişkenini uygulamadaki tüm bileşen şablonlarında ve her bileşen örneğinin `this` bağlamında erişilebilir hâle getirir:

  ```js
  export default {
    mounted() {
      console.log(this.msg) // 'hello'
    }
  }
  ```

- **Ayrıca bakınız** [Rehber – Global Özellikleri Genişletme](/guide/typescript/options-api#augmenting-global-properties) <sup class="vt-badge ts" />

## app.config.optionMergeStrategies {#app-config-optionmergestrategies}

Özel bileşen seçenekleri için birleştirme (merge) stratejilerini tanımlamak amacıyla kullanılan bir nesnedir.

- **Tip**

  ```ts
  interface AppConfig {
    optionMergeStrategies: Record<string, OptionMergeFunction>
  }

  type OptionMergeFunction = (to: unknown, from: unknown) => any
  ```

- **Detaylar**

  Bazı eklentiler / kütüphaneler, özel bileşen seçenekleri için destek ekler (global mixin’ler enjekte ederek). Bu seçenekler, aynı seçeneğin birden fazla kaynaktan (ör. mixin’ler veya bileşen kalıtımı) “birleştirilmesi” gerektiğinde özel bir birleştirme mantığı gerektirebilir.

  Bir özel seçenek için birleştirme stratejisi fonksiyonu, seçeneğin adı anahtar (key) olarak kullanılarak `app.config.optionMergeStrategies` nesnesine atanarak kaydedilebilir.

  Birleştirme stratejisi fonksiyonu, o seçeneğin üst (parent) ve alt (child) örneklerde tanımlanan değerlerini sırasıyla birinci ve ikinci argüman olarak alır.

- **Örnek**

  ```js
  const app = createApp({
    // option from self
    msg: 'Vue',
    // option from a mixin
    mixins: [
      {
        msg: 'Hello '
      }
    ],
    mounted() {
      // merged options exposed on this.$options
      console.log(this.$options.msg)
    }
  })

  // define a custom merge strategy for `msg`
  app.config.optionMergeStrategies.msg = (parent, child) => {
    return (parent || '') + (child || '')
  }

  app.mount('#app')
  // logs 'Hello Vue'
  ```

- **Ayrıca bakınız** [Bileşen Örneği – `$options`](/api/component-instance#options)

## app.config.idPrefix <sup class="vt-badge" data-text="3.5+" /> {#app-config-idprefix}

Bu uygulama içinde [useId()](/api/composition-api-helpers.html#useid) ile oluşturulan tüm ID’ler için bir ön ek (prefix) yapılandırır.

- **Tip:** `string`

- **Varsayılan:** `undefined`

- **Örnek**

  ```js
  app.config.idPrefix = 'myApp'
  ```

  ```js
  // in a component:
  const id1 = useId() // 'myApp:0'
  const id2 = useId() // 'myApp:1'
  ```

## app.config.throwUnhandledErrorInProduction <sup class="vt-badge" data-text="3.5+" /> {#app-config-throwunhandlederrorinproduction}

Üretim modunda yakalanmamış hataların fırlatılmasını (throw edilmesini) zorlar.

- **Tip:** `boolean`

- **Varsayılan:** `false`

- **Detaylar**

Varsayılan olarak, Vue uygulaması içinde fırlatılan ancak açıkça ele alınmayan hatalar, geliştirme ve üretim modlarında farklı şekilde davranır:

- Geliştirme modunda hata fırlatılır ve uygulamanın çökmesine neden olabilir. Bu, hatanın daha belirgin olmasını ve geliştirme sırasında fark edilip düzeltilmesini sağlamak içindir.

- Üretim modunda hata yalnızca konsola yazdırılır; böylece son kullanıcılar üzerindeki etki en aza indirilir. Ancak bu durum, yalnızca üretimde ortaya çıkan hataların hata izleme servisleri tarafından yakalanmasını engelleyebilir.

`app.config.throwUnhandledErrorInProduction` değeri `true` olarak ayarlandığında, yakalanmamış hatalar üretim modunda da fırlatılır.
