bari@ubuntu24:~$ export GITHUB_USERNAME=YaQQrQ
bari@ubuntu24:~$ cd ${GITHUB_USERNAME}/workspace
bari@ubuntu24:~/YaQQrQ/workspace$ pushd .
~/YaQQrQ/workspace ~/YaQQrQ/workspace
bari@ubuntu24:~/YaQQrQ/workspace$ source scripts/activate
bari@ubuntu24:~/YaQQrQ/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab07 lab08
Cloning into 'lab08'...
remote: Enumerating objects: 92, done.
remote: Counting objects: 100% (92/92), done.
remote: Compressing objects: 100% (53/53), done.
remote: Total 92 (delta 28), reused 89 (delta 26), pack-reused 0 (from 0)
Receiving objects: 100% (92/92), 54.63 KiB | 165.00 KiB/s, done.
Resolving deltas: 100% (28/28), done.
bari@ubuntu24:~/YaQQrQ/workspace$ cd lab08
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git submodule update --init
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git remote remove origin
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab08
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat > Dockerfile <<EOF
> FROM ubuntu:18.04
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> RUN apt update
> RUN apt install -yy gcc g++ cmake
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> COPY . print/
> WORKDIR print
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
> RUN cmake --build _build
> RUN cmake --build _build --target install
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> ENV LOG_PATH /home/logs/log.txt
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> VOLUME /home/logs
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> WORKDIR _install/bin
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat >> Dockerfile <<EOF
> 
> ENTRYPOINT ./demo
> EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker build -t logger .
Command 'docker' not found, but can be installed with:
sudo snap install docker         # version 27.5.1, or
sudo apt  install docker.io      # version 26.1.3-0ubuntu1.1
sudo apt  install podman-docker  # version 5.0.3+ds1-5ubuntu1
See 'snap info docker' for additional versions.
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker images
Command 'docker' not found, but can be installed with:
sudo snap install docker         # version 27.5.1, or
sudo apt  install docker.io      # version 26.1.3-0ubuntu1.1
sudo apt  install podman-docker  # version 5.0.3+ds1-5ubuntu1
See 'snap info docker' for additional versions.
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo apt install docker
[sudo] password for bari: 
Package docker is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
However the following packages replace it:
  wmdocker


Error: Package 'docker' has no installation candidate
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo snap install docker
docker 27.5.1 from Canonical✓ installed
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker build -t logger .
ERROR: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger .
[+] Building 34.5s (10/13)                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 378B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:18.04                                           2.7s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [1/9] FROM docker.io/library/ubuntu:18.04@sha256:152dc042452c496007f07ca9127571cb9c29697f42acbfad723  3.8s
 => => resolve docker.io/library/ubuntu:18.04@sha256:152dc042452c496007f07ca9127571cb9c29697f42acbfad723  0.0s
 => => sha256:152dc042452c496007f07ca9127571cb9c29697f42acbfad72324b2bb2e43c98 1.33kB / 1.33kB            0.0s
 => => sha256:dca176c9663a7ba4c1f0e710986f5a25e672842963d95b960191e2d9f7185ebe 424B / 424B                0.0s
 => => sha256:f9a80a55f492e823bf5d51f1bd5f87ea3eed1cb31788686aa99a2fb61a27af6a 2.30kB / 2.30kB            0.0s
 => => sha256:7c457f213c7634afb95a0fb2410a74b7b5bc0ba527033362c240c7a11bef4331 25.69MB / 25.69MB          2.9s
 => => extracting sha256:7c457f213c7634afb95a0fb2410a74b7b5bc0ba527033362c240c7a11bef4331                 0.7s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 493.30kB                                                                     0.0s
 => [2/9] RUN apt update                                                                                  6.5s
 => [3/9] RUN apt install -yy gcc g++ cmake                                                              21.0s
 => [4/9] COPY . print/                                                                                   0.0s
 => [5/9] WORKDIR print                                                                                   0.0s
 => ERROR [6/9] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install         0.3s
------
 > [6/9] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install:
