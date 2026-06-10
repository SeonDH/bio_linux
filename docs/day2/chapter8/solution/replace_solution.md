# [답지] 텍스트 검색과 대치

```bash
vi practice4.txt
```

## 검색

```text
/foo
n
N
?foo
```

## 바꾸기

```text
:s/foo/bar
:s/foo/bar/g
:%s/foo/bar/g
u
:1,2s/foo/bar
u
:1,2s/foo/bar/g
u
:1,3s/foo/bar/gc
```

`gc` 옵션에서는 바꿀지 물어볼 때 `y`를 누르면 바꾸고, `n`을 누르면 건너뛴다.
