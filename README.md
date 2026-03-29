## Жарков Матвей ИУ8-23
```
$ git clone https://github.com/MatveyZK/lab03 .
Cloning into '.'...
remote: Enumerating objects: 284, done.
remote: Counting objects: 100% (284/284), done.
remote: Compressing objects: 100% (122/122), done.
remote: Total 284 (delta 134), reused 279 (delta 132), pack-reused 0 (from 0)
Receiving objects: 100% (284/284), 1.11 MiB | 333.00 KiB/s, done.
Resolving deltas: 100% (134/134), done.
$ git remote rm origin
$ git remote add origin https://github.com/MatveyZK/lab4
$ mkdir .github
$ mkdir .github/workflows
$ cd .github/workflows/
$ nano lab4.yml
$ cat lab4.yml 
name: lab4

on:
 push:
  branches: [master]
  pull_request: [master]

jobs:
 Linux: 
  runs-on: ubuntu-latest
  steps: 
  - uses: actions/checkout@v3
   
  - name: Solver
    run: |
     cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build
     cmake --build ${{github.workspace}}/solver_application/build
   
  - name: Hello_world
    run: |
     cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build 
     cmake --build ${{github.workspace}}/hello_world_application/build  
 
 Windows:
  runs-on: windows-latest
  steps:
  - uses: actions/checkout@v3
    
  - name: Solver
    run: |
     cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build 
     cmake --build ${{github.workspace}}/solver_application/build 
   
  - name: Hello_world
    run: |
     cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build 
     cmake --build ${{github.workspace}}/hello_world_application/build 
$ git add .
$ git commit -m "new yml"
$ git push origin master
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 374 bytes | 374.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/MatveyZK/lab4
   55338af..08669b0  master -> master
```
В л/р 3 скорее всего нужно было добавить папку build в gitignore, но в инструкции этого не было, поэтому пришлось
удалить файлы кеша Cmake, чтобы не возникало конфликтов
