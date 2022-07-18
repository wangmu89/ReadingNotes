指标（Metrics）

Metrics are a numeric representation of data measured over intervals of time. Metrics can harness the power of mathematical modeling and prediction to derive knowledge of the behavior of a system over intervals of time in the present and future.

度量是在时间间隔内测量的数据的数字表示。 度量可以利用数学建模和预测的力量来获取系统在当前和未来一段时间内的行为知识。

Since numbers are optimized for storage, processing, compression, and retrieval, metrics enable longer retention of data as well as easier querying. This makes metrics perfectly suited to building dashboards that reflect historical trends. Metrics also allow for gradual reduction of data resolution. After a certain period of time, data can be aggregated into daily or weekly frequency.

由于数字针对存储、处理、压缩和检索进行了优化，因此指标可以延长数据的保留时间以及更轻松的查询。 这使得指标非常适合构建反映历史趋势的仪表板。 指标还允许逐渐降低数据分辨率。 一段时间后，可以将数据聚合为每日或每周频率。

指标度量的剖析





指标相比事件日志的优势

基于指标的监控相比基于日志的监控优势

- 与日志的生成和存储不同，指标传输和保存具有恒定的开销。
- 与日志不同，指标成本不会随着用户流量或任何其他可能导致数据急剧上升的系统活动同步增加。
- 使用指标，应用程序流量的增加不会像日志那样导致磁盘利用率、处理复杂性、可视化速度和运营成本的显着增加。
- 度量存储随着标签值的更多排列组合而增加（例如，当更多主机或容器启动时，或者当添加新服务或现有服务得到更多检测时），但客户端聚合可以确保指标流量的增加不会与用户流量成正比。

> Prometheus 等系统的客户端库在进程中聚合时间序列样本，并在成功抓取时将它们提交给 Prometheus 服务器（默认情况下每隔几秒发生一次，并且可以配置）。这与每次将指标记录到 statsd 守护程序时发送 UDP 数据包的 statsd 客户端不同（导致提交给 statsd 的指标数量与报告的流量成正比增加！）

度量一旦收集起来，就更容易适应数学、概率和统计转换，例如采样、聚合、汇总和相关性。这些特征使指标更适合报告系统的整体健康状况。

> Metrics are also better suited to trigger alerts, since running queries against an in-memory, time-series database is far more efficient, not to mention more reliable, than running a query against a distributed system like Elasticsearch and then aggregating the results before deciding if an alert needs to be triggered. Of course, systems that strictly query only in-memory structured event data for alerting might be a little less expensive than Elasticsearch. The downside here is that the operational overhead of running a large, clustered, in-memory database, even if it were open source, isn’t something worth the operational trouble for most organizations, especially when there are far easier ways to derive equally actionable alerts. Metrics are best suited to furnish this information.

指标也更适合触发警报，因为对内存中的时间序列数据库运行查询比对像 Elasticsearch 这样的分布式系统运行查询然后在决定之前聚合结果要高效得多，更不用说更可靠了 如果需要触发警报。

指标也更适合触发警报，因为对内存中的时间序列数据库运行查询比对像 Elasticsearch 这样的分布式系统运行查询然后在决定之前聚合结果要高效得多，更不用说更可靠了 如果需要触发警报。 当然，严格只查询内存中结构化事件数据以发出警报的系统可能比 Elasticsearch 便宜一些。 这里的缺点是运行大型集群内存数据库的操作开销，即使它是开源的，对于大多数组织来说，操作上的麻烦并不值得，特别是当有更简单的方法来获得同样可操作的 警报。 指标最适合提供此信息。

指标度量的缺点

- 应用程序日志和应用程序指标的最大缺点是它们是系统范围的，除了特定系统内部发生的事情之外，很难理解其他任何事情。 当然，指标也可以在请求范围内，但这需要伴随标签输出（fan-out）的增加，从而导致指标存储的增加。
- 对于没有花哨连接的日志，单行并不能提供关于跨系统所有组件的请求发生了什么的太多信息。虽然可以构建一个跨地址空间或 RPC 边界关联指标和日志的系统，但此类系统需要一个指标来携带 UID 作为标签。
- 使用像 UID 这样的高基数值作为度量标签可能会使时间序列数据库不堪重负。 尽管新的 Prometheus 存储引擎已针对处理时间序列流失进行了优化，但较长时间范围的查询仍然会很慢。 普罗米修斯只是一个例子。 所有流行的现有时间序列数据库解决方案在高基数标记下都会受到影响。
- 当使用最佳时，日志和指标可以让我们完全无所不知地进入一个孤岛，但仅此而已。 虽然这些可能足以理解单个系统的性能和行为，包括有状态和无状态的，但它们不足以理解遍历多个系统的请求的生命周期。
- 分布式跟踪是一种解决跨多个系统的请求生命周期可见性问题的技术。
