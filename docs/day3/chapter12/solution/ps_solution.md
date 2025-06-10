# [답지] ps 실습

- 답자의 예시일 뿐이며 여러 답안도 가능하다.

1. 

```bash
$ ps -ef | grep sleep_script.sh | grep -v grep
```


2. 

```bash
$ kill {pid} 
```

or 

```bash
$ pkill -f sleep_script.sh
```