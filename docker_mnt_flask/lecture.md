# 파일 구조
- 
```bash
(3.11.6) catherine@catherine-VirtualBox:~/Desktop/Docker_mnt/docker_mnt_flask$ tree
.
├── app.py
├── lecture.md
└── templates
    └── index.html

2 directories, 3 files
```

# 시나리오
- 1차 : 컨테이너 실행된 상태에서 HTML 파일 변경 후, 실제 웹에서 변경된 사항 확인
- 2차 : Dockerfile 생성 후, 1차 재확인
- 3차 : 테스트 완료 ==> 배포 (이미지 배포)
- 4차 : 자동화 (deploy.sh) 활용해서, 배포 완료 후, 다시 테스트 컨테이너 생성 (Tag 업데이트)

