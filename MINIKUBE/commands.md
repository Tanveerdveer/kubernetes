## Step 1) Apply updates:


## Command:<a id="command"></a>

```
sudo apt update -y
sudo apt upgrade -y
```

## Step 2) Install Minikube dependencies:<a id="step-2-install-minikube-dependencies"></a>

## Command:<a id="command-1"></a>

```
sudo apt install -y curl wget apt-transport-https
```


##  Step 3) Download Minikube Binary:<a id="step-3-download-minikube-binary"></a>

## Command:<a id="command-2"></a>

```
wget https\://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
 

Once the binary is downloaded copy it to the path /usr/local/bin and set the executable permissions on it


## Command:<a id="command-3"></a>
```
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
```

```
sudo chmod +x /usr/local/bin/minikube
```

Verify the minikube version


## Command:<a id="command-4"></a>

```
minikube version
```

Output:

minikube version: v1.29.0

commit: ddac20b4b34a9c8c857fc602203b6ba2679794d3


## Step 4) Install Kubectl utility<a id="step-4-install-kubectl-utility"></a>

Kubectl is a command line utility which is used to interact with the Kubernetes cluster. It is used for managing deployments, service and pods etc. Use the curl command to download the latest version of kubectl.


## Command:<a id="command-5"></a>

```
curl -LO https\://storage.googleapis.com/kubernetes-release/release/\`curl -s https\://storage.googleapis.com/kubernetes-release/release/stable.txt\`/bin/linux/amd64/kubectl
```

Once kubectl is downloaded then set the executable permissions on kubectl binary and move it to the path /usr/local/bin.


## Command:<a id="command-6"></a>

```
chmod +x kubectl
```

```
sudo mv kubectl /usr/local/bin/
```

Now verify the kubectl version:


## Command:<a id="command-7"></a>

```
kubectl version -o yaml
```

**Output:**

clientVersion:

  buildDate: "2023-01-18T15:58:16Z"

  compiler: gc

  gitCommit: 8f94681cd294aa8cfd3407b8191f6c70214973a4

  gitTreeState: clean

  gitVersion: v1.26.1

  goVersion: go1.19.5

  major: "1"

  minor: "26"

  platform: linux/amd64

kustomizeVersion: v4.5.7


## Step 5) Start minikube:<a id="step-5-start-minikube"></a>

## Command:<a id="command-8"></a>

```
minikube start
```

In case you want to start minikube with customize resources and want installer to automatically select the driver then you can run following command,


## Command:<a id="command-9"></a>
```
minikube start --addons=ingress --cpus=2 --cni=flannel --install-addons=true --kubernetes-version=stable --memory=6g
```
**Output:**

😄  minikube v1.29.0 on Ubuntu 22.04

✨  Automatically selected the kvm2 driver. Other choices: qemu2, none, ssh

💾  Downloading driver docker-machine-driver-kvm2:

    > docker-machine-driver-kvm2-...:  65 B / 65 B \[---------] 100.00% ? p/s 0s

    > docker-machine-driver-kvm2-...:  12.30 MiB / 12.30 MiB  100.00% 2.45 MiB 

💿  Downloading VM boot image ...

    > minikube-v1.29.0-amd64.iso....:  65 B / 65 B \[---------] 100.00% ? p/s 0s

    > minikube-v1.29.0-amd64.iso:  276.35 MiB / 276.35 MiB  100.00% 10.08 MiB p

👍  Starting control plane node minikube in cluster minikube

💾  Downloading Kubernetes v1.26.1 preload ...

    > preloaded-images-k8s-v18-v1...:  397.05 MiB / 397.05 MiB  100.00% 10.18 M

🔥  Creating kvm2 VM (CPUs=2, Memory=2200MB, Disk=20000MB) ...

🐳  Preparing Kubernetes v1.26.1 on Docker 20.10.23 ...

    ▪ Generating certificates and keys ...

    ▪ Booting up control plane ...

    ▪ Configuring RBAC rules ...

🔗  Configuring bridge CNI (Container Networking Interface) ...

    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5

🔎  Verifying Kubernetes components...

🌟  Enabled addons: default-storageclass, storage-provisioner

🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

Run below minikube command to check status,


## Command:<a id="command-10"></a>
```
    minikube status
