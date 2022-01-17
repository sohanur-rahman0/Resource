#### Check what is running on port 80
`netstat -tulpn | grep :80`
#### Kill process running on port 80
`sudo lsof -t -i tcp:80 -s tcp:listen | sudo xargs kill`