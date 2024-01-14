# Install specific version of Zephyr
```bash
mkdir zephyr<version> &&
cd zehpyr<version> &&
git clone --single-branch --branch v<version>-branch https://github.com/zephyrproject-rtos/zephyr.git &&
west init -l zephyr &&
west update &&
source zephyr/zephyr-env.sh
```
