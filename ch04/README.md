## <u>Chapter 4.</u> 편집기의 활용

* 과거 유닉스부터 현재 대부분의 리눅스 배포판에서 사용되는 vi 편집기를 이용해보기
* https://vim-adventures.com/

### <u>4.1.</u> 리눅스에서의 편집기

<u>편집기의 개요</u>

* 모드형 편집기 (Mode Type Editor)
  * 입력모드와 명령모드가 명확히 구분된 편집기
  * 입력모드: 문서에 글자를 입력할 수 있는 모드(상태)
  * 명령모드: 내용 수정 및 편집 가능한 모드(상태)
  * 리눅스의 vim 등
* 비모드형 편집기 (Non-mode Type Editor)
  * 입력모드와 명령모드가 구분되어 있지 않은 편집기
  * 윈도우의 메모장, 노트패드 등
  * 리눅스의 gedit 등

<u>리눅스의 편집기</u>

* X윈도 이후, 리눅스에서는 많은 패키지가 GUI 환경에서 수행되면서 gedit 이라는 GUI 편집기를 제공함
  (gedit 은 윈도우의 메모장과 유사함)
* 서버용 운영체제로 사용되는 리눅스의 경우, X윈도를 사용하지 않을 수 있음
  (클라이언트 시스템은 사용자 편의성을 위해 GUI 를 제공하나 서버 시스템은 보통 CLI 임)
* 터미널 환경의 리눅스 시스템에서는 대표적인 모드형 편집기인 vim 을 제공
  (입력모드, 명령모드, 라인모드를 사용하여 문서 편집)
* vim 은 유닉스 편집기였던 vi 의 기능을 개선시킨 편집기

### <u>4.2.</u> vi 편집기 사용법

##### <u>4.2.1.</u> vi 편집기의 실행 저장 종료

<u>(1)</u> vi 편집기 실행

* `vi` 명령어만 입력

  ```bash
  $ vi
  ```

* `vi` 명령어와 파일이름을 추가로 입력

  ```bash
  $ vi test.txt
  ```

  > test.txt 가 존재하면 해당 파일을 불러오고 없으면 편집 후 저장할때 새로 생성됨

<u>(2)</u> 파일의 저장

* 라인모드에서 파일 저장이 가능함
  (라인모드 진입: 명령모드에서 `:` 입력)

* `w` 명령

  * 현재 작업물 저장 명령

    ```bash
    :w
    ```

    > 이름없는 작업물이거나 새로운 이름으로 저장하려면, 파일 이름을 인자로 넣어야함 (`:w test.txt`)

  * 강제 저장

    ```bash
    :w!
    ```

    > 위와 달리, 경고 메세지를 출력하지 않고 저장을 수행함
    >
    > 이 경우, 강제로 파일 덮어쓰기 등 의도치 않은 상황이 발생할 수 있어 주의해서 사용해야함

<u>(3)</u> vi 편집기 종료

* `q` 명령

  ```bash
  :q
  ```

  > 파일 수정 이후 해당 명령어 입력 시, 저장을 권유하는 경고 메세지가 뜨고 편집기 종료도 되지 않는다.

* 저장하고 종료

  ```bash
  :wq
  ```

  ```bash
  :x
  ```

  > `:wq` 명령이 워낙 자주 쓰이다보니 `:x` 로 축약시켜 사용하기도함

* 수정한 내용 저장하지 않고 종료

  ```bash
  :q!
  ```

<u>(Exercise)</u>

1. vi 편집기 실행

   ```bash
   $ vi
   ```

2. vi_test1.txt 라는 이름으로 저장

   ```bash
   :w vi_test.txt
   ```

3. "Hello" 입력 후, 저장

   ```bash
   Hello
   :w
   ```

4. 새로운 이름 vi_test2.txt 으로 저장

   ```bash
   :w vi_test2.txt
   ```

5. "world" 입력 후, 저장

   ```bash
   world
   :w
   ```

6. 두 파일에 내용을 확인

   ```bash
   $ cat vi_test1.txt
   Hello world
   $ cat vi_test2.txt
   Hello
   ```

##### <u>4.2.2.</u> vi 편집기의 모드

<u>(1)</u> 모드의 역할

* vi 편집기는 입력/명령/라인 등 3가지 모드를 가짐
* 입력모드: 문자를 입력할 수 있는 상태
* 명령 모드: 명령어를 통한 수정, 삭제 등 편집 작업을 할 수 있는 상태
* 라인모드: 현재 작업 저장, 편집기 종료 등 편집기 자체에 대한 작업을 할 수 있는 상태

