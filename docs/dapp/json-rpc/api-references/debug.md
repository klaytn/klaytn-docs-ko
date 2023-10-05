---
description: >-
  런타임 중 노드 상태와 블록체인 데이터를 검사하고 디버깅하는 API입니다.
---

# debug <a id="namespace-debug"></a>

`debug` namespace는 몇몇 비표준 RPC 메서드에 접근하여 런타임 중의 특정 디버깅 플래그를 검사, 디버깅, 설정하도록 합니다.

**NOTE** Some debug namespace APIs are unsafe/unappropriate to be opened to public. We recommend you to provide the debug namespace APIs to authorized users only. However, if you want to maintain a public EN and provide debug namespace APIs to the public, we strongly recommend you to set the `rpc.unsafe-debug.disable` flag which will disable APIs that are unsafe/unappropriate to be opened to the public and enable only a subset of the debug namespace APIs. The enabled APIs are as follows:
- [VM Tracing](./debug/tracing.md) APIs, however with limited functionality (only [pre-defined tracers](./debug/tracing.md#tracing-options) are allowed)
- debug_dumpBlock, debug_dumpStateTrie, debug_getBlockRlp, debug_getModifiedAccountsByHash, debug_getModifiedAccountsByNumber, debug_getBadBlocks, debug_getModifiedStorageNodesByNumber
- debug_metrics


## [로깅](./debug/logging.md) <a id="logging"></a>

- [debug_backtraceAt](./debug/logging.md#debug_backtraceat)
- [debug_setVMLogTarget](./debug/logging.md#debug_setvmlogtarget)
- [debug_verbosity](./debug/logging.md#debug_verbosity)
- [debug_verbosityByName](./debug/logging.md#debug_verbositybyname)
- [debug_verbosityByID](./debug/logging.md#debug_verbositybyid)
- [debug_vmodule](./debug/logging.md#debug_vmodule)


## [프로파일링](./debug/profile.md) <a id="profiling"></a>

- [debug_blockProfile](./debug/profile.md#debug_blockprofile)
- [debug_cpuProfile](./debug/profile.md#debug_cpuprofile)
- [debug_mutexProfile](./debug/profile.md#debug_mutexprofile)
- [debug_isPProfRunning](./debug/profile.md#debug_ispprofrunning)
- [debug_setBlockProfileRate](./debug/profile.md#debug_setblockprofilerate)
- [debug_startCPUProfile](./debug/profile.md#debug_startcpuprofile)
- [debug_stopCPUProfile](./debug/profile.md#debug_stopcpuprofile)
- [debug_startPProf](./debug/profile.md#debug_startpprof)
- [debug_stopPProf](./debug/profile.md#debug_stoppprof)
- [debug_writeBlockProfile](./debug/profile.md#debug_writeblockprofile)
- [debug_writeMemProfile](./debug/profile.md#debug_writememprofile)
- [debug_writeMutexProfile](./debug/profile.md#debug_writemutexprofile)


## [런타임 추적](./debug/go_trace.md) <a id="runtime-tracing"></a>

- [debug_goTrace](./debug/go_trace.md#debug_gotrace)
- [debug_startGoTrace](./debug/go_trace.md#debug_startgotrace)
- [debug_stopGoTrace](./debug/go_trace.md#debug_stopgotrace)


## [런타임 디버깅](./debug/runtime.md) <a id="runtime-debugging"></a>

- [debug_freeOSMemory](./debug/runtime.md#debug_freeosmemory)
- [debug_gcStats](./debug/runtime.md#debug_gcstats)
- [debug_memStats](./debug/runtime.md#debug_memstats)
- [debug_metrics](./debug/runtime.md#debug_metrics)
- [debug_setGCPercent](./debug/runtime.md#debug_setgcpercent)
- [debug_stacks](./debug/runtime.md#debug_stacks)


## [VM 추적](./debug/tracing.md) <a id="vm-tracing"></a>

- [debug_traceBadBlock](./debug/tracing.md#debug_tracebadblock)
- [debug_traceBlock](./debug/tracing.md#debug_traceblock)
- [debug_traceBlockByHash](./debug/tracing.md#debug_traceblockbyhash)
- [debug_traceBlockByNumber](./debug/tracing.md#debug_traceblockbynumber)
- [debug_traceBlockByNumberRange](./debug/tracing.md#debug_traceblockbynumberrange)
- [debug_traceBlockFromFile](./debug/tracing.md#debug_traceblockfromfile)
- [debug_traceTransaction](./debug/tracing.md#debug_tracetransaction)
- [debug_traceCall](./debug/tracing.md#debug_tracecall)
- [debug_traceChain](./debug/tracing.md#debug_tracechain)
- [Tracing Options](./debug/tracing.md#tracing-options)
- [JavaScript-based Tracing](./debug/tracing.md#javascript-based-tracing)


## [VM 표준 추적](./debug/standard_tracing.md) <a id="vm-standard-tracing"></a>

- [debug_standardTraceBadBlockToFile](./debug/standard_tracing.md#debug_standardtracebadblocktofile)
- [debug_standardTraceBlockToFile](./debug/standard_tracing.md#debug_standardtraceblocktofile)
- [Standard Tracing Options](./debug/standard_tracing.md#standard-tracing-options)


## [블록체인 검사](./debug/blockchain.md) <a id="blockchain-inspection"></a>

- [debug_dumpBlock](./debug/blockchain.md#debug_dumpblock)
- [debug_dumpStateTrie](./debug/blockchain.md#debug_dumpstatetrie)
- [debug_getBlockRlp](./debug/blockchain.md#debug_getblockrlp)
- [debug_getModifiedAccountsByHash](./debug/blockchain.md#debug_getmodifiedaccountsbyhash)
- [debug_getModifiedAccountsByNumber](./debug/blockchain.md#debug_getmodifiedaccountsbynumber)
- [debug_getBadBlocks](./debug/blockchain.md#debug_getbadblocks)
- [debug_preimage](./debug/blockchain.md#debug_preimage)
- [debug_printBlock](./debug/blockchain.md#debug_printblock)
- [debug_setHead](./debug/blockchain.md#debug_sethead)
- [debug_seedHash](./debug/blockchain.md#debug_seedhash)
- [debug_startWarmUp](./debug/blockchain.md#debug_startwarmup)
- [debug_startContractWarmUp](./debug/blockchain.md#debug_startcontractwarmup)
- [debug_stopWarmUp](./debug/blockchain.md#debug_stopwarmup)
- [debug_startCollectingTrieStats](./debug/blockchain.md#debug_startCollectingTrieStats)

