# VSCode를 위한 명령어

```bash
# VSCode로 현재 작업 위치에서 해당하는 file_path를 실행
$ code {file_path}
```

# directory create
```bash
$ mkdir {dir_name}
```

# 현재 위치의 list
```bash
$ ls
```

# 파일 생성
```bash
$ touch {file_path}
```

# 이동 / 수정
```bash
# 없는 {new_path}를 지정하면, {o}ld_path}에 해당하는 디렉토리 이름이 {new_path}로 변경됨
$ mv {old_path} {new_path}
```

# 삭제
```bash
# dir 삭제와 파일 삭제는 방법이 다름

# 파일 삭제 => rm은 단일 객체만 삭제 가능
$ rm {file_path}

# dir 삭제 => -r : recursion(재귀)
$ rm -r {dir_path}
```

# 작업 위치
```bash
$ cd {dir_path}

# 현재 위치의 상위 경로로 이동
$ cd ..
```

---

# CLI

- Command Line Interface
- 명령어를 통해 사용자와 컴퓨터가 상호작용하는 방식

### 왜 CLI를 사용해야 할까?

- 효율성
    - CLI는 키보드만으로 모든 작업을 수행할 수 있으며 메모리와 CPU사용량이 적어 저사양 시스템에서도 효율적으로 동작
- 정밀한 제어
    - 특정 프로그램이나 시스템의 세부 설정을 보다 정밀하게 제어할 수 있음
- 표준성
    - CLI 명령어는 대부분은 Unix 운영체제 기반 시스템에서 동일하게 작동하여 여러 환경에서 적용할 수 있음

### 절대 경로

- 파일 시스템의 루트 디렉토리부터 시작하는 경로

### 상대 경로

- 현재 작업하고 있는 디렉토리를 기준으로 계산된 상대적 위치를 작성한 것