0.241 CMake Error at CMakeLists.txt:1 (cmake_minimum_required):
0.241   CMake 3.14 or higher is required.  You are running version 3.10.2
0.241 
0.241 
0.241 -- Configuring incomplete, errors occurred!
------

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 12)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 18)
Dockerfile:9
--------------------
   7 |     WORKDIR print
   8 |     
   9 | >>> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
  10 |     RUN cmake --build _build
  11 |     RUN cmake --build _build --target install
--------------------
ERROR: failed to solve: process "/bin/sh -c cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install" did not complete successfully: exit code: 1
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger .
[+] Building 100.6s (10/13)                                                                     docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 378B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                           1.6s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [1/9] FROM docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd1e  4.3s
 => => resolve docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd1e  0.0s
 => => sha256:a76d0e9d99f0e91640e35824a6259c93156f0f07b7778ba05808c750e7fa6e68 424B / 424B                0.0s
 => => sha256:cc934a90cd99a939f3922f858ac8f055427300ee3ee4dfcd303c53e571d0aeab 2.30kB / 2.30kB            0.0s
 => => sha256:30a9c22ae099393b0131322d7f50d8a9d7cd06c5e518cd27a19ac960a4d0aba3 29.53MB / 29.53MB          3.4s
 => => sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd1e3120da3ff52c3 6.69kB / 6.69kB            0.0s
 => => extracting sha256:30a9c22ae099393b0131322d7f50d8a9d7cd06c5e518cd27a19ac960a4d0aba3                 0.7s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 3.95kB                                                                       0.0s
 => [2/9] RUN apt update                                                                                  7.4s
 => [3/9] RUN apt install -yy gcc g++ cmake                                                              22.0s
 => [4/9] COPY . print/                                                                                   0.0s
 => [5/9] WORKDIR print                                                                                   0.0s
 => ERROR [6/9] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install        65.1s
------
 > [6/9] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install:
0.326 -- [hunter] Initializing Hunter workspace (572541b3a9e2c1ccb0c0e552f6dc12219c0d6a0b)
0.326 -- [hunter]   https://github.com/cpp-pm/hunter/archive/v0.23.314.tar.gz
0.326 -- [hunter]   -> /root/.hunter/_Base/Download/Hunter/0.23.314/572541b
65.08 CMake Error at Build/Hunter-prefix/src/Hunter-stamp/download-Hunter.cmake:170 (message):
65.08   Each download failed!
65.08 
65.08     
65.08     
65.08 
65.08 
65.08 gmake[2]: *** [CMakeFiles/Hunter.dir/build.make:98: Hunter-prefix/src/Hunter-stamp/Hunter-download] Error 1
65.08 gmake[1]: *** [CMakeFiles/Makefile2:83: CMakeFiles/Hunter.dir/all] Error 2
65.08 gmake: *** [Makefile:91: all] Error 2
65.08 
65.08 [hunter ** INTERNAL **] Build project failed
65.08 [hunter ** INTERNAL **] [Directory:/print]
65.08 
65.08 -- Configuring incomplete, errors occurred!
65.08 ------------------------------ ERROR ------------------------------
65.08     https://hunter.readthedocs.io/en/latest/reference/errors/error.internal.html
65.08 -------------------------------------------------------------------
65.08 
65.08 CMake Error at cmake/HunterGate.cmake:88 (message):
65.08 Call Stack (most recent call first):
65.08   cmake/HunterGate.cmake:98 (hunter_gate_error_page)
65.08   cmake/HunterGate.cmake:347 (hunter_gate_internal_error)
65.08   cmake/HunterGate.cmake:511 (hunter_gate_download)
65.08   CMakeLists.txt:4 (HunterGate)
65.08 
65.08 
------

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 12)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 18)
Dockerfile:9
--------------------
   7 |     WORKDIR print
   8 |     
   9 | >>> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
  10 |     RUN cmake --build _build
  11 |     RUN cmake --build _build --target install
