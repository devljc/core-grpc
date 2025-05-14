# 🧩 Core gRPC Module - gRPC 모듈

> - **gRPC 모듈** 은 Spring Boot 기반 마이크로서비스 간 통신을 위한 gRPC 서버 및 클라이언트 인터페이스를 제공합니다.
> - 서비스 간 의존도를 낮추고, 고성능 바이너리 프로토콜 기반의 통신을 통해 안정적이고 빠른 데이터 교환이 가능하게 합니다.
> - 버전 관리는 Gradle의 Version Catalog를 사용하여 효율적으로 관리합니다.
---

## 📁 프로젝트 구조

```
core-grpc/
├── build.gradle
├── gradle/libs.versions.toml
├── settings.gradle
├── src/
│   └── main/
│       ├── proto/
│           └── hello.proto
│     
└── build/
    └── generated/
        └── source/
            └── proto/
                └── main/
                    ├── java/      ← 일반 protobuf 메시지 코드
                    └── grpc/      ← gRPC Stub (서비스용)
```

---

## ⚙️ Gradle 설정 요약

```kotlin
plugins {
    id("java-library")
    alias(libs.plugins.protobuf)
}

dependencies {
    implementation(libs.grpc.netty.shaded)
    implementation(libs.grpc.stub)
    implementation(libs.grpc.protobuf)
    implementation(libs.protobuf.java)
    implementation(libs.javax.annotation.api) // @Generated 해결
}
```

---

## 📦 사용 라이브러리 및 버전

| 라이브러리                                        | 설명                            | 버전              |
|----------------------------------------------|-------------------------------|-----------------|
| `io.grpc:grpc-netty-shaded`                  | gRPC용 Netty 기반 네트워크 전송        | `1.65.1`        |
| `io.grpc:grpc-stub`                          | gRPC Stub 코드 생성 라이브러리         | `1.65.1`        |
| `io.grpc:grpc-protobuf`                      | gRPC용 Protobuf 직렬화 지원         | `1.65.1`        |
| `com.google.protobuf:protobuf-java`          | 일반 Protobuf 메시지 처리            | `4.28.2`        |
| `com.google.protobuf:protobuf-gradle-plugin` | Protobuf 컴파일 플러그인             | `0.9.4`         |
| `javax.annotation:javax.annotation-api`      | @Generated 오류 방지용 Java 표준 API | `1.3.2`         |
| `net.devh:grpc-client-spring-boot-starter`   | gRPC 클라이언트 스타터                | `3.1.0.RELEASE` |
| `net.devh:grpc-server-spring-boot-starter`   | gRPC 서버 스타터                   | `3.1.0.RELEASE` |

> 📌 버전 관리는 libs.versions.toml 에서 통합 관리합니다.
---

## ✅ 사용 예시: proto 정의 (예: `hello.proto`)

```proto
syntax = "proto3";

package hello;

option java_package = "com.example.hello";
option java_multiple_files = true;

service HelloService {
  rpc SayHello (HelloRequest) returns (HelloResponse);
}

message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}
```

---

## 📄 License

MIT License © 2025 leebak