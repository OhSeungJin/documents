# iotop

- `top` 의 경우 특정 프로세스가 사용하는 CPU, Memory 사용률을 모니터링 하는 도구이다. 이와 비슷한게 `iotop` 의 경우에는 disk I/O 를 많이 유발하는 프로세스를 찾아낼 수 있도록 프로세스별 IO 사용량을 보여준다.


## Install

```bash
$ sudo apt-get install iotop
```

## Run iotop

- root 권한으로 실행해야 한다.
```bash
$ sudo iotop
```

### Useful Option 
- `-o` : 아무 옵션 없이 `iotop` 을 수행할 경우에는 모든 프로세스가 결과로 뜬다. 이 때 실제 IO를 하는 프로세스만 보고싶으면 `-o` 옵션을 사용하면 된다.
- `-a` : iotop 에서 1초 마다 계속 순간 값이 갱신되기 때문에 긴 시간 동안의 IO 양을 모니터링하기가 어렵다. 이에 누적 IO 양을 확인하고 싶은 경우 `-a` 옵션을 사용하면 `iotop` 명령 시작 시점부터 disk IO 양이 누적된다.


## io top result
- `iotop` 명령을 수행하면 아래의 사진과 같은 결과를 얻을 수 있다.
- Disk 에 내려오는 총 write, read 양이 오른쪽 위에 출력되며 `top` 명령어 수행 시에 같이 아래에 프로세스마다 정보가 나오며 1초마다 갱신된다.
- 각각의 프로세스(쓰레드)가 내리는 IO 를 read, write 로 분리해서 확인할 수 있다. 예를 들어 아래의 사진에서 java 프로그램 쓰레드가 5개 동작하고 있으며 해당 상위의 프로세스들이 주로 read 를 아래의 한 쓰레드가 RW 를 같이 수행함을 알 수 있다. 


![image](https://user-images.githubusercontent.com/18457707/77458152-0e4bce00-6e41-11ea-8ad7-418d086ca41d.png)
