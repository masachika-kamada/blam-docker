# blam-docker

- Purpose: Run [blam](https://github.com/erik-nelson/blam) with Docker
- Tested environment: Ubuntu20.04

## Usage

```
git clone https://github.com/masachika-kamada/blam-docker.git
cd ros_melodic_blam_fork
sh build.sh
sh run.sh
cd catkin_ws
mkdir src && cd src
git clone https://github.com/naisy/blam.git
cd blam
sh build
# SLAM
./blam_offline.sh [bag file]
```

## Reference page

https://qiita.com/k-koh/items/fa87e9eae3aa4203ba2c

Due to build errors in the original repository, I used the forked repository.
