# rclc_on_macos
ros2/rclc (galactic branch) build on macOS Monterey

## Set up

```shell
$ mkdir -p ~/ros/galactic/src
$ cd ~/ros/galactic
$ wget https://raw.githubusercontent.com/youtalk/rclc_on_macos/main/ros2.repos
$ vcs import src < ros2.repos
$ export C_INCLUDE_PATH=/usr/local/include
$ export CPLUS_INCLUDE_PATH=/usr/local/include
$ pushd src/ros2/rclc && wget https://raw.githubusercontent.com/youtalk/rclc_on_macos/main/disable_example_pingpong.patch && patch -p1 < disable_example_pingpong.patch && popd
$ touch src/ros2/ros2cli/ros2lifecycle_test_fixtures/COLCON_IGNORE
$ colcon build --symlink-install --cmake-args -DBUILD_TESTING=OFF
```

## Demo

```shell
$ source ~/ros/galactic/install/setup.zsh
$ ros2 run rclc_examples example_service_node
Service request value: 24 + 42
```

```shell
$ source ~/ros/galactic/install/setup.zsh
$ ros2 run rclc_examples example_client_node
Send service request 24 + 42.
Received service response 24 + 42 = 66.
```
