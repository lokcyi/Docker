---
icon: qq
---

# Docker & Kubernetes

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="188"><figcaption></figcaption></figure>

Docker本身並不是容器，它本身是一個能創建容器的工具，故`Build(搭建), Ship(運送) and Run(執行)`是重要的流程步驟。

`Build once，Run anywhere`(搭建一次，隨處可用)，則是上述流程的優勢特性，完全符合現代化懶人的需求。\


上述故事放入背包中的鏡像就是Docker Image。

而背包本身就是Docker Repository。

最後在新找的空地上用口令變出的民宿就是一個Docker Container。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

一旦民宿數量日益增多龐大時，開始就會混亂，無論是客戶入住，金流物資房型等一坨拉古鬼一般的需求蜂擁而來，這時候如何能好好和平共處，在一個良善的編寫排定調度管理讓這一個個的民宿能夠永續經營。所以K8S的到來，它的全名就是Kubernetes。

一個基於容器的集群管理平台

如果真要比較 Kubernetes 與 Docker，其實應該是就特性來說`Kubernetes與Docker Swarm`。

Kubernetes與Docker最基本差異是，K8s是在整個叢集內執行，而Docker則是在單一節點上執行。

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