<u>(2)</u> 모드의 전환

입력모드와 명령모드 사이의 전환

* 입력모드에서 명령모드로 전환
  * `ESC` 키를 누름
  * 문서에 문자 입력 불가능, 문서 편집을 위한 명령어만 입력 가능
* 명령모드에서 입력모드로 전환
  * 입력모드로 전환하는 명령어(`a`, `A`, `i`, `I`, `o`, `O`)들 중 하나를 입력
  * 편집기를 열면 처음에는 명령모드임

명령모드와 라인모드 사이의 전환

* 명령모드에서 라인모드로 전환
  * 라인모드로 전환하는 명령어(`:`,`?`,`/`)들 중 하나를 입력
  * `/`, `?`: 문서 내의 특정 단어 검색 등
  * `:`: 문서 저장, 편집기 종료 등
* 라인모드에서 명령모드로 전환
  * `ENTER` 혹은 `ESC` 키를 누름

입력모드와 라인모드 사이의 전환

* 입력모드에서 명령모드로 전환하고 명령모드에서 라인모드로 전환해야함
* 반대도 마찬가지임

### <u>4.3.</u> 명령 모드의 명령키

##### <u>4.3.1.</u> 문자의 입력, 수정, 삭제

<u>(1)</u> 문자의 입력

* 명령모드에서 `a`, `A`, `i`, `I`, `o`, `O` 중 하나를 사용하여 입력모드로 진입하여 문자를 입력

| 명령키 | 설 명                                                      |
| :----: | ---------------------------------------------------------- |
|  `a`   | 현 커서 기준 다음칸에 문자 입력                            |
|  `A`   | 현 커서 기준 문장 맨 끝에 문자 입력                        |
|  `i`   | 현 커서 기준 현재칸에 문자 입력 (제일 많이씀)              |
|  `I`   | 현 커서 기준 문장 맨 앞에 문자 입력                        |
|  `o`   | 현 커서 기준 문장 아래에 새로운 빈 문장을 만들고 문자 입력 |
|  `O`   | 현 커서 기준 문장 위에 새로운 빈 문장을 만들고 문자 입력   |

<u>(Exercise)</u>

1. vi 편집기 실행 후, '2, korea japan' 을 입력

   ```bash
   $ vi
   2. korea japan
   ~
   ```

2. 방향키를 쓰지 않고 입력한 문장 맨 끝에 'china' 입력

   * 명령모드에서 `A` 입력 후, 'china' 입력

3. 'japan' 과 'china' 사이에 'taiwan' 입력

4. 방향키를 쓰지 않고 현재 문장 위에 '1. usa canada' 를 입력

   * 명령모드에서 `O` 입력 후, '1. usa canada' 입력

<u>(2)</u> 문자의 수정

| 명렁키  | 설 명                                                        |
| :-----: | ------------------------------------------------------------ |
|   `r`   | 한문자 덮어쓰기                                              |
|   `R`   | `ESC` 입력 전까지 덮어쓰기                                   |
| `[n]s`  | 현 커서 기준 다음 n개의 문자를 지우고 입력모드 집입          |
| `[n]S`  | 현 커서 기준 다음 n개의 문장을 지우고 입력모드 진입          |
| `[n]cw` | 현 커서 기준 다음 n개의 단어를 지우고 입력모드 진입          |
|   `C`   | 현 커서부터 해당 문장 끝까지 모든 문자를 지우고 입력모드 진입 |
| `[n]cc` | 현 커서 기준 다음 n개의 문자를 지우고 입력모드 집입          |

<u>(3)</u> 문자의 삭제

|   명령키   | 설 명                                              |
| :--------: | -------------------------------------------------- |
|   `[n]x`   | 현 커서 포함 뒤의 n개 문자 삭제 (`del`)            |
|   `[n]X`   | 현 커서 포함 앞의 n개 문자 삭제 (`backspace`)      |
|  `[n]dw`   | 현 커서 포함 뒤의 n개의 단어 삭제                  |
| `d^`, `d0` | 현 커서 기준 문장 처음부터 커서 위치까지 문자 삭제 |
| `d$`, `D`  | 현 커서 기준 커서 위치부터 문장 끝까지 삭제        |
|  `[n]dd`   | 현 커서 포함 아래 n개 문장 삭제                    |

<u>(Exercise)</u>