--------------------
ERROR: failed to solve: process "/bin/sh -c cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install" did not complete successfully: exit code: 1
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker build -t logger .
ERROR: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger .\
> 
[+] Building 67.6s (11/14)                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 428B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                           2.3s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [ 1/10] FROM docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd  0.0s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 4.00kB                                                                       0.0s
 => CACHED [ 2/10] RUN apt update                                                                         0.0s
 => CACHED [ 3/10] RUN apt install -yy gcc g++ cmake                                                      0.0s
 => [ 4/10] COPY . print/                                                                                 0.0s
 => [ 5/10] WORKDIR print                                                                                 0.0s
 => [ 6/10] RUN apt update && apt install -y ca-certificates                                              2.6s
 => ERROR [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install      62.5s
------
 > [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install:
0.194 -- [hunter] Initializing Hunter workspace (572541b3a9e2c1ccb0c0e552f6dc12219c0d6a0b)
0.194 -- [hunter]   https://github.com/cpp-pm/hunter/archive/v0.23.314.tar.gz
0.194 -- [hunter]   -> /root/.hunter/_Base/Download/Hunter/0.23.314/572541b
62.43 CMake Error at Build/Hunter-prefix/src/Hunter-stamp/download-Hunter.cmake:170 (message):
62.43   Each download failed!
62.43 
62.43     
62.43     
62.43 
62.43 
62.44 gmake[2]: *** [CMakeFiles/Hunter.dir/build.make:98: Hunter-prefix/src/Hunter-stamp/Hunter-download] Error 1
62.44 gmake[1]: *** [CMakeFiles/Makefile2:83: CMakeFiles/Hunter.dir/all] Error 2
62.44 gmake: *** [Makefile:91: all] Error 2
62.44 
62.44 [hunter ** INTERNAL **] Build project failed
62.44 [hunter ** INTERNAL **] [Directory:/print]
62.44 
62.44 ------------------------------ ERROR ------------------------------
62.44     https://hunter.readthedocs.io/en/latest/reference/errors/error.internal.html
62.44 -------------------------------------------------------------------
62.44 
62.44 CMake Error at cmake/HunterGate.cmake:88 (message):
62.44 Call Stack (most recent call first):
62.44   cmake/HunterGate.cmake:98 (hunter_gate_error_page)
62.44   cmake/HunterGate.cmake:347 (hunter_gate_internal_error)
62.44   cmake/HunterGate.cmake:511 (hunter_gate_download)
62.44   CMakeLists.txt:4 (HunterGate)
62.44 
62.44 
62.44 -- Configuring incomplete, errors occurred!
------

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 14)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 20)
Dockerfile:11
--------------------
   9 |     RUN apt update && apt install -y ca-certificates
  10 |     
  11 | >>> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
  12 |     RUN cmake --build _build
  13 |     RUN cmake --build _build --target install
--------------------
ERROR: failed to solve: process "/bin/sh -c cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install" did not complete successfully: exit code: 1
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger
ERROR: "docker buildx build" requires exactly 1 argument.
See 'docker buildx build --help'.

Usage:  docker buildx build [OPTIONS] PATH | URL | -

