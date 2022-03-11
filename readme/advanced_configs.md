## Advanced Configs

### Advanced Params

There are `9` modules params for tools.  Introductions as below:

- EC2_VPC_PARAMS: These params of the module are for creating a VPC.

- EC2_RDS_PARAMS: These params of the module are for creating an RDS.

- EC2_STATIC_SERVICES_PARAMS: These params of the module are for creating a Prometheus Server and other static services.

- EC2_ZOOKEEPERS_PARAMS: These params of the module are for creating a Zookeeper Cluster.

- EC2_SPARK_MASTER_PARAMS: These params of the module are for creating a Spark Master node.

- EC2_KYLIN4_PARAMS: These params of the module are for creating a Kylin4.

- EC2_SPARK_WORKER_PARAMS: These params of the module are for creating **Spark Workers**, the default is **3** spark workers for all clusters.

- EC2_KYLIN4_SCALE_PARAMS: these params of the module are for scaling **Kylin4 nodes**, the range of **Kylin4 nodes** is related to `KYLIN_SCALE_UP_NODES` and `KYLIN_SCALE_DOWN_NODES`.

  > Note:
  >
  > 1. `KYLIN_SCALE_UP_NODES` is for the range of Kylin nodes to scale up. 
  > 2. `KYLIN_SCALE_DOWN_NODES` is for the range of Kylin nodes to scale down.
  > 3. The range of `KYLIN_SCALE_UP_NODES` must contain the range of `KYLIN_SCALE_DOWN_NODES`.
  > 4. **They are effective to all clusters which are not only `default cluster` but also another cluster whose index is in `${CLUSTER_INDEXES}`.**

- EC2_SPARK_SCALE_SLAVE_PARAMS: these params of the module are for scaling **Spark workers**, the range of **Spark Workers is related to `SPARK_WORKER_SCALE_UP_NODES` and `SPARK_WORKER_SCALE_DOWN_NODES`.

  > Note:
  >
  > 1. `SPARK_WORKER_SCALE_UP_NODES` is for the range for spark workers to scale up. **It's effective to all clusters which are not only `default cluster` but also another cluster whose index is in `${CLUSTER_INDEXES}`.**
  > 2. `SPARK_WORKER_SCALE_DOWN_NODES` is for the range for spark workers to scale down. **It's effective to all clusters which are not only `default cluster` but also another cluster whose index is in `${CLUSTER_INDEXES}`.**
  > 3. The range of `SPARK_WORKER_SCALE_UP_NODES` must contain the range of `SPARK_WORKER_SCALE_DOWN_NODES`.
  > 4. **They are effective to all clusters which are not only `default cluster` but also another cluster whose index is in `${CLUSTER_INDEXES}`.**

### Customize Configs

User also can customize the params in `kylin_configs.yaml` to create an expected instance. Such as **the type of instance**, **the volume size of the instance** and **the volume type of instance,** and so on.

1. If you want to customize configs for instances, you must modify the `EC2Mode` from `test` to `product` in `kylin_configs.yml`.
2. `Ec2Mode` is only in the parms of `EC2_STATIC_SERVICES_PARAMS`, `EC2_ZOOKEEPERS_PARAMS`, `EC2_SPARK_MASTER_PARAMS`, `EC2_KYLIN4_PARAMS`, `EC2_SPARK_WORKER_PARAMS`, `EC2_KYLIN4_SCALE_PARAMS` and `EC2_SPARK_SCALE_SLAVE_PARAMS`.
3. So instances can be customized to effect `Monitor Node`(`EC2_STATIC_SERVICES_PARAMS`), `Zookeeper Nodes`(`EC2_ZOOKEEPERS_PARAMS`), `Spark Master Node` ( `EC2_SPARK_MASTER_PARAMS`), `Kylin4 Node`( `EC2_KYLIN4_PARAMS`), `Spark workers `(`EC2_SPARK_WORKER_PARAMS`), `Kylin4 scale nodes`(`EC2_KYLIN4_SCALE_PARAMS`) and `Spark scale workers`(`EC2_SPARK_SCALE_SLAVE_PARAMS`).
4. Now`Ec2Mode` **only effect** the related params are `Ec2InstanceTypeFor*`,`Ec2VolumeSizeFor*`  and `Ec2VolumnTypeFor`* in the params modules.
5. If you don't change `ENABLE_LOCAL_CACHE_SOFT_AFFINITY` from `"false"` to `"true"` then the cluster will be created normally without the `Local Cache + Soft Affinity` feature!

#### Example

As an example in `EC2_STATIC_SERVICES_PARAMS`:

- change `Ec2Mode` from `test` to `product`.
- change `Ec2InstanceTypeForStaticServices`  from `m5.2xlarge` to `m5.4xlarge`.
- change `Ec2VolumeSizeForStaticServicesNode`  from `'20'` to `'50'`.
- change `Ec2VolumnTypeForStaticServicesNode` from `gp2` to `standard`.
- Then create the node of static service node will be an `m5.4xlarge` and it attaches a volume which size is `50` and type is `standard`.

![static service params](../images/staticserviceparam.png)