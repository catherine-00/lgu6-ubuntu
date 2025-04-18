# ruby 관련 파일
- 파일명 : hello.rb

# 컨테이너 실행
```bash
docker container run \
--name ruby \
--rm \
--interactive \
--tty \
--mount type=bind,source="$(pwd)",destination=/my-work \
ruby:3.3.4 \
bash
```
