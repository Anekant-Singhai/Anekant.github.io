
### JSluice
```
echo "http://x/y.js" | jsluice urls <(curl -sk "$url") | jq -r '.url, .queryParams[], .bodyParams[], .method' | sed 's/null//g' | awk '{ORS=NR%6?",":"\n"}1' | awk 'BEGIN{FS=","} {printf "%s%s%s%s%s\r\n\r\n", $1, ($2?"?"$2:""), ($3?"&"$3:""), ($4?"?"$4:""), ($5?"&"$5:"")}'
```

echo "http://x/y.js" | /root/go-workspace/bin/jsluice urls <(curl -sk "$url") | jq -r '.url, .queryParams[], .bodyParams[], .method' | sed 's/null//g' | awk '{ORS=NR%6?",":"\n"}1' | awk 'BEGIN{FS=","} {printf "%s%s%s%s%s\r\n\r\n", $1, ($2?"?"$2:""), ($3?"&"$3:""), ($4?"?"$4:""), ($5?"&"$5:"")}'
