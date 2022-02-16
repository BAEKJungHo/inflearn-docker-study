# Buildkit 이 기본적으로 enable 되는 현상

- 도커 2.4.0+ 버전 업데이트로 인해서 `Buildkit` 을 기본적으로 사용할 수 있게됐습니다.
- 이 Buildkit 을 사용하므로 인해 나타나는 현상은 도커 파일을 빌드 할 때 나타납니다. 
- 빌드 하는 과정에서 다른 출력 문구를 내보냅니다.
- 그 중에서 가장 주요한 차이점은 빌드 프로세스 마지막 부분에 나오는 이미지 ID 입니다. 

## 기존 빌드 프로세스에서 나오는 출력 문구
    
```
---> bd70880ecc90
Successfully built bd70880ecc90
```

## Buildkit 이 기본으로 사용될 때 빌드 프로세스에서 나오는 출력 문구   

```
=> => exporting layers  0.0s

=> => writing image sha256:aa19c32ksj94839dj2-2039ccbd9cddd 0.0 s 
```

결론적으로는 두개의 ID 모두 컨테이너를 실행할 수 있는 아이디 입니다.    

- docker run bd70880ecc90 
- docker run aa19c32ksj94839dj2-2039ccbd9cddd   

이 둘 모두 같은 컨테이너를 실행하게 됩니다.

그러기에 이 강의를 더 쉽게 따라가기 위해서는 Buildkit 을 비활성화 하시면 됩니다. 

Buildkit 비활성화 하는 방법 

1. 도커 아이콘을 클릭 합니다. 
2. 아래 그림과 같이 Preferences 버튼을 클릭합니다.   
3. Docker Engine 버튼을 클릭 합니다. 
4. 마지막으로 buildkit 키의 값을 false로 바꿔줍니다. 

```
{
    "experimental" : false,
    "features" :  {
        "buildkit" : false
    },
    "builder" : {
        "gc" : {
            "enabled" : true,
            "defaultKeepStorage" : "20GB"
        }
    }
}
```

```