```
**Output:**

minikube

type: Control Plane

host: Running

kubelet: Running

apiserver: Running

kubeconfig: Configured


## Command:<a id="command-11"></a>
```
kubectl cluster-info
```
**Output:**

Kubernetes control plane is running at https\://192.168.39.196:8443

CoreDNS is running at https\://192.168.39.196:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.


## Command:<a id="command-12"></a>
```
kubectl get nodes
```
**Output:**

NAME       STATUS   ROLES           AGE   VERSION

minikube   Ready    control-plane   73m   v1.26.1


## Step 6) Managing Addons on minikube<a id="step-6-managing-addons-on-minikube"></a>

## Command:<a id="command-13"></a>
```
minikube addons list
```
**Output**:

\|-----------------------------|----------|--------------|--------------------------------|

\|         ADDON NAME          | PROFILE  |    STATUS    |           MAINTAINER           |

\|-----------------------------|----------|--------------|--------------------------------|

\| ambassador                  | minikube | disabled     | 3rd party (Ambassador)         |

\| auto-pause                  | minikube | disabled     | Google                         |

\| cloud-spanner               | minikube | disabled     | Google                         |

\| csi-hostpath-driver         | minikube | disabled     | Kubernetes                     |

\| dashboard                   | minikube | disabled     | Kubernetes                     |

\| default-storageclass        | minikube | enabled ✅   | Kubernetes                     |

\| efk                         | minikube | disabled     | 3rd party (Elastic)            |

\| freshpod                    | minikube | disabled     | Google                         |

\| gcp-auth                    | minikube | disabled     | Google                         |

\| gvisor                      | minikube | disabled     | Google                         |

\| headlamp                    | minikube | disabled     | 3rd party (kinvolk.io)         |

\| helm-tiller                 | minikube | disabled     | 3rd party (Helm)               |

\| inaccel                     | minikube | disabled     | 3rd party (InAccel             |

\|                             |          |              | \[info\@inaccel.com])            |

\| ingress                     | minikube | disabled     | Kubernetes                     |

\| ingress-dns                 | minikube | disabled     | Google                         |

\| istio                       | minikube | disabled     | 3rd party (Istio)              |

\| istio-provisioner           | minikube | disabled     | 3rd party (Istio)              |

\| kong                        | minikube | disabled     | 3rd party (Kong HQ)            |

\| kubevirt                    | minikube | disabled     | 3rd party (KubeVirt)           |

\| logviewer                   | minikube | disabled     | 3rd party (unknown)            |

\| metallb                     | minikube | disabled     | 3rd party (MetalLB)            |

\| metrics-server              | minikube | disabled     | Kubernetes                     |

\| nvidia-driver-installer     | minikube | disabled     | Google                         |

\| nvidia-gpu-device-plugin    | minikube | disabled     | 3rd party (Nvidia)             |

\| olm                         | minikube | disabled     | 3rd party (Operator Framework) |

\| pod-security-policy         | minikube | disabled     | 3rd party (unknown)            |

\| portainer                   | minikube | disabled     | 3rd party (Portainer.io)       |

\| registry                    | minikube | disabled     | Google                         |

\| registry-aliases            | minikube | disabled     | 3rd party (unknown)            |

\| registry-creds              | minikube | disabled     | 3rd party (UPMC Enterprises)   |

\| storage-provisioner         | minikube | enabled ✅   | Google                         |

\| storage-provisioner-gluster | minikube | disabled     | 3rd party (Gluster)            |

\| volumesnapshots             | minikube | disabled     | Kubernetes                     |

\|-----------------------------|----------|--------------|--------------------------------|

Let’s assume we want to enable and access kubernetes dashboard.


## Command:<a id="command-14"></a>
```
 minikube dashboard
```
**Output:**

 ![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcbhOsjit0lhVJ9l7mcv8UpuUNxBBWcNSO8jnqvhaLWAszbX1exL_4LX0_rUb64gUWp8n_APTWIjKAEKrWiQTZt-QZxAWTtTSYx5VAE4xcUrc3QM1MjcaYwm_LIlMQ3A7XtxgjOI70bRXQNtk0ymSNktv3v?key=Gfh5yd9lEvdYsgkp3UCezw)
