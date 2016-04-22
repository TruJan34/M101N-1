# Homework 6.3

Which of the following statements are true about choosing and using a shard key?

## Answer

* The shard key must be unique

No

* You can change the shard key on a collection if you desire.

No. hard keys are immutable and cannot be changed after insertion. See the system limits for sharded cluster for more information.

* There must be a index on the collection that starts with the shard key.

Yes. All sharded collections must have an index that starts with the shard key.

* MongoDB can not enforce unique indexes on a sharded collection other than the shard key itself, or indexes prefixed by the shard key.

Yes. For sharded collections these unique indexes cannot enforce uniqueness because insert and indexing operations are local to each shard.

* Any update that does not contain the shard key will be sent to all shards.

Yes. If a query does not include the shard key, the mongos must direct the query to all shards in the cluster.