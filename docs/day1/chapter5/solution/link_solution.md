# [답지] 링크

```bash
cd ~/inode

ln hello.sh ~/inode/1/hello_h.sh
~/inode/1/hello_h.sh

ln -s ~/inode/hello.sh ~/inode/2/hello_s.sh
~/inode/2/hello_s.sh

rm hello.sh
~/inode/1/hello_h.sh
~/inode/2/hello_s.sh
```

원본 삭제 후 하드 링크는 실행되지만, 심볼릭 링크는 원본 경로가 사라져 실행되지 않는다.
