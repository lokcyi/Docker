---
description: >-
  Docker Client 本身並不直接支援多人同時登入和使用。Docker Client
  主要設計為單一使用者使用，每個使用者通常會使用自己的帳戶和權限來與 Docker Daemon 互動。
icon: head-side-brain
---

# Docker

## 雖然 Docker Client 不直接支援多人登入，但您可以透過以下方式來實現多人同時使用 Docker：

* **使用不同的使用者帳戶：**
  * 每個使用者可以使用自己的 Windows 帳戶登入到 Windows Server 2025。
  * 每個使用者都可以在自己的帳戶下安裝和配置 Docker Client。
  * 這樣每個使用者都擁有自己的 Docker Client 環境，彼此之間不會互相影響。
* **使用遠端 Docker Daemon：**
  * 您可以設定一個遠端的 Docker Daemon，讓多個使用者透過 Docker Client 連接到同一個 Daemon。
  * 這樣可以實現多人共享同一個 Docker 環境，但需要注意權限管理和資源分配。
* **使用容器編排工具：**
  * 如果您需要管理大量的容器，可以考慮使用容器編排工具，例如 Docker Swarm 或 Kubernetes。
  * 這些工具提供了更完善的權限管理和資源分配機制，可以更好地支持多人協作。

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

**Docker Image（映像檔）：**

Docker 映像檔是一個輕量級的、獨立的、可執行的軟體包，包含了執行應用程式所需要的一切，包括程式碼、運行環境、函式庫、環境變數和設定文件等等。由於映像檔包含了應用運行所需的全部相依套件，這使得您可以在任何 Docker 環境上一致地運行您的應用。Docker 映像檔可以透過 Dockerfile 來建立，也可以透過 Docker Hub 或其他 Docker Registry 下載。

**Docker Container（容器）：**

Docker 容器(container)是 Docker 映像檔(image)的一個執行實例。當透過 `docker run` 指令啟動一個映像檔時，該映像檔就會成為一個活動的容器。每一個容器都是從映像檔建立的，而且是完全獨立的，它有獨立的檔案系統、網路接口和進程空間等等。可以在一台主機上同時運行多個容器，它們之間彼此隔離，但又可以透過特定的方式進行互動。

**Docker Daemon：**

Docker Daemon 是一個持續運行的後臺進程，用於管理 Docker 容器。當作業系統開啟 Docker Desktop 或者運行 Docker 時。就能透過 `docker` 指令來建立、運行、或管理容器時，實際上是 Docker Daemon 在幕後處理這些任務。

例如，當執行 `docker run` 時，Docker Daemon 會找到或者下載適當的映像檔，創建新的容器，並且分配資源給它。Docker Daemon 也負責監控、日誌記錄、網路配置等等。

### Docker 常見指令

* `docker run <image>`：從映像檔建立並啟動一個新的容器。
* `docker ps`：列出正在運行的容器。
* `docker stop <container>`：停止一個容器。
* `docker ps -a` ：列出所有容器，包含停止的容器。
* `docker rm <container>`：移除一個容器。
* `docker images`：列出本地的所有映像檔。
* `docker rmi <image>`：移除一個映像檔。
* `docker pull <image>`：從 Docker Hub 或其他 Docker Registry 下載一個映像檔。
* `docker build -t <image> .`：從當前目錄的 Dockerfile 建立一個新的映像檔。
* `docker exec -it <container> bash`：進入一個正在運行的容器的 bash shell。
* `docker run -d -p 8080:3000 <image名稱:tag>` ：在背景運行
