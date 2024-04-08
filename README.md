# SolTG-CAV-2024

## Artifact evaluation


Download the VM [image](https://drive.google.com/file/d/1lJYFp505tUttvF0hOOHRemWAuoJ1-y9c/view?usp=sharing) first. Password for the "tester" is "pass"

### Reproducing general coverage numbers

When image is ready and running:
1. Enter `Documents/benchmarks_project`
2. Run `./execute_testGen.sh`.  *ATTENTION*: it might take significant amount of time, in our run it took +- 3 hours for the whole set of benchmarks.
3. After the execution of this script you should receive an image like the one below, the last line depicts an average | line coverage | statement coverage | branch coverage | function coverage | for the whole benchmark set:
   
  <img width="926" alt="image" src="https://github.com/BritikovKI/SolTG-CAV-2024/assets/31989062/c9d9082f-323d-4a54-b8fc-ad89bde7cded">
  
*The results in the last line (with the name `Total`) should correspond to the results, described in the paper: 81% line coverage and 91% function coverage*
4. To produce coverage report in HTML format call `forge coverage --report lcov` and `genhtml --branch-coverage --output cov_rep ./lcov.info`

### Reproducing data from the Fig.3 in the paper

To reproduce the results from Fig.3:
1. Enter `Documents/benchmarks_project`
2. Run `./execute_cumulative_testGen.sh` *ATTENTION*: it will take even more time then the first execution (up to 12 hours), so highly recomended to run the `execute_testGen.sh` first to check if there are any errors.
3. After the script execution you should have a set of coverage reports in the directory with naming `coverage_t.txt`, where `t` is the time, for which the `tg_nonlin` was executed. You should also get a table in `cumplot.res`, which in first row shows the time, which was taken for the test generation, and all the following rows demonstrate the percentage of the coverage for every single test for a specific timeout. There also should be a file `cumplot.png`, which should resemble the results at Fig. 3.

## Installing SolTG for usage locally

SolTG works on multiple platforms, specifically it supports Linux and MacOS. Tests were ran specifically on Ubuntu 20 and MacOS 13. If you wish to install SolTG on your machine, follow the steps below.

1. You should have an installed `docker`. For the installation instructions look into: [Mac](https://docs.docker.com/desktop/install/mac-install/), [Linux](https://docs.docker.com/desktop/install/linux-install/). Docker service should be running
in the background, to check it in Linux call: ```service docker status```. In MacOs just make sure that the Docker Desktop program is running.
2. Install `foundry`. For the instructions look here: [founry](https://book.getfoundry.sh/getting-started/installation)
3. Make sure that you have `Python 3` and `pip3` installed.
4. After the previous steps, to install `SolTG` simply call: ```pip3 install solTg```. This command will install `solTg` on your computer
*NB: under some distros it is possible you'll need to run ```sudo pip3 install solTg``` to make it runnable!*

## Using SolTG

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

