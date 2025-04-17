🔐 Performance Evaluation of AES and AVX Hardware Accelerators

This project investigates and benchmarks two critical hardware accelerators — AES (Advanced Encryption Standard)for cryptographic operations and AVX (Advanced Vector Extensions)for vector processing. The goal is to understand the impact of hardware acceleration on performance across different CPU architectures using benchmarking tools like OpenSSL and Gem5.


🧠 Abstract

Hardware accelerators significantly enhance the performance of compute-intensive operations by offloading them from the CPU. This project benchmarks:
- AES (cryptographic accelerator)
- AVX (vector instruction accelerator)

The results demonstrate how hardware acceleration reduces computational time and increases throughput, providing insights into CPU architecture support for these accelerators.


🔐 AES: Advanced Encryption Standard

AES is a symmetric encryption standard widely adopted for data security. In this study, AES is benchmarked with and without hardware acceleration on x86 and ARM architectures using:

⚒️ Benchmarking AES with OpenSSL

- Tool Used: `openssl speed -evp aes-128-cbc`
- Key Sizes Tested: 128, 192, 256 bits
- Encryption Modes: ECB, CBC, CFB, OFB, CTR
- `-evp` flag ensures use of hardware acceleration.

🧪 Results on x86 and ARM

- x86 (Intel Xeon) shows throughput increases up to 20x when hardware AES instructions are used.
- ARM (Cortex-A57)also demonstrates significant improvement, although slightly lower than x86.
- Performance depends on CPU clock, AES instruction set availability, and memory subsystem.

🧮 AVX: Advanced Vector Extensions

AVX accelerates vector and floating-point computations using SIMD (Single Instruction, Multiple Data) instructions.

🛠️ Simulating AVX using Gem5

- Simulator: Gem5 (with AVX extension support)
- AVX versions tested: AVX, AVX2, AVX-512
- CPUs tested:
  - Intel Core Ultra 5
  - Intel Core i7 11th Gen

🧪 AVX Workload and Results

```c
// AVX Vector Addition
__m256 vec_a = _mm256_load_ps(a);
__m256 vec_b = _mm256_load_ps(b);
__m256 vec_result = _mm256_add_ps(vec_a, vec_b);
```

- The performance in `sim_seconds` was reduced by more than 50% with AVX instructions enabled.
- AVX instructions resulted in significant SIMD utilization; none were used in non-AVX runs.

| CPU        | Sim Seconds (AVX) | Sim Seconds (No AVX) |
|------------|-------------------|---------------------- 
| Core Ultra 5 | 0.000201           | 0.000489          |
| Core i7      | 0.000201           | 0.000511          |

---

✅ Conclusion

- AES acceleration via the `-evp` OpenSSL flag boosts encryption throughput drastically.
- AVX instructions significantly reduce compute time for vector workloads.
- Both AES and AVX accelerators are critical in modern CPU architecture for achieving high performance in cryptography and data-parallel operations.

