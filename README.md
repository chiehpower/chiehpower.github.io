# Docker 

## Build 
```
cd docker
docker build -t chiehpower/blog:0.1 .
cd .. 
docker run -ti --name blog -p 5000:5000 -v $PWD:/workspace/blog chiehpower/blog:0.1 bash
```

## Usage:
git clone your repository
Enter the folder.
```
npm install -g hexo-cli 
```