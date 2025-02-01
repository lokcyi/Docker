# Kubernetes 簡介 背景知識

首先來看官方網站的一段簡短介紹：

> [Kubernetes](https://kubernetes.io/docs/concepts/overview/), also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.
>
> 中文：Kubernetes 又稱為 K8s，是個開源系統，用來自動部署、擴展、和管理容器應用程式。

簡單來說，K8s 能夠讓我們以宣告的方式來定義**叢集**（cluster）的狀態。

{% hint style="info" %}
**叢集（Cluster）**:由 Kubernetes 管理的一群節點，這些節點通常會運行一些容器化應用程式。多數情況下，叢集中的節點並不會公開暴露於網際網路。
{% endhint %}

我們可以用一個純文字檔案來描述你想要以怎樣的配置來運行整個系統（內容通常以 yaml 語法編寫），而 K8s 就會依照檔案中的指示來進行調配，以確保整體環境符合我們期望的狀態。這便是 K8s 能替我們做的事。

## Master Node、Worker Node、Cluster <a href="#master-nodeworker-nodecluster" id="master-nodeworker-nodecluster"></a>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



## Pod <a href="#pod" id="pod"></a>

接著來看另一個重要的元件：Pod。

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Pod 是容器的 host，也是配置與部署的最小單位，因為我們（DevOps 工程師）在 K8s 叢集中配置或部署的對象都是 Pods，而不是直接去處理容器。

由此可見，Pod 就像是一個抽象層，裡面包覆著容器。你也可以把 Pod 理解成一個箱子，而這個箱子裡面裝著容器。實務上比較常見的情形是一個 Pod 裡面只裝載一個容器，但也可以裝載多個容器。

\
（Pods）彼此之間要如何溝通呢？它們需要倚賴 K8s 叢集裡面的另一個基礎元件：**虛擬網路**（virtual network）。

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

剛才提過，我們並不會直接去處理 K8s 叢集當中的容器，而是對 Pods 來進行相關操作。

一旦 pod 當中的某個容器故障了，或者完全停擺，我們也須介入，因為 Pod 當中的容器將會自動重啟。

那麼，如果是 Pod 本身掛掉呢？此時 K8s 會替那個掛掉的 Pod 再建立一個新的執行個體。

每當一個新的 Pod 被建立起來，它就會有一個新的 IP 位址，這會造成一些困擾。舉例來說，假設有一個 Pod A 是提供資料庫伺服器的功能，而其他 Pods 是透過 IP 位址來存取 Pod A 的資料庫，那麼每當 Pod A 因為故障而重新建立，IP 位址隨之改變，就會導致其他 Pods 無法存取資料庫。針對這種情形，我們必須認識 K8s 的另一個元件：Service。

### Service <a href="#service" id="service"></a>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

這裡的 Service 並非平常泛指的軟體服務，而是 Kubernetes 用來協助 **Pods 之間彼此溝通的連接機制**。

我們可以想像每個 Pod 都連接了一 個 Service 來當作對外聯繫的窗口，故彼此不再需要倚賴 Pod 的 IP 位址，而是透過這些服務來進行溝通。Service 和 Pod 之間的關係，是有點黏而又不太黏的——意思是二者之間雖有連結，但生命週期並不相同。

當某個 Pod 因為故障而重新建立並獲取新的IP位址，原先與之相連的那個 Service 並不會消失或重建，而是持續存在。於是，各 Pod 之間透過這些 Services 來當作聯繫窗口，即使某個 Pod 因為故障而頻繁重建，也不會因為 IP 位址變更而令系統停擺。

<mark style="color:blue;">**與 Pod 類似，Kubernetes 也會給每一個 Service 指派一個 IP 位址，只是派給 Service 的 IP 位址是固定的，不像 Pods 那樣很容易因為重建而頻繁變動 IP 位址**</mark>。

然而，如果你的應用程式會以 HTTP 協定的方式提供外部存取，我們當然不希望用戶端以類似 `http://10.20.152.3:8080` 的位址來存取應用程式的服務，而會希望提供更友善的網址，例如 `https://my-app.xyz.com`，這個部份則是由 Kubernetes 的另一個元件來處理：Ingress。

當外界要存取 Kubernetes 叢集中的應用程式服 務時，**Ingress 會負責將來自外部的請求（通常是 HTTP 或 HTTPS 請求）轉介至對應的目標服務**。其運作方式可參考下圖：

![](https://huanlin.cc/docs/devops/k8s/overview/k8s-ingress.png)

