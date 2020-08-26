# 개발 및 운영시 필요한 Tip

## Container 내부 소스 수정하여 실행하기
> nodejs와 같은 script기반 언어로 작성된 소스를 Debug할 때, 원소스의 수정이 필요한 경우  
> 소스를 sudo docker cp [container_name]:[sourcepath] [host_path] 로 복사하고 수정  
> docker run -v 를 이용항 해당 경로를 Replace


## Container 정보 획득
> container의 세부 정보를 통해 실행 명령어 등을 확인 할 수 있음.
> 예) sudo docker inspect nginx

## Container 위조 방법(Fishing)
> Container는 Registry내에 Registry/Project/Repository:Tag로 구성되어 있으며,  
> 실행 및 Pull시에 해당 URI를 통해 실행하는 경우,  
> Tag를 재정의(kubepia/my-nginx:v1.0 --> docker.io/library/nginx:latest)하여 해당 Host에 저장(Cache) 이후에 sudo docker run 을 하면 재정의된 container가 실행됨

## Container 위변조 방지
> 위변조를 원천적으로 방지하기 위해서는 Registry 내에 유일하게 관리되는 digest 값을 이용하여 pull/run 실행 할 때 container image를 지정하면 위변조를 방지 할 수 있음  
> 예) sudo docker run nginx@sha256:b0ad43f7ee5edbc0effbc14645ae7055e21bc1973aee5150745632a24a752661

## 불필요한 file 제거 : .dockerignore
> Copy/Add 실행시에 .dockerignore에 지정한 패턴의 file은 제외되어 복사됨