Start a build
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger .
[+] Building 28.0s (11/14)                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 428B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                           0.8s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [ 1/10] FROM docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd  0.0s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 4.60kB                                                                       0.0s
 => CACHED [ 2/10] RUN apt update                                                                         0.0s
 => CACHED [ 3/10] RUN apt install -yy gcc g++ cmake                                                      0.0s
 => [ 4/10] COPY . print/                                                                                 0.1s
 => [ 5/10] WORKDIR print                                                                                 0.0s
 => [ 6/10] RUN apt update && apt install -y ca-certificates                                              2.5s
 => ERROR [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install      24.5s
------
 > [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install:
0.240 -- [hunter] Initializing Hunter workspace (a1c4e0b5e6e9a9a0f8e1b2c3d4e5f6a7b8c9d0e1)
0.240 -- [hunter]   https://github.com/cpp-pm/hunter/archive/v0.24.8.tar.gz
0.240 -- [hunter]   -> /root/.hunter/_Base/Download/Hunter/0.24.8/a1c4e0b
24.44 CMake Error at Build/Hunter-prefix/src/Hunter-stamp/download-Hunter.cmake:170 (message):
24.44   Each download failed!
24.44 
24.44     
24.44     
24.44 
24.44 
24.44 gmake[2]: *** [CMakeFiles/Hunter.dir/build.make:98: Hunter-prefix/src/Hunter-stamp/Hunter-download] Error 1
24.44 gmake[1]: *** [CMakeFiles/Makefile2:83: CMakeFiles/Hunter.dir/all] Error 2
24.44 gmake: *** [Makefile:91: all] Error 2
24.45 
24.45 [hunter ** INTERNAL **] Build project failed
24.45 [hunter ** INTERNAL **] [Directory:/print]
24.45 
24.45 ------------------------------ ERROR ------------------------------
24.45     https://hunter.readthedocs.io/en/latest/reference/errors/error.internal.html
24.45 -------------------------------------------------------------------
24.45 
24.45 CMake Error at cmake/HunterGate.cmake:88 (message):
24.45 Call Stack (most recent call first):
24.45   cmake/HunterGate.cmake:98 (hunter_gate_error_page)
24.45   cmake/HunterGate.cmake:347 (hunter_gate_internal_error)
24.45   cmake/HunterGate.cmake:511 (hunter_gate_download)
24.45   CMakeLists.txt:4 (HunterGate)
24.45 
24.45 
24.45 -- Configuring incomplete, errors occurred!
------

 3 warnings found (use docker --debug to expand):
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 20)
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 14)
Dockerfile:11
--------------------
   9 |     RUN apt update && apt install -y ca-certificates
  10 |     
  11 | >>> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
  12 |     RUN cmake --build _build
  13 |     RUN cmake --build _build --target install
--------------------
ERROR: failed to solve: process "/bin/sh -c cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install" did not complete successfully: exit code: 1
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build --network=host -t logger .
[+] Building 104.3s (11/14)                                                                     docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 428B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                           2.2s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => CACHED [ 1/10] FROM docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e179  0.0s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 3.60kB                                                                       0.0s
 => [ 2/10] RUN apt update                                                                                7.9s
 => [ 3/10] RUN apt install -yy gcc g++ cmake                                                            44.5s 
 => [ 4/10] COPY . print/                                                                                 0.0s 
 => [ 5/10] WORKDIR print                                                                                 0.0s 
 => [ 6/10] RUN apt update && apt install -y ca-certificates                                              2.6s 
 => ERROR [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install      47.1s 
------
 > [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install:
0.096 -- [hunter] Initializing Hunter workspace (a1c4e0b5e6e9a9a0f8e1b2c3d4e5f6a7b8c9d0e1)
0.096 -- [hunter]   https://github.com/cpp-pm/hunter/archive/v0.24.8.tar.gz
0.096 -- [hunter]   -> /root/.hunter/_Base/Download/Hunter/0.24.8/a1c4e0b
47.01 CMake Error at Build/Hunter-prefix/src/Hunter-stamp/download-Hunter.cmake:170 (message):
47.01   Each download failed!
47.01 
47.01     
47.01     
47.01 
47.01 
47.01 gmake[2]: *** [CMakeFiles/Hunter.dir/build.make:98: Hunter-prefix/src/Hunter-stamp/Hunter-download] Error 1
47.01 gmake[1]: *** [CMakeFiles/Makefile2:83: CMakeFiles/Hunter.dir/all] Error 2
47.01 gmake: *** [Makefile:91: all] Error 2
47.01 -- Configuring incomplete, errors occurred!
47.01 
47.01 [hunter ** INTERNAL **] Build project failed
47.01 [hunter ** INTERNAL **] [Directory:/print]
47.01 
47.01 ------------------------------ ERROR ------------------------------
47.01     https://hunter.readthedocs.io/en/latest/reference/errors/error.internal.html
47.01 -------------------------------------------------------------------
47.01 
47.01 CMake Error at cmake/HunterGate.cmake:88 (message):
47.01 Call Stack (most recent call first):
47.01   cmake/HunterGate.cmake:98 (hunter_gate_error_page)
47.01   cmake/HunterGate.cmake:347 (hunter_gate_internal_error)
47.01   cmake/HunterGate.cmake:511 (hunter_gate_download)
47.01   CMakeLists.txt:4 (HunterGate)
47.01 
47.01 
------

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 14)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 20)
Dockerfile:11
--------------------
   9 |     RUN apt update && apt install -y ca-certificates
  10 |     
  11 | >>> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
  12 |     RUN cmake --build _build
  13 |     RUN cmake --build _build --target install
