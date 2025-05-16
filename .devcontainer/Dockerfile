FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# 安装基础依赖
RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    curl \
    unzip \
    wget \
    git \
    zip \
    && rm -rf /var/lib/apt/lists/*

# 设置 JAVA_HOME
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# 安装 Android SDK cmdline-tools
ENV ANDROID_HOME=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools

RUN mkdir -p $ANDROID_HOME/cmdline-tools && \
    cd $ANDROID_HOME/cmdline-tools && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O tools.zip && \
    unzip tools.zip -d latest && \
    rm tools.zip

# 设置 sdkmanager 可用前，必须先创建 .android 目录
RUN mkdir -p ~/.android && touch ~/.android/repositories.cfg

# 安装 Android 12 (API 31) 的平台工具和构建工具
RUN yes | sdkmanager --licenses && \
    sdkmanager \
        "platform-tools" \
        "platforms;android-31" \
        "build-tools;31.0.0"
