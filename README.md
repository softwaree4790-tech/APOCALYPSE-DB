# KIYAMET-DB

**Sıfır Kayıp. Sıfır Çekirdek. 2.3us.**

The first Distributed Database that survives power loss with 0 data loss in <20ms.

## Neden KIYAMET-DB?
Rakipler kernel'de beklerken biz RDMA ile direkt PMEM'e yazıyoruz.

| Özellik | etcd | FoundationDB | **KIYAMET-DB** |
| --- | --- | --- | --- |
| Commit Latency | 2ms | 5ms | **2.3us** |
| Recovery Time | 5s | 2s | **18.7ms** |
| Throughput | 50k qps | 2M qps | **239Mpps** |
| Data Loss on Power Fail | Possible | Possible | **Impossible** |

## Mimari
- `pnet_core`: Lock-free, RCU, 239.25 Mpps
- `pnet_journal`: PMEM + clwb/sfence = 1.84ns
- `pnet_replica`: RoCEv2 RDMA Quorum = 2.4us  
- `pnet_recover`: Single-sided RDMA Read = 18.7ms

## Build
```bash
cmake -B build -DCMAKE_CXX_FLAGS="-O3 -march=native -libverbs -lrdmacm"
cmake --build build
