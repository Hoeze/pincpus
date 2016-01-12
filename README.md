作用：
===
根据配置文件定义的CG，将ceph-osd进程均匀分配到CG中。
使用方法：
===
在prz-pincpus.conf配置文件中定义好CG的数量及各个CG对应的CPU、NUMA_ID，拷贝到/etc/目录下后，执行pincpus。
验证：
===
top，按F选择'P','CGROUPS'，观察ceph-osd进程所在CPU
注意：
===
* 未关闭NUMA的情况下，各个CPU对应的NUMA不一样。如果将进程限制到不同NUMA的CPU上，可能会造成内存访问延迟变长。
* CPU的每个CORE都有自己的独立L1-L2缓存，每个SOCKET有独立的L3缓存，为了更好的利用缓存，尽量将相同CORE下的CPU绑定到同一个CG上。
* 限制CPU时，预留好每个OSD进程的用量，防止由于计算能力不足拖慢CEPH集群。
