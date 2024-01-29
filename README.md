# h100-test
Environment: default
* `nvhpc/23.9` (with cuda 12.2)


## EXP1: cuda_spmmlib_eval
```
unzip cuda_spmmlib_eval
cd cuda_spmmlib_eval

./scripts/test_cuda_small.sh
./scripts/test_cuda_medium.sh
./scripts/test_cuda_large.sh
```

## EXP2: CLASP_graph

```
unzip CLASP_graph
cd CLASP_graph

rm -rf build && mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DCUDA_ARCHS="90" && make -j 12
```
* In `build/include/CLASP/CMakeFiles/spmm_benchmark_ve_amp.dir/link.txt`
    * remove `-lcublas -lcusparse`
* In `/build/src/CMakeFiles/benchmark_spmm.dir/link.txt`
    * remove `-lcublas -lcusparse` 
    * modify `/x/xshen5/h100-test` → `/xxx/xxxid/h100-test`
``` 
make -j 12

cd ../tmp
./scripts/test_cuda_small.sh 
./scripts/test_cuda_medium.sh
./scripts/test_cuda_large.sh
```

## EXP3: venom

```
unzip venom
cd venom

rm -rf build && mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DCUDA_ARCHS="90" && make -j 16

cd ../tmp
./scripts/test_venom_small.sh
./scripts/test_venom_medium.sh
./scripts/test_venom_large.sh
```