--------------------
ERROR: failed to solve: process "/bin/sh -c cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install" did not complete successfully: exit code: 1
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker build -t logger .
[+] Building 44.0s (15/15) FINISHED                                                             docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 428B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                           5.5s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [ 1/10] FROM docker.io/library/ubuntu:22.04@sha256:d80997daaa3811b175119350d84305e1ec9129e1799bba0bd  0.0s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 4.60kB                                                                       0.0s
 => CACHED [ 2/10] RUN apt update                                                                         0.0s
 => CACHED [ 3/10] RUN apt install -yy gcc g++ cmake                                                      0.0s
 => [ 4/10] COPY . print/                                                                                 0.1s
 => [ 5/10] WORKDIR print                                                                                 0.0s
 => [ 6/10] RUN apt update && apt install -y ca-certificates                                              2.9s
 => [ 7/10] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install            33.3s
 => [ 8/10] RUN cmake --build _build                                                                      0.8s
 => [ 9/10] RUN cmake --build _build --target install                                                     0.3s
 => [10/10] WORKDIR _install/bin                                                                          0.1s
 => exporting to image                                                                                    0.9s
 => => exporting layers                                                                                   0.8s
 => => writing image sha256:059555e440f08ef7d261e97926f26b297812c83397a0de357cc66a4953b23e99              0.0s
 => => naming to docker.io/library/logger                                                                 0.0s

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 7)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 14)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 20)
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker images
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
logger       latest    059555e440f0   39 seconds ago   452MB
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ mkdir logs
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
<C-D>
EOF

^Cbari@ubuntu24:~/YaQQrQ/workspace/lab08$ docker inspect logger
[]
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/containers/logger/json": dial unix /var/run/docker.sock: connect: permission denied
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sudo docker inspect logger
[
    {
        "Id": "sha256:059555e440f08ef7d261e97926f26b297812c83397a0de357cc66a4953b23e99",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2025-04-30T19:08:36.952889748Z",
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": null,
            "Image": "",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 452324047,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/snap/docker/common/var-lib-docker/overlay2/y820syj0d78gnnr6uufnqeamk/diff:/var/snap/docker/common/var-lib-docker/overlay2/nf5s41rapp1erky27nj0fdehw/diff:/var/snap/docker/common/var-lib-docker/overlay2/qk1zzxwmwuch7dpjvx8vn3bhm/diff:/var/snap/docker/common/var-lib-docker/overlay2/zagszix6f27co11yiykrcmzxk/diff:/var/snap/docker/common/var-lib-docker/overlay2/d05w8wq8cdivk35749zyjxjyf/diff:/var/snap/docker/common/var-lib-docker/overlay2/xd2j4vpyln3fdp6v9ehhhznsa/diff:/var/snap/docker/common/var-lib-docker/overlay2/r6labihgtcrq98580i76pxdg6/diff:/var/snap/docker/common/var-lib-docker/overlay2/z9mjve9qwejhiz8updrcji65j/diff:/var/snap/docker/common/var-lib-docker/overlay2/360689b909e6c9ce9171ee622d8fa472c7f5bd091bf3af64df7ab7afbb4de5f6/diff",
                "MergedDir": "/var/snap/docker/common/var-lib-docker/overlay2/pizuhz0pd41oi4alcsvrxyjxp/merged",
                "UpperDir": "/var/snap/docker/common/var-lib-docker/overlay2/pizuhz0pd41oi4alcsvrxyjxp/diff",
                "WorkDir": "/var/snap/docker/common/var-lib-docker/overlay2/pizuhz0pd41oi4alcsvrxyjxp/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:65c636ce09f299ba8ea7157c8d126dfd5b115fa7bbc5d634a91b34786958546e",
                "sha256:c758aa535cf266329b507e556d364b3587604f610cdbc4b637d584fbf46c1dfb",
                "sha256:d8010138858dbb5ebf4ea24fe880a9d76e04c069c899bbce36cb6fc6ca0706c3",
                "sha256:2a903e3f259450fca820b0a27c50ac655e26183314b66fe9fdbbd10878deda73",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:0d0f0bdaba4205ec5900022bc2839529c00441d2d0acaf0a95e0dfc49228160b",
                "sha256:c4c847c531f87120a3fa24aafbcf94ef6b4673c5e598a7b151f16af134b9db03",
                "sha256:afd2c5889e2c08d73d298c92929967d53268bf0d052d83fdea086bdcc62ef4c0",
                "sha256:4458541468089a44859967bb2153e30686c20915ac359eed6540efeeccfee893",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2025-04-30T19:08:37.815213308Z"
        }
    }
]
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ cat logs/log.txt
text1
text2
text3
<C-D>
EOF
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ gsed -i 's/lab07/lab08/g' README.md
Command 'gsed' not found, did you mean:
  command 'gted' from deb gnome-text-editor (48.1-1)
  command 'sed' from deb sed (4.9-2build1)
  command 'gsnd' from deb ghostscript (10.05.0dfsg1-0ubuntu1)
