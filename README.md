# kubevirt 云平台管理 — 产品界面预览

基于 **KubeVirt + Kube-OVN** 的虚拟化云管控制台界面截图。  
**源码不开源**；部署请使用构建好的容器镜像（计划发布至 Docker Hub / 阿里云容器镜像服务）。

默认演示账号：`admin`（密码部署时配置，不在此公开）。

---

## 功能一览

| 模块 | 说明 |
|------|------|
| 虚拟化资源 | 虚拟机列表、副本集、启停/重启/暂停、创建与详情 |
| 基础网络 | VPC / 子网 / IP / 安全组（Kube-OVN） |
| 云网络资源 | OVN EIP / SNAT / DNAT / FIP |
| 网络高级功能 | NAD、QoS 等 |
| 存储与镜像 | PVC、DataVolume、模板与镜像导入 |
| 运维中心 | 事件日志、告警、任务、热迁移 |

---

## 界面截图

### 1. 登录

![登录](images/01-login.png)

### 2. 虚拟化资源 · 虚拟机列表

![虚拟机列表](images/02-virt-resources.png)

### 3. 创建虚拟机

![创建虚拟机](images/08-create-vm-form.png)

### 4. 虚拟机详情

![虚拟机详情](images/09-vm-detail.png)

### 5. 基础网络 · VPC

![基础网络 VPC](images/03-kube-ovn-basic-net.png)

### 6. 子网

![子网](images/10-kube-ovn-subnet.png)

### 7. 云网络资源 · EIP

![云网络 EIP](images/04-kube-ovn-cloud-net.png)

### 8. 网络高级功能 · NAD

![NAD](images/05-kube-ovn-adv-net.png)

### 9. 存储与镜像 · PVC

![存储 PVC](images/06-storage-center.png)

### 10. 模板与镜像

![模板](images/11-templates.png)

### 11. 运维中心 · 事件与日志

![运维中心](images/07-ops-center.png)

---

## 获取与部署（镜像，非源码）

源码仓库不公开。对外分发方式：

- **Docker Hub**：`docker.io/<namespace>/kubevirt-admin:<tag>`（待发布）
- **阿里云 ACR**：`registry.cn-<region>.aliyuncs.com/<namespace>/kubevirt-admin:<tag>`（待发布）

拉取示例（镜像发布后可用）：

```bash
docker pull docker.io/<namespace>/kubevirt-admin:latest
# 或
docker pull registry.cn-hangzhou.aliyuncs.com/<namespace>/kubevirt-admin:latest
```

需已安装并可用：Kubernetes、KubeVirt、（可选）Kube-OVN / Multus。

---

## 说明

本仓库仅包含**产品截图与说明**，不含业务源码。  
截图拍摄于本地运行环境（`2026-10-21`），界面以实际部署版本为准。
