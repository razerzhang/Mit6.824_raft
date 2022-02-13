# Mit6.824_raft
implement based on course of mit_6.824 and raft paper

##Mit 6.824

###2A leader election
Implement Raft leader election and heartbeats (AppendEntries RPCs with no log entries). The goal for Part 2A is for a single leader to be elected, for the leader to remain the leader if there are no failures, and for a new leader to take over if the old leader fails or if packets to/from the old leader are lost. Run go test -run 2A -race to test your 2A code.

实现Raft选择和心跳检查（通过no log entries的appendEntries RPCs），2A部分的目标是成功选举一个leader直到其发生错误，然后一个新的leader会取代其位置，通过`go test -run 2A -race to test` 检查代码。

### 分析
着重理解论文中figure 2

**状态**

所有服务器上持久性状态（相应RPCs前已经更新到稳定的存储设备）

currentTerm	服务器已知最新的任期（在服务器首次启动时初始化为0，单调递增）

votedFor	当前任期内收到选票的 candidateId，如果没有投给任何候选人 则为空

log[]	日志条目；每个条目包含了用于状态机的命令，以及领导人接收到该条目时的任期（初始索引为1）
