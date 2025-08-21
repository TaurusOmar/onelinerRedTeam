```bash
find / -perm /6000 -type f 2>/dev/null | awk 'BEGIN{while(( "curl -s https://gtfobins.github.io/"|getline l)>0){if(match(l,/\/gtfobins\/([^\/]+)\//,m))g[m[1]]=1}close("curl -s https://gtfobins.github.io/")} {p=$0;n=p;sub(/^.*\//,"",n);if(n in g)print "[MATCH] "p}' | tree --fromfile -C
```
