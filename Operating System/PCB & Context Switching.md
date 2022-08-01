# PCB & Context Switching

### Process Management

운영체제는 PCB에 담긴 프로세스 정보를 이용하여 프로세스를 관리하고 제어한다. 프로세스가 생성될 때 마다 고유의 PCB가 생성되어 메인 메모리에 유지되고, 프로세스가 완료되면 제거된다.

**Process Metadata**

- Process ID
- Process State
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memory Usage

이 메타데이터는 프로세스가 생성되면 `PCB(Process Control Block)`이라는 곳에 저장된다.

</br>

</br>

### PCB (Process Control Block)

프로세스 메타데이터들을 저장해 놓는 곳이다. 한 PCB 안에는 하나의 프로세스 정보가 담긴다.

```
프로그램 실행 -> 프로세스 생성 -> 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 -> 메타데이터 PCB에 저장
```

**PCB 필요한 이유**

CPU는 프로세스의 상태에 따라서 교체 작업이 이루어진다. 이때, 교체되는 프로세스의 상태 값을 PCB에 저장해두었다가 다시 수행할 때 사용한다.

**관리 방식**

연결 리스트 방식으로 관리된다. 삽입, 삭제가 용이하며 프로세스가 생성되면 해당 PCB가 생성되고, 프로세스가 완료되면 제거된다.

</br>

</br>

### Context Switching (문맥 교환)

CPU가 현재 작업 중인 프로세스에서 다른 프로세스로 넘어갈 때 지금까지의 프로세스 상태를 저장하고, 새 프로세스의 상태를 다시 적재하는 작업이다.

**Context Switching 발생하는 경우**

- 멀티태스킹 : 실행 가능한 프로세스들이 운영체제의 스케줄러에 의해 조금씩 번갈아가며 수행될 때 Context Switching 발생한다.
- 인터럽트 핸들링 : 인터럽트 발생 시 Context Switching이 일어난다.
- 유저모드와 커널모드 전환