1. 첫번째 행의 "canada" 를 "Canada" 로 변경

   * "c" 에 커서를 위치시키고 `r` 을 입력하고 "C" 를 입력

2. 두번째 행의 "korea" 를 "Korea" 로 변경

   * "k" 에 커서를 위치시키고 `r` 을 입력하고 "K" 를 입력

   * "k" 에 커서를 위치시키고 `cw` 를 입력하고 "Korea" 를 입력

3. 두번째 행의 "taiwan" 이후의 문자를 삭제

   * "t" 에 커서를 위치시키고 `3cw` 입력
   * "t" 에 커서를 위치시키고 `3dw` 입력
   * "t" 에 커서를 위치시키고 `d$` 입력

4. 두 문장을 모두 삭제

   * 첫번째 행에 커서를 위치시키고 `2dd` 입력

##### <u>4.3.2.</u> 커서와 화면의 이동

* 리눅스 배포판마다 화살표 키를 이용한 커서 이동이 불가능 한 경우, 커서 이동법에 대해 알아두면 좋음

<u>(1)</u> 문자 단위 이동

* `h`: 왼쪽으로 한 칸 이동
* `j`: 아래쪽으로 한 칸 이동
* `k`: 위쪽으로 한 칸 이동
* `l`: 오른쪽으로 한 칸 이동

<u>(2)</u> 단어 단위 이동

* `w`, `W`: 현재 커서 기준 다음 단어의 첫 문자로 커서 이동
* `b`, `B`: 현재 커서 기준 이전 단어의 첫 문자로 커서 이동

<u>(3)</u> 문장 단위 이동

|    명령키     | 설 명                                           |
| :-----------: | ----------------------------------------------- |
|   `^`, `0`    | 현 커서가 위치한 문장의 첫번째 문자로 커서 이동 |
|      `$`      | 현 커서가 위치한 문장의 마지막 문자로 커서 이동 |
| `[n]+`, `[n]` | 현 커서 기준 n번째 아래 문장으로 이동           |
|    `[n]-`     | 현 커서 기준 n번째 위 문장으로 이동             |
|      `H`      | 현 화면 기준 제일 위 문장으로 이동              |
|      `M`      | 현 화면 기준 가운데 문장으로 이동               |
|      `L`      | 현 화면 기준 제일 아래 문장으로 이동            |

<u>(4)</u> 화면 단위 이동

|       명령키       | 설 명                                                        |
| :----------------: | ------------------------------------------------------------ |
| `ctrl+F`(Forward)  | 커서를 아래 화면으로 이동                                    |
| `ctrl+B`(Backward) | 커서를 위 화면으로 이동                                      |
|   `ctrl+D`(Down)   | 커서를 아래 화면으로 반만큼 이동                             |
|    `ctrl+U`(Up)    | 커서를 위 화면으로 반만큼 이동                               |
|      `ctrl+Y`      | 커서를 한 행씩 아래 화면으로 이동                            |
|      `ctrl+E`      | 커서를 한 행씩 위 화면으로 이동                              |
|    `[n]shift+G`    | 커서를 문서의 제일 마지막 문장으로 이동<br />(`5shift+G` 는 `:5`와 같이 5번 라인으로 커서 이동) |
|        `gg`        | 커서를 문서의 제일 처음 문장으로 이동                        |

##### <u>4.3.3.</u> 작업 취소, 반복

<u>(1)</u> 작업 취소

* `u`(undo): 이전 작업 취소

<u>(2)</u> 작업 반복

* `.`: 직전 작업 반복 수행

##### <u>4.3.4.</u> 복사하기, 오려두기

<u>(1)</u> 복사하기 (`y`, yank)

* 문서의 특정 부분의 내용을 버퍼에 저장

| 명령어  | 설 명                                               |
| :-----: | --------------------------------------------------- |
|  `yw`   | 현 커서를 포함한 단어를 복사                        |
|  `y0`   | 현 커서가 있는 문장의 처음부터 커서까지 문자들 복사 |
|  `y$`   | 현 커서부터 문장 끝까지의 문자들 복사               |
| `[n]yy` | 현 커서 포함한 아래 n개의 문장 복사                 |

<u>(2)</u> 오려두기

* `d` 명령을 통해 문자를 삭제하면 삭제한 내용을 버퍼에 저장함
* 즉, 엄밀하게 말하면 `d` 명령은 삭제가 아닌 오려두기임

<u>(3)</u> 붙이기 (`p`, paste)

