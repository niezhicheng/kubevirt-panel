# KubeVirt 面板

面向 KubeVirt 集群的 Web 管理面板。  
比 [kubevirt-manager](https://github.com/kubevirt-manager/kubevirt-manager) 更完整：虚拟机全生命周期 + **Kube-OVN 网络** + 存储镜像 + 运维迁移，一套界面搞定。

> 用镜像部署即可，无需自己编译源码。

---

## 快速部署（Docker Compose）

**依赖**：本机能访问目标 Kubernetes；集群已装 [KubeVirt](https://kubevirt.io/)；[Kube-OVN](https://github.com/kubeovn/kube-ovn) / Multus 可选（网络相关功能需要）。

```bash
git clone https://github.com/niezhicheng/kubevirt-panel.git
cd kubevirt-panel

# 可选：改 kubeconfig 路径或端口
cp .env.example .env

docker compose pull
docker compose up -d
```

浏览器打开：**http://localhost:8080**  
默认账号：`admin` / `admin123`（请尽快修改或仅用于内网试用）

停止：

```bash
docker compose down
```

### 镜像（阿里云 ACR · 河源）

| Tag | 说明 |
|-----|------|
| `web-latest` | 前端（Nginx，反代 `/api`） |
| `api-latest` | HTTP API |
| `virt-latest` | KubeVirt gRPC（需挂载 kubeconfig） |
| `ovn-latest` | Kube-OVN gRPC（需挂载 kubeconfig） |

完整地址：`registry.cn-heyuan.aliyuncs.com/yuanbuluo/kubevirt:<tag>`

### 常见问题

- **拉镜像失败**：确认能访问 `registry.cn-heyuan.aliyuncs.com`（国内网络一般可直连）。
- **面板能开但列表空 / 报错**：检查 `.env` 里 `KUBECONFIG_HOST` 是否指向有效 kubeconfig，且该凭证对目标集群有权限；容器内需能访问 apiserver 地址（若 kubeconfig 里是内网 IP，请在能路由到该网段的机器上跑 Compose）。
- **只要 VM、不用 OVN**：仍建议一起启动 `ovn` 服务（compose 已编排）；无 OVN 时相关菜单会不可用或报错，不影响纯虚拟机能力。

试用 / 部署问题加微信：**rz1433**

---

## 为什么不用 kubevirt-manager？

| | kubevirt-manager | **KubeVirt 面板** |
|--|--|--|
| 虚拟机创建 / 启停 / VNC | ✅ | ✅ |
| 硬件模板 / Preference | 有限 | ✅ Instancetype + Preference |
| Kube-OVN VPC / 子网 / NAD | ❌ | ✅ |
| EIP / SNAT / DNAT / FIP | ❌ | ✅ |
| PVC / DataVolume / 镜像导入 | 基础 | ✅ 含上传与模板 |
| 事件、告警、热迁移 | 弱 | ✅ 运维中心 |

适合已经在用（或准备用）**KubeVirt + Kube-OVN** 的环境，不想再为网络/存储另开一套工具。

---

## 能力概览

- **虚拟机**：列表、向导创建、详情、重启/暂停、VNC、YAML、资源关系  
- **网络**：VPC、子网、IP、安全组、NAD、QoS、EIP/SNAT/DNAT/FIP  
- **存储**：PVC、DataVolume、模板与镜像导入  
- **运维**：事件日志、告警、任务、热迁移  

---

## 界面预览

### 登录

![登录](images/01-login.png)

### 虚拟机列表

![虚拟机列表](images/02-virt-resources.png)

### 创建虚拟机

![创建虚拟机](images/08-create-vm-form.png)

### 虚拟机详情

![虚拟机详情](images/09-vm-detail.png)

### VPC / 基础网络

![VPC](images/03-kube-ovn-basic-net.png)

### 子网

![子网](images/10-kube-ovn-subnet.png)

### 云网络（EIP 等）

![云网络](images/04-kube-ovn-cloud-net.png)

### NAD / 高级网络

![NAD](images/05-kube-ovn-adv-net.png)

### 存储与 PVC

![存储](images/06-storage-center.png)

### 硬件模板

![模板](images/11-templates.png)

### 运维 · 事件

![运维](images/07-ops-center.png)

---

## 联系方式

微信 / 联系：**rz1433**

---

## 仓库说明

本仓库提供产品说明、界面截图与 **Docker Compose 部署文件**。  
业务源码不开源，通过容器镜像分发。
