# Bladebit2
An improved version of the Chia Bladebit plotter and harvester.

This repo incudes a plotter `bladebit_cuda` that supports compression levels up to 12, and a harvester component embedded in `ProofOfSpace` that takes about 1/9 of the time to find a proof and finds 5% more proofs compared to the official software `ProofOfSpaceOfficial` compiled with timing enabled on Ubuntu 20.04.

To verify the result, first make a plot with the following parameters:
```
./bladebit_cuda -n 1  --compress 7 -i 824871870ead30e476ea73701a189d061141455c7a9b9761671b19c74306514f \
			-f b866264a2bcefe5f42ea5b267703f72e3f93e211c0af66e24beaf91bd21edcea49f75775f676db3e4828c9aab92d96c5 \
			-p b85077391c9384fbc4d448dd78dbb4b1e7f48c85f8519483d80a1b9cac4ce4d2f33e970fc20596ca2358aeafa3594567 \
			cudaplot -d 0 ./
```
These parameters are chosen for no others reason than the fact that they are the ones I initially randomly chose for testing while developing the software. Other parameters should give very similar results. The GPU used was NVIDIA GeForce RTX 3070.

After plotting, run the following command to test the improved version of `ProofOfSpace`:
```
./ProofOfSpace check -f ./plot-k32-c07-2024-03-07-00-36-824871870ead30e476ea73701a189d061141455c7a9b9761671b19c74306514f.plot > log &
```
This will quickly find 1021 proofs for 1000 challenges without any failures or exceptions (see end of file `log`). On average, each proof takes 0.054 seconds to finish.

Run the following command to test the official version of `ProofOfSpace` (it is much slower and may take 10min; get a coffee):
```
./ProofOfSpaceOfficial check -f ./plot-k32-c07-2024-03-07-00-36-824871870ead30e476ea73701a189d061141455c7a9b9761671b19c74306514f.plot > log.official &
```
This will only find 971 proofs for 1000 challenges with 22 failures and 28 exceptions (see end of file `log.official`). On average, each proof takes about 0.47 seconds to finish.