* `p`: 버퍼에 저장된 내용을 커서 아래 혹은 뒤에 붙임
* `P`:버퍼에 저장된 내용을 커서 위 혹은 앞에 붙임

<u>(Exercise)</u>

1. "KOREA" 단어를 복사
   * "K" 에 커서를 위치시키고 `yw` 명령어로 복사
2. 복사한 단어를 "usa" 와 "canada" 사이에 붙여넣기
   * 두 단어 사이 공백문자에 커서를 위치시키고 `p` 명령어로 붙여넣기
3. 두번째 문장을 복사
   * 두번째 문장에 커서를 위치시키고 `yy` 명령어로 복사
4. 복사한 문장을 첫번째 문장 위로 붙여넣기
   * 첫번째 문장에 커서를 위치시키고 `P` 명령어로 붙여넣기

### <u>4.4.</u> 라인모드의 사용

##### <u>4.4.1.</u> 문장 번호 삽입과 문장 이동

* 편집기에서 문장번호를 화면상으로 띄우면 편집할 때 보기 좋음

  ```bash
  :set nu
  ```

  ```bash
  :set number
  ```

  > 문장번호 화면상에서 제거는 `:set nonu` 혹은 `:set nonumber`

* 특정 행으로 커서 이동

  ```bash
  :[n]
  ```

  > `[n]shift+G` 와 동일한 명령임

##### <u>4.4.2.</u> 복사하기와 오려두기

* 라인모드에서도 복사하기, 오려두기 수행 가능
* 복사하기, 오려두기 수행을 적용할 범위를 지정하는 것이 선행되어야함

<u>(1)</u> 범위 지정

* 범위 지정 형식

  ```bash
  시작, 끝
  ```

  | (특수)문자 | 설 명                            |
  | ---------- | -------------------------------- |
  | 숫자       | 문장 행 번호 의미                |
  | `$`        | 마지막을 의미                    |
  | `%`        | 전체를 의미                      |
  | `.`        | 현재 커서가 위치한 문장을 가리킴 |

  * `:1,$`, `:%`: 문장 전체를 범위로 지정

  * `:5,10`: 5행부터 10행까지 범위로 지정
  * `:1,.`: 1행부터 현재 커서가 있는 문장행까지 범위로 지정
  * `:.,$`: 현재 커서가 있는 문장행부터 마지막행까지 범위로 지정

<u>(2)</u> 복사하기

* `:[n]y`: 현재 커서 기준, n번째 아래 문장 복사
* `:범위y`: 지정한 범위의 내용을 버퍼에 저장

<u>(3)</u> 오려두기

* `:[n]d`: 현재 커서 기준, n번째 아래 문장을 삭제하고 버퍼에 저장
* `:범위d`: 지정한 범위의 내용을 삭제하고 버퍼에 저장

<u>(4)</u> 붙이기

* `[n]pu`: 현재 커서 기준, n번째 아래 라인에 버퍼에 저장된 내용 붙이기

<u>(Exercise)</u>

1. 아래 내용을 vi 편집기를 열어 입력하고 저장

   ```bash
   a. korea
   b. japan
   c. china
   ```

2. 각 문장에 번호가 출력되도록 명령어 입력

   * `set nu` 혹은 `set number` 명령어 입력

3. 세 문장을 모두 범위로 지정하여 복사

   * `:1,3y`, `:%y`, `:1,$y` 중 하나의 명령어 입력

4. 복사한 내용을 3번 문장 아래에 붙여넣기

   * `:3pu`

5. 5~6번 문장 오려두기

   * `:5,6d`

6. 오려둔 내용을 3번 문장 아래에 붙여넣기

   * `:3pu`

##### <u>4.4.3.</u> 문자열 검색과 변경

<u>(1)</u> 문자열 검색

* `/`, `?` 명령어를 통해 찾고 싶은 문자열을 검색함

  ```bash
  :/STRING 이후 `n` 혹은 `N`
  :?STRING 이후 `n` 혹은 `N`
  ```

  |   명령어   | 설 명                                    |
  | :--------: | ---------------------------------------- |
  | `:/STRING` | 현재 커서 기준 아래 방향으로 문자열 검색 |
  | `:?STRING` | 현재 커서 기준 위 방향으로 문자열 검색   |
  |    `n`     | 검색 순방향으로 다른 문자열 검색         |
  |    `N`     | 검색 역방향으로 다른 문자열 검색         |

<u>(2)</u> 문자열 변경

* `s`: 검색된 문자열을 다른 문자열로 바꾸는 명령어

