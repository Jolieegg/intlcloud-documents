## Introduction

### Volume types

<table>
	<tr>
	<th>Volume Type</th><th>Description</th>
	</tr>
	<tr>
	<td>Use temporary path</td>
	<td>/</td>
	</tr>
	<tr>
	<td>Use host path</td>
	<td>Mount the file directory of the host where the container resides to the path specified by the container (corresponding to HostPath in Kubernetes). You can also choose not to set the source path (corresponding to EmptyDir in Kubernetes). If the source path is not specified, the system mounts the temporary directory of the assigned host to the mount target of the container.<b>Local disk volumes that have specified source paths are suitable for persisting data to the host where the container resides, whereas EmptyDir is suitable for temporary storage for containers.</b></td>
	</tr>
	<tr>
	<td>Use NFS disk</td>
	<td>Simply enter the NFS path. You can use Tencent Cloud's <a href="https://intl.cloud.tencent.com/document/product/582/9127">Cloud File Storage (CFS)</a> or user-built NFS file storage. <b>An NFS volume is suitable for persistent storage with frequent reads and writes in scenarios such as big data analysis, media processing, and content management.</b></td>
	</tr>
	<tr>
	<td>Use existing PersistentVolumeClaim</td>
	<td>Use the storage of the existing PersistentVolumeClaim to declare the storage for workloads, and automatically assign or create a PersistentVolume and mount it to the corresponding pod. This is suitable for stateful applications created by StatefulSet. </td>
	</tr>
	<tr>
	<td>Use ConfigMap</td>
	<td>A ConfigMap is mounted to a pod as a file system. You can mount the custom ConfigMap entries to a specific path. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/30675">ConfigMap Management</a>.</td>
	</tr>
	<tr>
	<td>Use Secret</td>
	<td>A Secret is mounted to a pod as a file system. You can mount custom Secret entries to a specific path. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/30676">Secret Management</a>.</td>
	</tr>
</table>




### Notes on volumes

- **After creating a volume, you need to set the mount target of the container in the "Containers in the Pod" module.**
- Under the same service, the name of the volume and the set mount target must be unique.
- When the source path of a local disk volume is empty, the system will assign a temporary directory `/var/lib/kubelet/pods/pod_name/volumes/kubernetes.io~empty-dir`, and the lifecycle of the volume using the temporary directory is the same as the lifecycle of the Pod.
- If no permission is set for volume mount, the default setting will be read/write permission.

## Operation Guide for Volumes in the Console
### Creating a workload to mount a volume

1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the cluster where you want to deploy a workload to go to the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
For example, select **Workload** -> **DaemonSet** to go to the DaemonSet page as shown in the following figure:
![](https://main.qcloudimg.com/raw/33e75aa3aab80d66c1dbcd4702cb564c.png)
4. Click **Create** to go to **Create Workload** page.
5. <span id="Step5"></span>Set the workload name, namespace and other information as instructed. In **Volume**, click **Add Volume**.
6. Select a storage method for the volume. **Use Tencent Cloud CBS** is selected in this case.
7. Configure the mount point in **Mount Target** under **Containers in the Pod**, as shown in the following figure:
You can configure the mount point only after selecting **Add Volume** in [Step 5](#Step5).
![](https://main.qcloudimg.com/raw/c3270454a7520ffac86c94917905012f.png)
8. Set other options as needed and click **Create Workload** to finish the creation.


### Configurations for mounting different volumes
This table shows the details of the use of different volumes. **When you are creating a workload and have selected **Add Volume**, you can refer to the following content to add the volume and set the mount point:

<table>
<thead>
        <tr>
            <th colspan="3" class="text-center salesInfoStyle">
                Volume
            </th>
            <th colspan="3" class="text-center dispositionStyle">
                Mount Target
            </th>
        </tr>
      <tr>
        <!-- <th style="position: relative;" [style.top]="columnTop"><span></span></th> -->
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span rtsort="del_order">Type</span></th>
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span rtsort="type">Name</span></th>
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span>Others</span></th>
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span rtsort="plant">Destination Path</span></th>
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span rtsort="customer">Sub-path</span></th>
        <th style="position: relative;" class="salesInfoStyle" [style.top]="columnTop"><span rtsort="shipto">Read and Write Permissions</span></th>
      </tr>
    </thead>
    <tbody><tr>
        <td>Temporary path</td><td rowspan="8">Custom</td><td>/</td><td rowspan="8">Specify this path as needed, for example, <code>/cache</code>.</td> <td rowspan="8">Mount only the sub-path or a single file in the selected volume, for example, <code>/data</code> or <code>/test.txt</code>.</td> <td rowspan="8">Select as needed. <li>Read-only: the container path volume can only be read and data modifications must be performed on the host.</li> <li>Read and write: data can be read from and modifications can be saved to the container path volume.</li></td>
    </tr>
    <tr>
        <td>Node path</td><td>Set the node path.<li>Node Path: the node path cannot be empty. For example, if the container needs to access Docker, the node path can be set to <code>/var/lib/docker</code>.</li><li>Check Type: TKE provides many check types such as NoChecks and DirectoryOrCreate. Read the description of each type in the console and select a check type as needed.</li></td>
    </tr>
    <tr>
        <td> NFS disk</td><td>NFS Path: enter the CFS address or user-built NFS address.<li>To create a file system, see <a herf="https://intl.cloud.tencent.com/document/product/582/9132">Creating File Systems and Mount Targets.</a></li><li><code>10.0.0.161:/</code> is an example NFS path. To obtain the NFS path, please log in to the <a href="https://console.cloud.tencent.com/cfs" target="_blank">CFS console</a>, click the ID of the target file system and find it in **Mount under Linux** on the **Mount Target Info** tab.</li></td>
    </tr>
    <tr>
        <td>Existing PVC</td><td>Choose a PVC as needed.</td>
    </tr>
    <tr>
        <td>ConfigMap</td><td rowspan="2"><li>Select a ConfigMap: select a ConfigMap as needed.</li> <li>Options: **All** and **Specific keys**.</li><li>Items: if you select **Specific keys**, you can mount it to a specific path by adding items. For example, if the mount point is <code>/data/config</code> and the sub-path is <code>dev</code>, the data will be stored under <code>/data/config/dev</code>.</li></td>
    </tr>
    <tr>
        <td>SECRET</td>
</tr></tbody></table>



## Using kubectl to Manipulate Volumes

The following is a sample where which you can perform creation by using kubectl directly.

### Sample YAML for Mounting a Volume to a Pod
```Yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir: {}
```
- **spec.volumes**: set the name, type, and parameters of the volume.
  - **spec.volumes.emptyDir**: set the temporary path
  - **spec.volumes.hostPath**: set the host path
  - **spec.volumes.nfs**: set the NFS disk
  - **spec.volumes.persistentVolumeClaim**: set the existing PersistentVolumeClaim.
- **spec.volumeClaimTemplates**: if this declaration is used, PersistentVolumeClaim and PersistentVolume will be automatically created based on the content of the declaration
- **spec.containers.volumeMounts**: enter the mount point of the volume.
