# hibernate use ehcahce as second-level cache on standalone service #

*org.hibernate.cache.spi.RegionFactory* 定义了hibernate与具体缓存实现的服务接口
*hibernate.cache.region.factory_class* 定义具体的接口服务商，hibernate内置了两种流行的缓存框架（ehcache与infinispan）

hibernate 缓存接口开发也遵循了常见的SPI（service provider interface）机制，只是面向接口编程，具体的服务通过加载机制来实现，实现进行可插拔，实现模块之间的解耦。常见的spi实现方式有log日志，数据库数据源

## configuration parameters ##

    hibernate.cache.use_second_level_cache: true/false #是否开通二级缓存
    hibernate.cache.use_query_cache: true/false #是否开通二级查询缓存
    hibernate.cache.region.factory_class: class #spi provider class 
    hibernate.cache.query_cache_factory: class #org.hibernate.cache.spi.QueryCacheFactory implementation 默认是不允许访问陈旧数据的，一般不扩展此配置
    hibernate.cache.use_minimal_puts: true/false #读写优化，最小化写，更多的读操作。
    hibernate.cache.region_prefix: String #所有的region前缀
    hiberante.cache.default_cache_concurrency_strategy: read-only/read-write/nonstrict-read-write/transactional 一般不进行配置，因为每个provider有自己默认的strategy
    hibernate.cache.use_structured_entries: true/false #是否开启结构化实体，主要是便于查看缓存数据，不过会带来性能开销
    hibernate.cache.auto_evict_collection_cache: true/false #当双向关联中的Owning方（即多方）变化时自动将缓存中关联的集合剔除
    hibernate.cache.use_reference_entries: true/false #允许直接使用二级缓存中的read-only或者不变数据
    hibernate.cacke.keys_factory: default/simply/org.hibernate.cache.spi.CacheKyesFactory implemetations,暂时只有Infinispan支持

## org.hibernate.annotations.cache ##