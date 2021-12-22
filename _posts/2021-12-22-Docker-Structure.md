---
layout: post
title: "Docker-Structure"
date: 2021-12-16
categories: Docker
tags: [hello, groompang, serverless, bob]
---

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F75791858-addb-4153-9f15-b8496675dacc%2FUntitled.png?table=block&id=c36c0488-2f2f-4797-8503-a2aea75f3086&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)

- Docker Network 구조
    
    # Docker Network 구조
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F99200835-440a-4a03-89ac-ec1fe9233c19%2FUntitled.png?table=block&id=9683d143-02c9-47c2-a1ab-838a5fabdf5c&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    Docker0 interface : bridge interface
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F039a15ea-59a8-4ba5-969d-80b2278d28eb%2FUntitled.png?table=block&id=827d6345-a8be-4a35-98e8-fdaf3d31019c&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ## network Driver
    
    - host
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc6433539-16bf-47a0-81e8-f5ba003d0e50%2FUntitled.png?table=block&id=4fce0499-0646-42ed-97e5-97d8fe3d9f18&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    - bridge
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6d5b5956-e1bc-4ad8-89c2-a1694747a147%2FUntitled.png?table=block&id=2d101815-390b-43b0-90e5-363b3aa35e03&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff44ff258-c50f-442e-810a-660d01c9dc47%2FUntitled.png?table=block&id=6e5f3dbd-b004-4204-ae89-74426e77269e&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    - container: 다른 컨테이너의 네트워크 공유
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F98073d3b-bf52-4585-828c-2d756c3fd48b%2FUntitled.png?table=block&id=913ddc41-ae7c-4c24-87cb-bb13b3cab960&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    - overlay: container 끼리 연결되는 가상의 네트워크 망 생성
    - MACVLAN
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F62147f42-35c4-44b7-96f9-afc3e89d1f3a%2FUntitled.png?table=block&id=f0fac772-83e5-4de5-8666-3b347a68cf8e&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    - none: 외부통신 불가능
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2f801633-a326-4518-88dd-61d5bdc7e622%2FUntitled.png?table=block&id=cd61f289-63ae-4822-8ed3-3f45cc1b3a67&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ## 외부 통신
    
    port-forwarding
    
    ```bash
    root@~~# docker run -d -p 8080:80 --name web_svr01 httpd 
    
    root@~~# docker ps -a
    CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
    0fa48359f36d        httpd               "httpd-foreground"   12 minutes ago      Up 12 minutes       0.0.0.0:8080->80/tcp   web_svr01
    ```
    
    docker-proxy: 요청을 기다리는 주체
    
    ## Containter link DNS
    
    ```bash
    root@~~# docker run -d --name web02 --link mysql httpd
    
    # hosts 파일 자동 링크
    root@~~# docker exec -t web02 cat /etc/hosts
    127.0.0.1       localhost
    ::1     localhost ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    172.17.0.6      mysql 17b6c5f037a9
    172.17.0.2      14f6f2a16abc
    
    # hosts 파일 마운트 상태 확인
    root@~~# docker exec -t web02 df -h
    Filesystem                                                                                        Size  Used Avail Use% Mounted on
    /dev/disk/by-uuid/736fad7a-387f-4420-b934-4ccbafa26d16                                            7.8G  2.1G  5.3G  28% /etc/hosts
    
    # hosts 디렉토리 탐색
    root@~~# docker inspect -f "{{ .HostsPath }}" web02
    /var/lib/docker/containers/14f6f2a16abc8660ba32004c8eff091e5a16f0ace57a3609d770f845485d103f/hosts
    
    # 알아낸 파일 경로를 통한 확인
    root@~~# cat /var/lib/docker/containers/14f6f2a16abc8660ba32004c8eff091e5a16f0ace57a3609d770f845485d103f/hosts
    ```
    
- Docker 구조
    
    # Docker 구조
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F87a641f7-48c8-4fc5-9b07-1e44619d41f1%2FUntitled.png?table=block&id=153a1b92-c6f2-4d32-be35-6b41256c9c08&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    [[네트워크] REST API란? REST, RESTful이란?](http://khj93.tistory.com/entry/네트워크-REST-API란-REST-RESTful이란)
    
    ### RESTful API:REST의 설계 규칙을 따르는 시스템 API
    
    REST(Representational State Transfer): 분산 시스템 설계를 위한 아키텍처 스타일/ 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 것
    
    HTTP URI를 이용하여 자원을 명시 ⇒ HTTP Method(GET, POST, PUT, DELETE)를 이용하여 CRUD를 적용
    
    구성요소: HTTP URI, HTTP Method, HTTP Message Payload
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fec4f20ff-66fe-42bf-b9d7-7f8a27375791%2FUntitled.png?table=block&id=b90f11e1-af1d-4b65-8eb2-ac79383cdeb2&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F631de34b-8300-4030-b1ec-494d11d4ca9c%2FUntitled.png?table=block&id=1583651e-5f60-47ba-9990-16a814c881aa&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ## Docker Client
    
    ## Docker Host
    
    ### Docker Daemon: Object를 관리하거나 Docker API 요청을 기다리기 위한 프로세스
    
    ### Docker Object(images, containers, networks, volumes, plugins 포함)
    
    Images: 도커 컨테이너를 만들기위한 read-only 템플릿
    
    Containers: Image 가 동작하고 있는 인스턴스를 의미
    
    ## Docker registry: Docker 이미지를 저장하기 위한 공간(public, private)
    
    [Docker Private Registry](http://judo0179.tistory.com/32)
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F03cdbe68-8978-4daf-8e58-c48b2ef5f501%2FUntitled.png?table=block&id=3b557981-f46c-4cab-b49d-88687b4bc352&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    ## Docker platform?
    
    ## Docker Engine?
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa4435896-7d0c-4116-89d7-09f9affff68c%2FUntitled.png?table=block&id=deb2bf90-604b-4df1-b366-4d2f8d779ff2&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    Docker CLI, Docker Engine API, Docker Daemon(server)
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F90f8fb8d-5e5e-46cb-9e0a-8c082c0dbdc2%2FUntitled.png?table=block&id=89258e25-ee17-4dcc-ae7a-96f4be288706&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)
    
    dockerd: object 관리 & REST API 요청 처리
    
    containerd: 컨테이너의 라이프사이클 관리
    
    gRPC: Google에서 개발한 RPC 방식(RPC: 원격지의 자원을 가져와서 로컬처럼 사용)
    
    IPC 방식은 일련의 통신과정을 개발자가 직접 구현
    
    shim: init 과 같은 역할
    
    runC: container runtime
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6e4bbfb8-f8b3-4f9f-835d-b14786fc3439%2FUntitled.png?table=block&id=c1cbdba9-051c-4bf9-83f9-4e01b9ab5e35&spaceId=ae7a77d7-affd-4cb7-ade5-4e864d03f9e7&width=1920&userId=320669f8-b576-40b2-82a4-2c596c3240e9&cache=v2)