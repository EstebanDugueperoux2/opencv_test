# Conan opencv test

conan new cmake_exe -d name=opencv_test -d version=0.0.1 

docker run --memory=10g --cpus=10 --rm -ti -v conan_cache:~/.conan2/ debian:bullseye
apt -y update
apt install -y python3-pip cmake ninja-build git vim pkg-config
pip install --upgrade "conan"

git clone https://github.com/EstebanDugueperoux2/opencv_test.git

## Standard build using conan 2.x

conan create . --build missing -o */*:shared=True -s build_type=Debug --profile:build .conan/profiles/build_profile --profile:host .conan/profiles/build_profile -c tools.system.package_manager:mode=install &> build_shared.log

## Cross build to arm

apt install -y crossbuild-essential-arm64 python3-pip cmake ninja-build ssh git vim pkg-config

conan create . --build missing -s build_type=Debug -o */*:shared=True --profile:build .conan/profiles/build_profile --profile:host .conan/profiles/linux-armv7hf-gcc7 -c tools.system.package_manager:mode=install

E: Unable to locate package libva-dev:arm64
ERROR: vaapi/system: Error in system_requirements() method, line 38
	apt.install(["libva-dev"], update=True, check=True)
	ConanException: Command 'apt-get install -y --no-install-recommends libva-dev:arm64' failed
