```bash
## platform x86, ubuntu 20.04
(command -v jq >/dev/null 2>&1 || ( apt update &&  apt install jq -y)) && \
(command -v curl >/dev/null 2>&1 ||  apt install curl -y) && \
jq -r 'select(.symbol=="TSLA" and .side=="sell") | .order_id' ./transaction-log.txt | xargs -I {} curl -s "https://example.com/api/{}" >> ./output.txt
```