|           명령어            | 설 명                                                        |
| :-------------------------: | ------------------------------------------------------------ |
|     `:s문자열1/문자열2`     | 현 커서 행에서 발견된 첫번째 "문자열1"을 "문자열2"로 변경    |
|    `:s문자열1/문자열2/c`    | 현 커서 행에서 발견된 첫번째 "문자열1"을 "문자열2"로 변경 (변경 여부 물어봄) |
|    `:s문자열1/문자열2/g`    | 현 커서 행에서 발견된 모든 "문자열1"을 "문자열2"로 변경      |
|   `:%s문자열1/문자열2/g`    | 현 문저 내에서 발견된 모든 "문자열1"을 "문자열2"로 변경      |
| `:<범위>s문자열1/문자열2/g` | 지정된 범위 내에서 발견된 모든 "문자열1"을 "문자열2"로 변경  |

<u>(Exercise)</u>

0. vi 편집기를 열어 아래 내용 입력 후 저장

   ```bash
   I like linux and like ubuntu
   I studying ubuntu now
   I like kpops
   I like bearutiful flower
   I like steak
   ```

1. 첫번째 문장에서 처음 등장하는 "like"를 "love"로 변경

   * `:1s/like/love`

2. 첫번째 문장에서 처음 등장하는 "like"를 "love"로 변경 (변경 여부 묻기)

   * `:1s/like/love/c`

3. 첫번째 문장의 모든 "like"를 "love"로 변경

   * `:1s/like/love/g`

4. 현재 문서의 모든 "like"를 "love"로 변경

   * `:%s/like/love/g`

5. 첫번째 문장부터 세번째 문장 사이의 모든 "love"를 "like"로 변경

   * `:1,3s/like/love/g`

##### <u>4.4.4.</u> 기타 라인 모드의 기능 사용

<u>(1)</u> 파일 불러오기 및 전환

* 라인모드에서 다른 파일을 불러와 현재 커서 위치에 삽입 가능

* 현재 작업한 파일 저장 이후, vi 편집기 종료 없이 다른 파일 불러오기 가능

* vi 편집기를 켤 때, 여러 파일을 동시에 불러오기 가능

  ```bash
  vi FILENAME1, FILENAME2, FILENAME3, ...
  ```

|    명령어     | 설 명                                                     |
| :-----------: | --------------------------------------------------------- |
| `:r FILENAME` | 지정한 파일을 현재 커서 아래에 삽입                       |
| `:e FILENAME` | 현재 작업 중인 파일에서 지정한 파일로 전환                |
|    `:[n]n`    | 여러 파일을 부른 경우, 현재 파일에서 n번 다음 파일로 전환 |
|    `:[n]N`    | 여러 파일을 부른 경우, 현재 파일에서 n번 이전 파일로 전환 |

<u>(2)</u> shell 사용

* vi 편집기 사용 중, 편집기 종료 없이 shell 명령어 실행 가능
* `:! SHELL_COMMAND`: 단일 shell 명령어 실행
* `:sh`: shell 프롬프트를 띄워 shell 명령어를 실행 (`exit` 명령어로 편집기로 돌아옴)

<u>(Exercise)</u>

1. 아래처럼 3개의 파일을 vi 편집기로 작성하고 저장

   ```bash
   This is a first file
   ~
   "firstfile.txt"
   ```

   ```bash
   This is a second file
   ~
   "secondfile.txt"
   ```

   ```bash
   This is a third file
   ~
   "thirdfile.txt"
   ```

2. vi 편집기로 firstfile.txt 파일을 불러온 다음, 파일 하단에 secondfile.txt 파일의 내용 삽입

   * `vi firstfile.txt`
   * `:r secondfile.txt`

3. 현재 작업을 저장하고 vi 편집기를 종료하지 않고 thirdfile.txt 로 전환

   * `:w` 이후 `:e thirdfile.txt`

4. vi 편집기를 종료하고 3개의 파일을 함께 열어보기

   * `vi firstfile.txt secondfile.txt thirdfile.txt`

5. secondfile.txt 로 전환

   * `:n` 혹은 `:e secondfile.txt`

6. vi 편집기로 firstfile.txt 열기

   ```bash
   $ vi firstfile.txt
   ```

7. 편집기 종료없이 `ls` 명령어 수행

   * `:ls`

8. 편집기 종료없이 shell 프롬프트 띄워서 `ls` 수행

   * `:sh` 이후,  `$ ls`

9. 편집기로 돌아오기

   * `$ exit`
