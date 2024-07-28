# Kubernetes 101

* [Nedir?](#nedir)
    * [Temel Özellikleri](#temel-ozellikleri)
    * [Nasıl Çalışır?](#nasil-calisir)
    * [Kullanım Senaryoları](#kullanim-senaryolari)
* [Yararları](#yararlari)
* [Minikube Nedir?](#minikube-nedir)
    * [Minikube Temel Özellikleri](#minikube-temel-ozellikler)
    * [Kullanım Senaryoları](#kullanim-senaryolari)
* [kubeadm  Nedir?](#kubeadm-nedir)
    * [Kubeadm Özellikleri ve İşlevleri](#kubeadm-ozellikleri-ve-islevleri)
    * [Kubeadm Kurulumu](#kullanim-kurulumu)
* [Minikube VS kubeadm](#minikube-vs-kubeadm)
    * [Minikube](#minikube)
    * [Kubeadm](#kubeadm)
    * [Karar Verme](#karar-verme)
* [Kurulum](#kurulum)
* [Kubernates Temel Bileşemler](#kubernates-temel-bilesenler)
    * [coredns](#coredns)
    * [etcd](#etcd)
    * [kube-apiserver](#kube-apiserver)
    * [kube-controller-manager](#kube-controller-manager)
    * [kube-proxy](#kube-proxy)
    * [kube-scheduler](#kube-scheduler)
    * [storage-provisioner](#storage-provisioner)
    * [vpnkit-controller](#vpnkit-controller)
    * [Bu Temel Servisleri Yönetmem Gerekir Mi?](#bu-temel-servisleri-yönetmem-gerekir-mi)
    * [Kubernetes Sistem Bileşenlerinin Yönetimi](#kubernetes-sistem-bileşenlerinin-yönetimi)
    * [Ne Zaman İletişime Geçilir?](#ne-zaman-etkileşime-geçilir)
* [Ek Bilgiler](#ek-bilgiler)
   * [GitOps](#gitops)


## Nedir?

Kubernetes, genellikle k8s olarak kısaltılır ve Google tarafından başlatılan, daha sonra Linux Foundation tarafından yürütülen Cloud Native Computing Foundation (CNCF) tarafından desteklenen açık kaynaklı bir konteyner orkestrasyon platformudur. Kubernetes, 2014 yılında piyasaya sürüldü ve konteyner teknolojilerini kullanarak uygulamaların otomatik dağıtımı, ölçeklendirilmesi ve yönetilmesini sağlamak için tasarlanmıştır.

### Temel Özellikleri
1. **Otomatik paketleme**: Kubernetes, sunucu veya küme kaynaklarını en verimli şekilde kullanmak için konteynerleri otomatik olarak yerleştirir.
2. **Otomatik iyileştirme**: Hatalı veya yanıt vermeyen konteynerleri yeniden başlatır ve kullanıcı tanımlı sağlık kontrollerine dayalı olarak konteynerleri değiştirir.
3. **Yüksek erişilebilirlik ve ölçeklenebilirlik**: Uygulamaları isteğe bağlı olarak ölçeklendirme ve yüksek erişilebilirlik sağlar.
4. **Hizmet keşfi ve yük dengeleme**: Kubernetes, bir DNS adı veya kendi IP adresleri ile servisleri bulmayı ve yük dengelemeyi otomatik olarak yapabilir.

### Nasıl Çalışır?
Kubernetes mimarisi, bir dizi bağımsız, dağıtılmış bileşenden oluşur. En temel yapı taşlarından bazıları şunlardır:
- **Pod**: Kubernetes'teki en küçük dağıtım birimi, bir veya daha fazla konteyneri içerebilir.
- **Node**: Pod'ların çalıştığı fiziksel veya sanal makineler.
- **Cluster**: Node'ları içeren ve uygulamaların çalıştığı daha geniş yapı.
- **Master**: Kümenin koordinasyonunu sağlayan, planlama ve yönetim işlemleri için kullanılan node veya node grubu.

### Kullanım Senaryoları
- **Mikroservis mimarileri**: Bağımsız mikroservislerin dağıtımı ve yönetimi için idealdir.
- **DevOps ve sürekli entegrasyon/deployment (CI/CD)**: Uygulama geliştirme ve dağıtım süreçlerini otomatikleştirme.
- **Büyük veri ve analitik**: Kaynak yoğun iş yüklerinin dinamik ölçeklendirilmesi.

Kubernetes, modern yazılım geliştirme ve dağıtım süreçlerinde esneklik ve ölçeklenebilirlik sağlar, bu yüzden popülerliği her geçen gün artmaktadır. Konteyner teknolojisiyle çalışmak için güçlü bir temel sağlar.

## Yararları

Kubernetes, modern yazılım geliştirme ve altyapı yönetiminde önemli bir role sahip olan kapsamlı bir konteyner orkestrasyon aracıdır. İşletmelerin ve geliştiricilerin tercih ettiği bir çözüm olmasının birçok nedeni vardır. İşte Kubernetes'in sağladığı bazı önemli yararlar:

### 1. **Otomatik Ölçeklendirme**
Kubernetes, uygulama trafiği arttığında veya azaldığında otomatik olarak konteyner sayısını artırabilir veya azaltabilir. Bu, kaynak kullanımını optimize eder ve kullanıcı deneyimini iyileştirir.

### 2. **Yüksek Kullanılabilirlik ve Hata Toleransı**
Kubernetes, uygulamaları farklı makineler üzerinde çalışacak şekilde otomatik olarak dağıtarak tek noktadan arıza riskini azaltır. Bir node çökerse, Kubernetes otomatik olarak diğer node'lar üzerinde yeni pod'lar başlatır, böylece uygulamanın sürekli çalışmasını sağlar.

### 3. **Kaynak Kullanımı ve Maliyet Optimizasyonu**
Kubernetes, node'lar üzerindeki kaynakları (CPU ve bellek gibi) etkin bir şekilde yönetir. Uygulamalarınız için gereksiz kaynak tahsisi yapmadan, ihtiyaç duyulan kaynakları dinamik olarak ayarlayarak maliyetleri düşürür.

### 4. **Taşınabilirlik ve Platform Bağımsızlık**
Kubernetes, çeşitli bulut sağlayıcılarında (AWS, Google Cloud, Azure vb.) ve kendi sunucularınızda çalışabilir. Bu, uygulamalarınızı farklı altyapılarda kolayca taşımanıza ve bulut bağımlılığını azaltmanıza olanak tanır.

### 5. **DevOps ve Agile Entegrasyonu**
Kubernetes, sürekli entegrasyon ve sürekli dağıtım (CI/CD) süreçlerini destekler, bu da geliştirme ve operasyon ekipleri arasındaki işbirliğini artırır ve yazılım teslimat süreçlerini hızlandırır.

### 6. **Kendi Kendini İyileştirme Özellikleri**
Kubernetes, başarısız konteynerleri otomatik olarak yeniden başlatır, sağlıksız node'ları değiştirir ve kullanıcı tanımlı sağlık kontrollerine göre servisleri sürdürür.

### 7. **Servis Keşfi ve Yük Dengeleme**
Kubernetes, servisler arası iletişim için otomatik IP adresi ataması ve DNS adı yönetimi sağlar. Yük dengeleyiciler kullanarak gelen trafiği pod'lar arasında otomatik olarak dağıtır, bu da sistem performansını artırır.

### 8. **Yapılandırma Yönetimi ve Gizlilik**
Kubernetes, `ConfigMaps` ve `Secrets` ile uygulama yapılandırmalarını ve hassas verileri yönetir. Bu, uygulama kodundan yapılandırma bilgilerini ayırmanızı ve güvenlik standartlarına uygun bir şekilde hassas verileri saklamanızı sağlar.

### 9. **Genişletilebilirlik**
Kubernetes, çeşitli eklentiler ve araçlar ile genişletilebilir. İhtiyaçlarınıza özel işlevler ekleyebilir, mevcut iş akışlarınıza entegre edebilirsiniz.

Kubernetes'in bu yararları, onu büyük ölçekli ve karmaşık uygulama ortamlarını yönetmek için ideal bir araç haline getirir ve günümüzün dinamik ve çevik yazılım geliştirme gereksinimlerine cevap verir.

## Minikube Nedir?

Minikube, Kubernetes öğrenmek, geliştirmek ve test etmek isteyenler için tasarlanmış yerel bir Kubernetes ortamı sağlayan bir araçtır. Tek bir node'lu bir Kubernetes kümesi olarak çalışır ve bir masaüstü ya da dizüstü bilgisayar gibi tek bir makinede tüm Kubernetes bileşenlerini çalıştırabilir. Minikube, Kubernetes'in çekirdek işlevlerini ve API'lerini yerel olarak deneyimlemek isteyen geliştiriciler için idealdir.

### Minikube Temel Özellikleri

1. **Basit Kurulum**: Minikube, Linux, macOS ve Windows dahil olmak üzere çeşitli işletim sistemlerine kolayca kurulabilir. Bu, birkaç dakika içinde yerel bir Kubernetes ortamı hazırlamanıza olanak tanır.

2. **Hafif Ortam**: Minikube, Kubernetes'i öğrenmek ve test etmek için gerekli minimum kaynakları kullanarak çalışır. Bu, kaynakları kısıtlı makinelerde bile Kubernetes deneyimini mümkün kılar.

3. **Entegre Sanallaştırma Desteği**: Minikube, VirtualBox, VMware Fusion, HyperKit (Mac), Hyper-V (Windows), KVM (Linux) ve Docker gibi birçok sanallaştırma platformunu destekler. Kullanıcıların tercih ettiği sanallaştırma teknolojisini kullanmasına olanak tanır.

4. **Add-on Yönetimi**: Minikube, Kubernetes özelliklerini genişletmek için çeşitli add-on’ları kolayca yönetmenizi ve kullanmanızı sağlar. Örneğin, Ingress, metrics-server, istio ve daha fazlasını kolayca etkinleştirebilirsiniz.

5. **Geliştirme Dostu**: Minikube, yerel geliştirme süreçlerine uyum sağlar. `minikube start` komutu ile kümeniz çalışmaya başlar ve `minikube stop` ile durdurabilirsiniz. Ayrıca, Docker daemon ile entegrasyon sayesinde Docker image'larınızı doğrudan Minikube ortamına build edebilirsiniz.

6. **Dashboard Desteği**: Minikube, Kubernetes Dashboard'u entegre bir şekilde sunar, bu da küme kaynaklarınızı görsel olarak yönetmenizi ve izlemenizi sağlar.

### Kullanım Senaryoları
Minikube, özellikle şu durumlar için tercih edilir:
- **Öğrenme ve Eğitim**: Kubernetes'in temel kavramlarını ve işleyişini öğrenmek için mükemmel bir ortamdır.
- **Geliştirme ve Test**: Uygulamalarınızı Kubernetes üzerinde geliştirirken, yerel bir ortamda hızlı iterasyon ve test yapmanızı sağlar.
- **Demo ve Prototipleme**: Yeni fikirleri veya projeleri hızlı bir şekilde prototiplemek ve göstermek için kullanılır.

Minikube, Kubernetes ekosisteminde önemli bir araç olarak, başlangıç seviyesinden ileri seviyeye kadar kullanıcıların Kubernetes dünyasına adım atmasını kolaylaştırır.

## kubeadm  Nedir?

`kubeadm` Kubernetes tarafından sağlanan bir araçtır ve Kubernetes kümesi oluşturmak, yapılandırmak ve yönetmek için kullanılır. Kubernetes'i hızlı ve kolay bir şekilde kurmanıza olanak tanır. Özellikle Kubernetes'in temel bileşenlerini (API sunucusu, Controller Manager, Scheduler ve etcd gibi) başlatmak, çalıştırmak ve düzenli bir şekilde dağıtmak için tasarlanmıştır. `kubeadm` genellikle üretim seviyesindeki kümeler için bir başlangıç noktası olarak kullanılır ve gelişmiş yapılandırma seçenekleri sunar.

### Kubeadm Özellikleri ve İşlevleri

1. **Kolay Kurulum ve Yapılandırma**: `kubeadm init` ve `kubeadm join` komutları, bir Kubernetes master node'unu hızlıca başlatmanıza ve işçi node'larını (worker nodes) kümeye eklemenize olanak tanır. Bu komutlar, güvenlik ve ağ yapılandırmalarını otomatik olarak ele alır.

2. **Sertifika Yönetimi**: `kubeadm` otomatik olarak Kubernetes için gerekli olan TLS sertifikalarını oluşturur ve yönetir. Bu sertifikalar, küme bileşenleri arasında güvenli iletişim kurulmasını sağlar.

3. **Konfigürasyon Dosyaları**: `kubeadm` kullanıcıların, küme için gelişmiş yapılandırma seçeneklerini özelleştirebilecekleri bir yapılandırma dosyası üzerinden çalışmasına olanak tanır. Bu yapılandırma dosyası, küme bileşenlerinin davranışlarını detaylı bir şekilde kontrol etmenizi sağlar.

4. **Kubernetes Sürüm Yükseltme**: `kubeadm upgrade` komutu ile Kubernetes kümenizin sürümünü kolayca yükseltebilirsiniz. Bu işlem, Kubernetes bileşenlerinin yeni sürümlerine geçiş yapılmasını yönetir ve bu süreçte sertifika ve yapılandırma dosyalarını güncel tutar.

5. **Bağlantı ve Kontrol**: `kubeadm` tarafından oluşturulan kümeler, standart Kubernetes API'leri üzerinden yönetilir ve `kubectl` gibi araçlarla kolayca kontrol edilebilir.

### Kubeadm Kurulumu
Kubeadm'i kurmak için, resmi Kubernetes dökümantasyonundaki adımları takip edebilirsiniz. Genellikle Linux dağıtımlarında paket yöneticileri (apt, yum vb.) aracılığıyla kurulum yapılır. Kurulumdan sonra, `kubeadm init` komutu ile bir master node başlatılır ve çıktı olarak verilen `kubeadm join` komutu, diğer node'ların bu kümeyle nasıl birleşeceğini belirtir.

Kubeadm, Kubernetes ekosistemindeki en değerli araçlardan biridir ve Kubernetes kümesi yönetimini basitleştirerek, daha geniş bir kullanıcı kitlesinin Kubernetes'i benimsemesini teşvik eder. Özellikle, küme yönetimi ve orkestrasyon süreçlerinde standartlaşmayı sağlamak adına büyük kolaylık sunar.

## Minikube VS kubeadm

`Minikube` ve `kubeadm` arasında seçim yaparken, her ikisinin de farklı kullanım amaçlarına ve senaryolara hizmet ettiğini anlamak önemlidir. İkisi arasındaki temel farklar, kullanım kolaylıkları, ölçeklenebilirlikleri ve hedef kitleleri ile ilgilidir. Aşağıda her iki aracın özelliklerini ve kullanım senaryolarını karşılaştıralım:

### Minikube

1. **Amaç**: Minikube, Kubernetes öğrenmek ve yerel olarak uygulama geliştirmek için tasarlanmıştır. Tek bir node üzerinde çalışır ve Kubernetes'in tüm temel özelliklerini bir bilgisayarda deneyimlemenizi sağlar.

2. **Kurulum**: Minikube kurulumu oldukça basittir. Çeşitli işletim sistemlerinde tek bir komutla veya birkaç adımla kurulabilir.

3. **Kaynak Kullanımı**: Minikube, kaynak kullanımı açısından hafif tasarlanmıştır; küçük ölçekli ve az kaynak tüketen projeler için idealdir.

4. **Kullanıcı Kitlesi**: Yeni başlayanlar, öğrenciler ve geliştiriciler için uygun bir araçtır. Küçük denemeler ve öğrenme süreçleri için mükemmeldir.

5. **Özellikler**: Yerel geliştirme için yeterli özellikleri sunar, ancak üretim ortamları için gereken yüksek erişilebilirlik, yük dengesi ve ölçeklenebilirlik gibi özelliklerden yoksundur.

### Kubeadm

1. **Amaç**: `kubeadm`, üretim düzeyinde Kubernetes kümeleri kurmak ve yönetmek için kullanılır. Kubernetes'in tüm bileşenlerini başlatmak, yapılandırmak ve güncellemek için gerekli araçları sağlar.

2. **Kurulum**: `kubeadm` ile küme kurulumu, biraz daha teknik bilgi gerektirebilir. Birden fazla node'un kurulumu ve yönetimi söz konusu olduğunda, daha detaylı yapılandırmalar gerekir.

3. **Kaynak Kullanımı**: `kubeadm` ile kurulan kümeler, genellikle daha fazla kaynak tüketir çünkü birden fazla node ve daha kompleks yapılandırmalar desteklenir.

4. **Kullanıcı Kitlesi**: Sistem yöneticileri, DevOps profesyonelleri ve Kubernetes'i üretim ortamında kullanmayı hedefleyen kuruluşlar için idealdir.

5. **Özellikler**: Yüksek erişilebilirlik, yük dengesi, ölçeklenebilirlik ve güvenlik gibi üretim gereksinimlerini destekler. `kubeadm`, kompleks küme yapılandırmalarını ve güncellemeleri yönetebilir.

### Karar Verme

- **Eğer amacınız Kubernetes öğrenmek ve basit uygulamalar geliştirmekse, `Minikube` ideal bir seçimdir. (bizim öyle :))**
- Üretim ortamında kullanılmak üzere ölçeklenebilir, güvenilir ve yönetilebilir bir Kubernetes ortamı kurmayı planlıyorsanız, `kubeadm` daha uygun bir araçtır.

Her iki araç da Kubernetes ekosisteminde önemli bir yer tutar ve kullanıcıların ihtiyaçlarına göre farklı avantajlar sunar.

## Kurulum

Minikube, yerel bir Kubernetes kümesi kurmak ve test etmek için popüler bir seçenektir. Geliştirme ve öğrenme amaçları için mükemmeldir. İşte Minikube ile Kubernetes kurulumunun adım adım anlatımı:

### Adım 1: Gereksinimlerin Kontrolü
Minikube'u kurmadan önce, bilgisayarınızın aşağıdaki gereksinimleri karşıladığından emin olun:
- 2 CPU veya daha fazlası
- 2GB fiziksel RAM (4GB veya daha fazla önerilir)
- 20GB disk alanı
- İnternet bağlantısı
- VT-x veya AMD-v gibi donanım tabanlı sanallaştırma desteği

### Adım 2: Minikube Kurulumu
1. **Minikube İndirme**: Minikube'un en son sürümünü [Minikube resmi sitesinden](https://minikube.sigs.k8s.io/docs/start/) indirin.
   
2. **Kurulum**: İndirdiğiniz dosyaya uygun kurulum adımlarını takip edin. Windows için bir .exe dosyası, macOS ve Linux içinse bir komut dosyası olabilir. Örnek bir Linux kurulum komutu:

   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```

### Adım 3: Kubectl Kurulumu
`kubectl` komut satırı aracı, Kubernetes kümenizi yönetmenizi sağlar. Aşağıdaki adımlarla kurulum yapabilirsiniz:

1. **Kubectl İndirme**:
   
   ```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   ```

2. **Kubectl'ı Yürütülebilir Yapma**:

   ```bash
   chmod +x ./kubectl
   ```

3. **Kubectl'ı Sisteme Ekleme**:

   ```bash
   sudo mv ./kubectl /usr/local/bin/kubectl
   ```

4. **Versiyon Kontrolü ile Doğrulama**:

   ```bash
   kubectl version --client
   ```

### Adım 4: Minikube Başlatma
Minikube'u başlatmak için aşağıdaki komutu kullanın:

```bash
minikube start
```

Bu komut, varsayılan sürücü ile yerel bir Kubernetes kümesi oluşturur. Sürücü olarak VirtualBox, VMware, HyperKit gibi seçenekler kullanılabilir, ancak Minikube otomatik olarak en uygun olanı seçer.

### Adım 5: Küme Durumunu Kontrol Etme
Kümenizin başarıyla çalışıp çalışmadığını kontrol etmek için:

```bash
kubectl get nodes
```

Bu komut, kümedeki node'ları listeler ve sağlık durumlarını gösterir.

### Adım 6: Minikube Duraklatma, Durdurma veya Silme
Minikube'u duraklatmak, durdurmak veya tamamen silmek için aşağıdaki komutları kullanabilirsiniz:

- **Duraklatma**:
  
  ```bash
  minikube pause
  ```

- **Durdurma**:

  ```bash
  minikube stop
  ```

- **Silme**:

  ```bash
  minikube delete
  ```

Bu adımlarla, Minikube üzerinde bir Kubernetes kümesini başarıyla kurabilir ve yönetebilirsiniz. Bu ortam, Kubernetes özelliklerini öğrenmek ve geliştirme testleri yapmak için idealdir.

## Kubernates Temel Bileşenler

| Namespace    | Pod Name                                    | Ready | Status  | Restarts | Age |
|--------------|---------------------------------------------|-------|---------|----------|-----|
| kube-system  | coredns-76f75df574-xkvlz                     | 1/1   | Running | 0        | 24s |
| kube-system  | coredns-76f75df574-xn469                     | 1/1   | Running | 0        | 24s |
| kube-system  | etcd-docker-desktop                          | 1/1   | Running | 0        | 24s |
| kube-system  | kube-apiserver-docker-desktop                | 1/1   | Running | 0        | 21s |
| kube-system  | kube-controller-manager-docker-desktop       | 1/1   | Running | 0        | 28s |
| kube-system  | kube-proxy-5kfwn                             | 1/1   | Running | 0        | 24s |
| kube-system  | kube-scheduler-docker-desktop                | 1/1   | Running | 0        | 29s |
| kube-system  | storage-provisioner                          | 1/1   | Running | 0        | 22s |
| kube-system  | vpnkit-controller                            | 1/1   | Running | 0        | 22s |


### coredns
Kubernetes kümesindeki tüm isim çözümleme (DNS) isteklerini yöneten bir servistir. CoreDNS, servis adlarından IP adreslerine çözümleme yapar, bu da pod’lar arasındaki iletişimin ve servislerin bulunabilirliğinin sağlanmasında kritik bir role sahiptir. Çoğu kümede yüksek kullanılabilirlik için birden fazla CoreDNS kopyası çalışır.

### etcd
Dağıtık bir anahtar-değer veritabanıdır. Kubernetes’in tüm yapılandırma verilerini ve durumunu saklar. Kubernetes’in “beyni” olarak düşünülebilir. Küme üzerinde yapılan her türlü değişiklik etcd’de saklanır.

### kube-apiserver
Kubernetes API’sinin merkezi bileşenidir. Tüm Kubernetes komutları ve işlemleri, bu API sunucusu üzerinden gerçekleştirilir. Güvenlik, erişim kontrolü ve veri doğrulama gibi işlemleri yönetir.

### kube-controller-manager
Kubernetes’in çeşitli kontrol döngülerini (controller loops) çalıştıran bileşendir. Bu kontrol döngüleri, sistem durumunu sürekli olarak istenen durumla karşılaştırır ve gerekli düzeltmeleri yapar. Örneğin, çalışması gereken pod sayısı ile gerçekte çalışan pod sayısını karşılaştırır ve fark varsa yeni pod’lar başlatır.

### kube-proxy
Her Kubernetes node’unda çalışır ve pod’ların dış dünya ile iletişim kurabilmesi için ağ yönlendirmelerini sağlar. Ayrıca, içerideki servisler arası iletişimi de yönetir ve yük dengelendirme işlemlerini gerçekleştirir.

### kube-scheduler
Kubernetes’de yeni oluşturulan pod’ların hangi node’lara yerleştirileceğine karar veren bileşendir. Pod’ların gereksinimlerini, kaynak kullanılabilirliğini ve diğer kısıtları dikkate alarak en uygun node’u seçer.

### Storage Provisioner
Dinamik olarak depolama alanı sağlamakla görevlidir. Örneğin, bir PersistentVolumeClaim (PVC) yapıldığında, bu bileşen otomatik olarak bir PersistentVolume (PV) oluşturur ve bu talebi karşılar.

### Vpnkit Controller
Özellikle Docker Desktop’ın macOS ve Windows sürümlerinde, konteynerlerin ve Kubernetes pod’larının ana makine ile güvenli bir şekilde iletişim kurmasını sağlayan bir ağ köprüsüdür.

### Bu Temel Servisleri Yönetmem Gerekir Mi?
Listelenen Kubernetes sistem bileşenleri ve servisleri, Kubernetes kümesinin temel işlevselliğini sağlamak için otomatik olarak yönetilir ve çalıştırılır. Bu bileşenler, kümenin sağlıklı ve işlevsel kalmasını sağlamak için gereklidir. Ancak, günlük uygulama geliştirme ve yönetimi sırasında, bir kullanıcı olarak bu bileşenlerle doğrudan etkileşimde bulunmanız genellikle gerekmez. İşte bazı detaylar:

### Kubernetes Sistem Bileşenlerinin Yönetimi

1. **Otomatik Yönetim**: Kubernetes, `kube-apiserver`, `kube-scheduler`, `kube-controller-manager` gibi çekirdek bileşenleri otomatik olarak yönetir. Bu sistem bileşenleri, pod'ların planlanması, sağlık durumunun izlenmesi ve ağ politikalarının uygulanması gibi görevleri yerine getirir.

2. **Kullanıcı Etkileşimi**: Geliştiriciler ve sistem yöneticileri genellikle uygulama seviyesindeki kaynaklarla (örneğin, Deployment'lar, Service'ler, ConfigMaps) etkileşimde bulunurlar. `kubectl` ve diğer API çağrıları aracılığıyla bu kaynaklar üzerinde işlemler gerçekleştirilir.

3. **CoreDNS**: Kubernetes içindeki DNS çözünürlüğünü yönetir. Uygulama bileşenleriniz arasında isimle erişim gerektiğinde bu servis devreye girer, fakat günlük kullanımda bu servisin yönetimiyle ilgilenmeniz gerekmez.

4. **Etcd**: Kubernetes'in dağıtılmış veritabanıdır ve tüm küme verilerini saklar. Etcd'nin yedeğini almak ve izlemek gibi bazı ileri düzey operasyonlar dışında, etcd ile doğrudan etkileşimde bulunmanız genellikle gerekmez.

5. **Kube-proxy ve Networking**: Kube-proxy, Kubernetes ağ kurallarını işler ve containerlar arası ağ iletişimini sağlar. Ağ politikaları ve güvenlik grupları gibi konfigürasyonlarla ilgilenirken bu bileşenin varlığını bilmek önemlidir.

### Ne Zaman Etkileşime Geçilir?

- **Sorun Giderme ve Optimizasyon**: Eğer kümenizde performans sorunları veya hatalar meydana gelirse, bu sistem bileşenlerinin loglarına ve metriklerine bakmanız gerekebilir. Örneğin, yavaş yanıtlar veya planlama hataları için `kube-scheduler`'ın logları incelenebilir.
- **Güvenlik ve Yapılandırma Değişiklikleri**: Küme güvenliğini artırmak veya yapılandırmaları değiştirmek gibi ileri düzey değişiklikler yaparken, bu sistem bileşenlerinin konfigürasyonlarına müdahale etmeniz gerekebilir.

Genel olarak, Kubernetes'in sistem bileşenleri küme yönetimi tarafından otomatik olarak kontrol edilir ve bu, kullanıcıların bu bileşenlerle doğrudan etkileşimde bulunmasını azaltır. Ancak, ileri düzey küme yönetimi, performans optimizasyonu ve sorun giderme durumlarında bu bileşenlerin nasıl çalıştığını anlamak önemlidir.

## Ek Bilgiler

### GitOps

**GitOps**, yazılım geliştirme ve operasyon süreçlerini yönetmek için Git sürüm kontrol sistemini temel alan bir metodolojidir. GitOps, altyapının ve uygulama yapılandırmalarının kod olarak yönetilmesi (Infrastructure as Code) fikrini genişleterek, Git reposunu tek kaynak (single source of truth) olarak kullanır. Bu yaklaşım, otomasyon, yorumlanabilirlik ve kolaboratif çalışmayı teşvik eder.

### GitOps'un Temel Özellikleri

1. **Değişikliklerin Git Üzerinden Yönetilmesi**: Tüm altyapı ve uygulama yapılandırmaları bir Git reposunda tutulur. Değişiklik yapmak istediğinizde, Git üzerinden pull request (PR) açılır, inceleme ve onay sürecinden geçer, ve merge edilir. Bu süreç, değişikliklerin izlenebilir ve denetlenebilir olmasını sağlar.

2. **Otomasyon**: GitOps, sürekli entegrasyon (CI) ve sürekli dağıtım (CD) araçları ile entegre çalışır. Yapılandırma değişiklikleri Git'e push edildiğinde, otomatik olarak üretim ortamına veya hedef ortama uygulanır. Bu, manuel müdahaleyi azaltır ve hızlı geri dönüşler sağlar.

3. **Eşzamanlılık ve Senkronizasyon**: GitOps araçları, altyapının sürekli olarak Git reposundaki durumla eşzamanlı olmasını sağlar. Eğer canlı sistemde manuel bir değişiklik yapılırsa, bu değişiklikler ya geri alınır ya da uygun şekilde repo'ya yansıtılır.

4. **Güvenlik ve Uyumluluk**: Değişikliklerin merkezi bir yerden yönetilmesi ve tüm değişikliklerin izlenebilir olması, güvenlik ve uyumluluk gereksinimleri için büyük avantajlar sağlar. Ayrıca, kritik yapılandırma değişikliklerinin kod inceleme süreçlerinden geçmesi güvenliği artırır.

### GitOps Araçları

GitOps uygulamalarında kullanılan popüler araçlar şunları içerir:

- **Argo CD**: Kubernetes için tasarlanmış bir GitOps sürekli dağıtım aracıdır. Git reposundaki yapılandırmaları otomatik olarak Kubernetes kümelerine uygular.
- **Flux**: Kubernetes kaynaklarının otomatik hale getirilmesi ve yönetilmesi için kullanılan bir araçtır. Git reposundaki değişiklikleri takip eder ve gerekli güncellemeleri otomatik olarak uygular.
- **Jenkins X**: Kubernetes için özel olarak geliştirilmiş, GitOps ve sürekli dağıtımı destekleyen bir CI/CD çözümüdür.

### GitOps'un Avantajları

- **Hız ve Verimlilik**: Yapılandırma değişikliklerinin hızlı ve tutarlı bir şekilde uygulanması, geliştirme süreçlerini hızlandırır.
- **Daha Az Hata**: Otomasyon, insan kaynaklı hataları azaltır.
- **Kolay Geri Alma**: Git, tüm geçmişi sakladığı için yapılandırmalarda bir sorun oluştuğunda eski sürümlere hızla geri dönülebilir.
- **Geliştirilmiş Güvenlik ve Uyumluluk**: Her değişiklik kaydedilir ve denetlenebilir, bu da güvenlik ve regülasyonlara uyumu kolaylaştırır.

GitOps, modern yazılım geliştirme pratikleri arasında önemli bir yer tutar ve altyapı yönetimini daha güvenli, verimli ve şeffaf hale getirir.