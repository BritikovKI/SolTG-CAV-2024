# SolTG-CAV-2024

## Running SolTG in a VM

Download the VM [image](https://drive.google.com/file/d/1CuLUldD1-wPW-SGS8xSw5qsAWu7z_7Xz/view?usp=sharing) first. Password for the image/root is "4rfgt5"
When image is ready and running:
1. Enter `Documents/solTg_benchmarks`
2. Execute `solTg -i bench`
3. After the testgeneration is finished, execute three bash commands:
   ```mv test gen_tests```
   ```mkdir test```
   ```cp -r gen_tests/**/*.t.sol ./test```
   ```rm -r gen_tests```
4. After it call  `forge test` to check that tests work correctly
5. Call  `forge coverage` to see the generated coverage report
6. To produce coverage report in HTML format call `forge coverage --report lcov` and `genhtml --branch-coverage --output cov_rep ./lcov.info`


## Installing SolTG

SolTG works on multiple platforms, specifically it supports Linux and MacOS. Tests were ran specifically on Ubuntu 20 and MacOS 13.

1. You should have an installed docker. For the installation instructions look into: [Mac](https://docs.docker.com/desktop/install/mac-install/), [Linux](https://docs.docker.com/desktop/install/linux-install/). Docker service should be running
in the background, to check it in Linux call: ```service docker status```. In MacOs just make sure that the Docker Desktop program is running.
2. Install foundry forge. For the instructions look here: [founry](https://book.getfoundry.sh/getting-started/installation)
3. Make sure that you have Python 3 and pip3 installed.
4. After the previous steps, to install `SolTG` simply call: ```pip3 install solTg```. This command will install `solTg` on your computer
*NB: under some repositories it is possible you'll need to run ```sudo pip3 install solTg``` to make it runnable!*

## Running experiments

1. Create an empty directory with any name, for example `SolTgBench`
2. Go to newly created directory and call `foundry init` command from it
3. `foundry init` should create new empty project, remove files from `src`, `test` and `scripts` folders
4. Upload zip file containing benchmarks and src of the code from [here](https://drive.google.com/file/d/1WVtRMnjzNDhd96LZRsLjcNJnXsiDlhtF/view?usp=sharing).
5. Copy both `bench` and `src` directory to the forge project (in our case `SolTgBranch` directory).
6. Run `solTg -i bench`. This will run test generation for all of the `.sol` files in the `bench` directory. ATTENTION: it might take significant amount of time, on our run it takes +- 3 hours for the whole set of benchmarks.
7. After the testgeneration is finished, execute three bash commands:
   ```mv test gen_tests```
   ```mkdir test```
   ```cp -r gen_tests/**/*.t.sol ./test```
   ```rm -r gen_tests```
9. After it call  `forge test` to check that tests work correctly
10. Call  `forge coverage` to see the generated coverage report
11. To produce coverage report in HTML format call `forge coverage --report lcov` and `genhtml --branch-coverage --output cov_rep ./lcov.info`

Coverage numbers should be the same as demonstrated in the paper for this set of benchmarks!

ATTENTION!!! For used version of SolTg(it is fixed in later versions) it is required that file should have at least single assert statement in it inside of some contract method!

