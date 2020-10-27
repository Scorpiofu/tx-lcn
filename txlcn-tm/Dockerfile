# VERSION 6.0.0
# Author: fuyz
# 打包jar采用maven镜像
FROM maven:3.5.2-jdk-8-alpine AS MAVEN_BUILD
# 工作目录在镜像的 /build 目录下
WORKDIR /build/
# 把本地的 pom.xml 和 src目录 复制到镜像的/build目录下
COPY pom.xml /build/
COPY src /build/src/
# 执行maven打包
RUN mvn clean package '-Dmaven.test.skip=true'
# 运行jar采用jdk基础镜像
FROM frolvlad/alpine-oraclejdk8:slim
# 设置工作目录在镜像的 /app 目录下
WORKDIR /app
# 将jar包添加到容器中并更名为app.jar
COPY --from=MAVEN_BUILD /build/target/txlcn-tm-6.0.0.RELEASE.jar /app/
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone
EXPOSE 7970 8070
ENTRYPOINT ["java", "-jar", "/txlcn-tm-6.0.0.RELEASE.jar"]