Try: sudo apt install <deb name>
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ sed -i 's/lab07/lab08/g' README.md
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ vim .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ vim .travis.yml

[1]+  Stopped                 vim .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ vim .travis.yml

[2]+  Stopped                 vim .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ vim .travis.yml

[3]+  Stopped                 vim .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ nano .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git add Dockerfile
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git add .travis.yml
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git commit -m"adding Dockerfile"
[master fe7c346] adding Dockerfile
 2 files changed, 26 insertions(+)
 create mode 100644 Dockerfile
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git push origin master
Username for 'https://github.com': YaQQrQ
Password for 'https://YaQQrQ@github.com': 
Enumerating objects: 96, done.
Counting objects: 100% (96/96), done.
Delta compression using up to 8 threads
Compressing objects: 100% (55/55), done.
Writing objects: 100% (96/96), 55.33 KiB | 55.33 MiB/s, done.
Total 96 (delta 30), reused 91 (delta 28), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (30/30), done.
remote: error: GH013: Repository rule violations found for refs/heads/master.
remote: 
remote: - GITHUB PUSH PROTECTION
remote:   —————————————————————————————————————————
remote:     Resolve the following violations before pushing again
remote: 
remote:     - Push cannot contain secrets
remote: 
remote:     
remote:      (?) Learn how to resolve a blocked push
remote:      https://docs.github.com/code-security/secret-scanning/working-with-secret-scanning-and-push-protection/working-with-push-protection-from-the-command-line#resolving-a-blocked-push
remote:     
remote:     
remote:       —— GitHub Personal Access Token ——————————————————————
remote:        locations:
remote:          - commit: 3dbefd07df45839aa845f4053ff6222de4a836ba
remote:            path: README.md:2
remote:     
remote:        (?) To push, remove secret from commit(s) or follow this URL to allow the secret.
remote:        https://github.com/YaQQrQ/lab08/security/secret-scanning/unblock-secret/2wShQLtiOedSHJ0AwDLGygv4oMC
remote:     
remote: 
remote: 
To https://github.com/YaQQrQ/lab08
 ! [remote rejected] master -> master (push declined due to repository rule violations)
error: failed to push some refs to 'https://github.com/YaQQrQ/lab08'
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ git push origin master
Username for 'https://github.com': YaQQrQ
Password for 'https://YaQQrQ@github.com': 
Enumerating objects: 96, done.
Counting objects: 100% (96/96), done.
Delta compression using up to 8 threads
Compressing objects: 100% (55/55), done.
Writing objects: 100% (96/96), 55.33 KiB | 55.33 MiB/s, done.
Total 96 (delta 30), reused 91 (delta 28), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (30/30), done.
To https://github.com/YaQQrQ/lab08
 * [new branch]      master -> master
bari@ubuntu24:~/YaQQrQ/workspace/lab08$ 

