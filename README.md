# Appium Aurora Docker

## Building

Build image:

```
    docker build -t $appium-aurora -f build.alpine/Dockerfile .
```

Run Appium container:

```
    docker run --rm -it --network=host appium-aurora
```
